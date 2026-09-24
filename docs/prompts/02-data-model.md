# Промпт 02 — Модель данных (builder)

```
Задача: реализовать Prisma-схему по docs/01-TZ.md §7 (все сущности MVP; Product/Order/GiftCertificate — пустые
модели-заготовки под релиз 2) + миграции + сиды.

Требования:
- id: uuidv7 (Postgres 18 `uuidv7()` по умолчанию).
- Деньги: Int копейки, суффикс Kop. Время: timestamptz (UTC).
- Exclusion constraint против двойной брони: добавь в SQL-миграции
  `CREATE EXTENSION IF NOT EXISTS btree_gist;` и таблицу `booking_resource_lock(resource_id uuid, booking_id uuid,
  during tstzrange, active boolean)` с `EXCLUDE USING gist (resource_id WITH =, during WITH &&) WHERE (active)`.
  Prisma не умеет exclusion — делай raw SQL миграцию и типизированный репозиторий.
- Индексы: Booking(startsAt), Booking(status, holdExpiresAt), WaitlistEntry(serviceId, status, position),
  Client(phoneE164 unique), Consent(clientId, type).
- `Consent` хранит docVersion; отдельная таблица `LegalDocument(type, version, text, publishedAt)`.
- Анонимизация: функция `anonymizeClient(clientId)` — имя «Удалено», телефон → sha256(phone+pepper), email null,
  сохраняет Booking/Payment. Тест.
- Zod-схемы в packages/contracts для всех DTO API (create/update service, booking request, waitlist request...).
- Сиды (реалистичные, на русском): 1 локация (Переслегино), 2 ресурса (хозяйка, мастерская), 3 категории,
  8 услуг (мастер-класс «Пастила своими руками» групповой 8 мест 120 мин; «Зефир» групповой; «Травяной чай и
  дегустация» 60 мин; «Экскурсия по плантации» 90 мин; индивидуальная услуга 60/90 мин и т. п.),
  PriceGroup'ы по длительности, ReleaseRule FIXED_MONTHLY (16 число 22:00) и DAILY_ROLLING (18:00, D+1),
  3 мероприятия, 1 акция, шаблоны сообщений (тексты — плейсхолдеры в тёплом тоне, пометка TODO(owner)).

Тесты: миграции применяются на чистую БД; exclusion реально не даёт пересечения (интеграционный тест);
анонимизация. Проверки: typecheck, lint, test.
```
