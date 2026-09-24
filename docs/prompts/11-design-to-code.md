# Промпт 11 — Из Figma в код (builder с Figma MCP)

```
Figma-файл: <ССЫЛКА>. Используй get_variable_defs, get_design_context, get_screenshot; навык figma-code-connect.

1. Выгрузи переменные в website/src/styles/tokens.css и webapp/src/styles/tokens.css (CSS custom properties,
   light/dark через [data-theme] и prefers-color-scheme). Один источник: packages/tokens (генерация из JSON).
2. Реализуй компоненты библиотеки в website (Astro-компоненты + острова) и webapp (React) с одинаковыми именами;
   Code Connect маппинг для ключевых компонентов.
3. Экран за экраном: сверяй с get_screenshot; Playwright-скриншоты 390/1440 → docs/screens/<экран>.png;
   расхождения > 4px по отступам или любые по цвету/шрифту — исправить.
4. Иллюстрации/фоны: экспорт SVG, оптимизация svgo; фото — через astro:assets.
5. Не добавляй ничего, чего нет в макете, кроме состояний ошибок/загрузки (по брифу).
Проверки: Lighthouse CI, a11y (axe) без нарушений serious/critical.
```
