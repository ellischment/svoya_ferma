# Промпт 03 — Движок записи (builder; самый важный этап)

```
Задача: реализовать модуль backend/src/booking по docs/01-TZ.md §8.1–8.6. Сначала тесты, потом код.

1. slots.ts — чистая функция computeSlots({service, location, resources, workingHours, timeOff, bookings,
   releaseRules, now, range, gridMin, earlyAccessToken?}) → Slot[] с полями {startsAt, endsAt, resourceIds,
   status: 'free'|'few'|'not_released', releaseAt?, seatsLeft?}.
   Учитывай буферы, групповую вместимость, таймзону локации, переходы на границах суток, «только для новых».
   Тесты-таблицы: ≥ 25 кейсов (включая: отпуск, буфер между сеансами, групповая 8 мест с 7 занятыми → few,
   слот до открытия записи → not_released с releaseAt, ранний доступ по токену).
2. release.ts — вычисление момента открытия для FIXED_MONTHLY / DAILY_ROLLING / WINDOW_DAYS + earlyAccess.
   Джоба `release-tick` (раз в минуту): при наступлении момента → событие `booking.released` → уведомления
   подписчикам «сообщить, когда откроется».
3. hold.ts — createHold(clientDraft, slot): одна транзакция: upsert Client по телефону → Booking(HOLD, 15 мин)
   → строки в booking_resource_lock (active) → для групповых проверка SUM(seats) ≤ capacity с блокировкой строки
   Event/слота (SELECT ... FOR UPDATE). Конфликт exclusion → типизированная ошибка SLOT_TAKEN + ближайшие
   альтернативы (3 слота).
   Джоба `hold-expire` (раз в минуту): HOLD с истёкшим holdExpiresAt → CANCELLED(hold_expired), lock.active=false,
   событие `slot.freed`.
4. waitlist.ts — join, leave, onSlotFreed(slot): найти первого подходящего WAITING по окну → HOLD 30 мин на него →
   OFFERED + уведомление; джоба `waitlist-offer-expire` → EXPIRED → следующий. Идемпотентность по slot+entry.
5. manage.ts — по manageToken: reschedule (в рамках политики), swapService (только внутри одного PriceGroup,
   без доплаты), cancel (расчёт возврата по политике → вызов PaymentProvider.refund). Каждое действие → событие.
6. policy.ts — настройки: holdMinutes, freeCancelHours, rescheduleUntilHours, depositMode (FIXED|PERCENT|FULL),
   depositValue. Значения по умолчанию безопасные, помечены TODO(owner).
7. API (Hono + OpenAPI + Zod из contracts):
   GET /api/slots?serviceId&locationId&from&to[&ea=token]
   POST /api/bookings/hold  → {bookingId, holdExpiresAt, payment: {confirmationUrl}}
   GET/POST /api/manage/:token (view, reschedule, swap, cancel)
   POST /api/waitlist, DELETE /api/waitlist/:id
   GET /api/events/:slug/availability
   Rate-limit на hold (по IP и телефону). Проверка согласия PD_PROCESSING обязательна в hold (иначе 422).
8. События доменной шины (in-process + pg-boss): booking.held, booking.confirmed, booking.cancelled,
   slot.freed, booking.released, waitlist.offered — на них подпишутся уведомления (этап 05).

ОБЯЗАТЕЛЬНЫЙ тест гонки: 50 параллельных createHold на один индивидуальный слот → ровно 1 успех, 49 SLOT_TAKEN.
Для группового на 8 мест с 60 параллельными запросами → ровно 8 успехов.
Проверки: typecheck, lint, test. Отчёт: таблица покрытия веток для slots/release/waitlist/policy (цель 100%).
```
