# Промпт 13 — Деплой в Yandex Cloud (оркестратор)

```
Разверни прод в Yandex Cloud через yc cli + Terraform из infra/. Folder, SA-ключ, домен — от владельца (Lockbox).

1. terraform plan → показать человеку сводку ресурсов и ориентировочную месячную стоимость (по прайсу YC) 🚦 → apply.
2. Managed PostgreSQL 18 (ru-central1, 1 хост s3-c2-m8 или меньше по нагрузке, PITR 7 дней, шифрование),
   Serverless Container backend (min 1 инстанс для джоб или отдельная Compute VM под pg-boss worker — выбери и
   обоснуй в DECISIONS.md), Object Storage + Cloud CDN для website и медиа, Certificate Manager (Let's Encrypt),
   Cloud DNS, Lockbox, Yandex Monitoring + алерты (5xx, p95, очередь джоб, неудачные webhook'и платежей) в MAX/email.
3. Пайплайн GitHub Actions: main → staging автоматически; тег v* → prod после ручного approve.
4. Миграции Prisma — отдельным шагом до выката; откат — предыдущий образ контейнера.
5. Webhook пересборки website из админки → Actions workflow_dispatch или Cloud Function сборки → выгрузка в Object Storage → инвалидация CDN.
6. Бэкапы: проверь восстановление на staging (runbook docs/runbooks/restore.md).
7. Перед переключением DNS: TTL 300 заранее, 301-редиректы проверены, Метрика подключена (после согласия), Вебмастер.
🚦 Переключение DNS — только по явному «да» владельца, в низкий сезон и не в день открытия записи.
```
