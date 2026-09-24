# Промпт 07 — Публичный сайт на Astro (builder)

```
Задача: website/ — публичный сайт по docs/01-TZ.md §5–6 и дизайн-токенам docs/03-design-brief.md
(после гейта дизайна — строго по Figma через docs/prompts/11-design-to-code.md).
Используй навыки: cro, copywriting (тексты — из content/ после этапа 14), schema, site-architecture.

1. Astro SSG, данные из backend API на этапе сборки; живые данные (слоты, «осталось N мест») — островами
   (client:visible), с серверным fallback-текстом «Посмотреть свободное время».
2. Страницы и URL — точно по карте сайта ТЗ §5. Хлебные крошки. 404 с CTA записи.
3. Главная — блоки строго в порядке ТЗ §5.1. Sticky-бар на мобиле скрывается, когда видна основная CTA (IntersectionObserver).
4. Мастер записи — остров React/Preact ≤ 35 КБ gzip, 4 шага, состояние в URL, таймер hold, обработка SLOT_TAKEN
   с альтернативами, лист ожидания, «сообщить, когда откроется». Формы: autocomplete, inputmode, маска телефона +7.
   Согласия — компонент ConsentCheckbox (не предустановлен, ссылка на /soglasie-pd/ открывается в новой вкладке).
5. Виджет /w/:serviceSlug — облегчённый мастер для iframe/ссылки из Яндекс Карт/VK/QR, noindex, сохраняет utm.
6. Шапка с кликабельным телефоном на всех страницах; в нерабочие часы — подсказка из ТЗ A2.
7. Cookie-бар (не модальный) и загрузчик Метрики только после согласия (docs/02 §2).
8. Шрифты: самохостинг (fontsource), subset, preload только для H1-шрифта. Картинки: astro:assets → AVIF/WebP, srcset,
   width/height, hero — fetchpriority=high. Никаких сторонних запросов, кроме разрешённых (docs/02 §7).
9. Тёмная тема по prefers-color-scheme + переключатель.
10. prefers-reduced-motion: без видео (постер), без параллакса.
Проверки: build, Lighthouse CI (mobile: perf ≥ 90, a11y ≥ 95, seo 100), Playwright-скриншоты 390 и 1440 всех шаблонов
страниц в docs/screens/, тест «нет запросов на чужие домены».
```
