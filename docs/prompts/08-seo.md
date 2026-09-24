# Промпт 08 — SEO и AI-поиск (seo-auditor + builder)

```
Используй навыки seo-audit, schema, ai-seo, site-architecture. Контекст: docs/01-TZ.md §11, docs/00-discovery.md F1–F6.
Регион: Великие Луки, Псковская область (+ Москва/онлайн, если есть локации). Поисковик №1 — Яндекс.

1. Семантика: составь кластеры запросов (без выдумывания частот — помечай «проверить в Вордстате»):
   мастер-классы (пастила, зефир, травяной чай, для детей, корпоратив), экскурсия на ферму/плантацию,
   продукция (зефир без сахара, пастила без сахара, травяной сбор, купить в Великих Луках/Пскове/доставка СДЭК),
   подарочный сертификат. Сохрани в docs/seo/semantics.md: кластер → URL → title → H1 → description.
2. Для каждого шаблона страницы — JSON-LD: LocalBusiness (+ подходящий подтип), Service+Offer, Event
   (eventStatus, eventAttendanceMode, location, offers.availability/price/url), Product+Offer, FAQPage,
   BreadcrumbList, AggregateRating только из реальных отзывов с согласием. Генерация из данных, не руками.
3. sitemap.xml (lastmod из updatedAt), robots.txt, canonical, hreflang не нужен, OpenGraph/VK-превью с
   автогенерацией OG-картинок (satori/resvg на сборке, шрифты локально).
4. llms.txt: кто мы, адрес, часы, услуги с ценами, как записаться (ссылка), политика.
5. 301-редиректы со старых URL Tilda (/politika, /politika-23156, /oferta, /oferta-52504, /members/login → /moi-zapisi/).
6. Перелинковка: услуга ↔ похожие услуги ↔ мероприятия ↔ товары («попробовать дома»).
7. Чек-лист для владельца (docs/seo/owner-tasks.md): Яндекс Вебмастер, Яндекс Бизнес (кнопка «Записаться» на
   /w/...?utm_source=yandex_maps), 2ГИС, VK-сообщество, NAP одинаковый везде, просьба об отзывах через автоматику C5.
Проверки: валидатор структурированных данных (schema.org validator / Яндекс), отсутствие дублей title/description,
все страницы 200 и в sitemap, noindex на /w/, /moi-zapisi/, /zapis/uspeh.
```
