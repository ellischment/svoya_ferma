---
name: Лесная ягодка · Лесной
colors:
  background: "#ECE7DF"
  background-soft: "#F6F3EE"
  ink: "#2A2A26"
  ink-muted: "#5E5D56"
  accent: "#4A6B3A"
  on-accent: "#F6F3EE"
  line: "rgba(42,42,38,0.18)"
typography:
  display:
    fontFamily: Cormorant Garamond
    fontWeight: 400
    fontSize: { mobile: 40px, desktop: 96px }
    lineHeight: 1.05
  h2:
    fontFamily: Cormorant Garamond
    fontWeight: 400
    fontSize: { mobile: 36px, desktop: 60px }
  h3:
    fontFamily: Cormorant Garamond
    fontWeight: 500
    fontSize: { mobile: 24px, desktop: 28px }
  body:
    fontFamily: Onest
    fontWeight: 400
    fontSize: { mobile: 17px, desktop: 18px }
    lineHeight: 1.6
  small:
    fontFamily: Onest
    fontSize: 16px
  label:
    fontFamily: Onest
    fontWeight: 500
    fontSize: 14px
    letterSpacing: 0.14em
    textTransform: uppercase
  hand:
    fontFamily: Marck Script
    usage: "только слова Марины: подпись у логотипа, «с 2018 года», цитаты"
layout:
  maxWidth: 1280px
  gutter: { mobile: 24px, desktop: 80px }
  sectionGap: { mobile: 72px, desktop: 144px }
  spacingScale: [4, 8, 12, 16, 24, 32, 48, 72, 96, 144]
shapes:
  radius: 0
  divider: "1px solid {colors.line}"
components:
  button-primary:
    backgroundColor: "{colors.accent}"
    textColor: "{colors.on-accent}"
    height: 56px
    padding: "0 32px"
    typography: "{typography.label}"
    radius: 0
  button-secondary:
    backgroundColor: transparent
    border: "1px solid {colors.ink}"
    textColor: "{colors.ink}"
    height: 52px
  link-action:
    textDecoration: underline
    underlineOffset: 5px
  product-row:
    layout: "фото 64px слева, название антиквой 22px, вес и остаток, цена и «В корзину» ссылкой"
    divider: "{shapes.divider}"
---

## Overview
Спокойная редакционная упаковка фермерского производства: льняной фон, лесной зелёный как единственный акцент, изящная антиква и рукописная нота Марины. Ощущение — утро на плантации и деревянные полки с зефиром, а не глянцевый магазин. Много воздуха, мало элементов, одна главная кнопка на экран.

## Colors
Четыре цвета и линия. Фон `#ECE7DF` (лён), светлые блоки `#F6F3EE`, текст `#2A2A26`, акцент `#4A6B3A` (лес). Акцент — только кнопки, ссылки действий, выделенное курсивом слово в заголовке и подпись «Марина». Второго акцентного цвета нет. Контраст: текст 11,7:1, акцент на фоне 4,9:1, светлый текст на кнопке 5,5:1.

## Typography
Cormorant Garamond — заголовки и названия товаров; курсивом выделяется одно слово в заголовке («Дары псковских *лесов*»). Onest — весь текст, цены, навигация. Marck Script — только голос Марины. Текст не мельче 16 px. На сайте шрифты раздаются со своего сервера (не Google Fonts) — требование 152-ФЗ.

## Layout
Mobile-first, макет начинается с 390 px. Поля 24 px на телефоне и 80 px на компьютере, между блоками 72–144 px. Каталог на главной — прейскурант строками, а не сетка карточек. Фото — только реальные кадры Марины, её рук, ягод, цеха и упаковки.

## Elevation & Depth
Теней нет. Глубину создают фотографии и тонкие линии-разделители.

## Shapes
Всё прямоугольное, скругление 0. Разделители — линия 1 px цвета `line`.

## Components
Основная кнопка — заливка акцентом, капс с разрядкой, высота 56 px. Вторичная — контур цвета текста. Действия в строках товаров — подчёркнутые ссылки («В корзину», «Записаться»). Цели касания не меньше 44 px.

## Do's and Don'ts
Делаем: воздух, линии вместо карточек, одна кнопка на экран, живые фото, слова Марины её почерком, спокойное «разобрали — записаться».
Не делаем: кнопки-таблетки, тени, второй акцент, эмодзи, стоки, плашки-теги в каждом блоке, всплывающие окна, кричащие таймеры.
