# Промпт 01 — Бутстрап из шаблона vibe + Yandex Cloud

```
https://github.com/di-sukharev/vibe — установи этот шаблон в текущий репозиторий (не затирая docs/, CLAUDE.md,
CHECKLIST.md, .claude/agents/), будем делать из него систему онлайн-записи + сайт + магазин для
«Своя ферма / Лесная ягодка» (описание: docs/01-TZ.md). Но вместо Digital Ocean будем хостить это на
Yandex Cloud через yc cli. Мобильное приложение сейчас НЕ нужно (ветка main, без mobile).

Сделай:
1. Пройди CHECKLIST.md шаблона (его AGENTS.md требует этого) — ответы бери из docs/01-TZ.md.
   Слей правила шаблона из его CLAUDE.md/AGENTS.md с нашим CLAUDE.md (наши правила приоритетнее при конфликте).
2. Структура: backend/ (Bun+Hono+Prisma+Postgres 18, uuidv7), webapp/ (админка PWA + «Мои записи»),
   website/ (Astro, публичный сайт), packages/contracts (Zod), infra/ (Terraform для Yandex Cloud).
3. Добавь в backend очередь/планировщик на pg-boss (одна Postgres), модуль `jobs/`.
4. Замени авторизацию по email/паролю: вход по одноразовому коду на номер +7 (адаптер SmsProvider с
   реализациями `console` для dev и `smsru` заглушкой). Роли: OWNER, ADMIN, STAFF, CONTENT, CLIENT.
   Требование 406-ФЗ — см. docs/02-legal-152fz.md §3.
5. infra/: Terraform под ru-central1: Managed PostgreSQL (+ PITR бэкапы), Serverless Containers (backend),
   Object Storage + CDN (website static, фото), Lockbox (секреты), Certificate Manager, DNS.
   Не применяй terraform — только `terraform validate` и `plan` при наличии кредов; инструкция в docs/deploy-yc.md.
6. CI (GitHub Actions): typecheck, lint, unit, build всех пакетов; Lighthouse CI на website (порог из ТЗ §12).
7. Удали из шаблона всё, что тянет иностранные сервисы ПДн (Google Sign-In, Google Fonts, GA и т. п.).
8. `.env.example` для каждого пакета, с комментариями на русском.

Критерий готовности: `bun install && bun run typecheck && bun run lint && bun test && bun run build` зелёные;
`docker compose up` поднимает postgres + backend + webapp + website локально; docs/PROGRESS.md обновлён.
🚦 После — попроси у владельца: доступ yc (folder id, SA-ключ), домен, тестовые ключи ЮKassa или T-Банк, SMS-провайдер.
```
