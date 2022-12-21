---
title: Возможности Hugo
linktitle: Возможности Hugo
description: Hugo может похвастаться невероятной скоростью, надежным управлением контентом и мощным языком шаблонов, что делает его идеальным для всех видов статических веб-сайтов.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-01
menu:
  docs:
    parent: "about"
    weight: 20
weight: 20
sections_weight: 20
draft: false
toc: true
---

## Основные особенности

* [Чрезвычайно быстрая][] сборка (&lt; 1 ms на страницу)
* Полностью кроссплатформенный, с [простой установкой][install] на macOS, Linux, Windows и другие платформы.
* Визуализирует изменения на лету с помощью [LiveReload][] во время разработки.
* [Мощная шаблонизация][]
* [Возможность разместить сайт практически где угодно][hostanywhere]

## Организация проекта

* Простая [организация проекта][], включая его разделы.
* Кастомизация [URL][]
* Поддержка конфигурируемых [таксономий][], включающих категории и теги
* [Сортировка контента][] по своему усмотрению с использованием мощных [функций][] шаблонов
* Автоматическая генерация [оглавления][]
* [Динамическое создание][] меню
* Поддержка [человеко-понятных URL][]
* Поддержка шаблонов [Permalink][]
* Поддержка редиректов через [алиасы][]

## Содержание

* Встроенная поддержка Markdown и Emacs Org-Mode, а также других языков через *внешние помощники* (см. [поддерживаемые форматы][])
* Поддержка TOML, YAML, и JSON метаданных в парметрах в заголовках [Front Matter][]
* Полностью настраиваемая [домашняя страница сайта][]
* Множество [типов контента][]
* Автоматически и определяемые пользователем [краткие сведения о содержании][]
* Поддержка [Шорткодов][] чтобы включить расширенный контент в файлы с контентом на языке Markdown 
* Поддержка функционала генерации ["Времени чтения"][pagevars] страницы
* Поддержка функционала генерации ["Количества слов"][pagevars] на странице

## Дополнительные возможности

* Интегрированная поддержка сервиса комментариев [Disqus][] 
* Интегрированная поддержка [Google Analytics][]
* Автоматическая генерация [RSS][] ленты
* Поддержка [Go][] HTML шалонов
* [Подсветка синитаксиса][] с использованием [Chroma][]

[алиасы]: /ru/content-management/urls/#aliases
[Chroma]: https://github.com/alecthomas/chroma
[краткие сведения о содержании]: /ru/content-management/summaries/
[типов контента]: /ru/content-management/types/
[Disqus]: https://disqus.com/
[Динамическое создание]: /ru/templates/menu-templates/
[Чрезвычайно быстрая]: https://github.com/bep/hugo-benchmark
[Front Matter]: /ru/content-management/front-matter/
[функций]: /ru/functions/
[Go]: https://pkg.go.dev/html/template
[Google Analytics]: https://google-analytics.com/
[домашняя страница сайта]: /ru/templates/homepage/
[hostanywhere]: /ru/hosting-and-deployment/
[install]: /ru/installation/
[LiveReload]: /ru/getting-started/usage/
[организация проекта]: /ru/getting-started/directory-structure/
[pagevars]: /ru/variables/page/
[Permalink]: /ru/content-management/urls/#permalinks
[Мощная шаблонизация]: /ru/hugo-modules/theme-components/
[человеко-понятных URL]: /ru/content-management/urls/#pretty-urls
[RSS]: /ru/templates/rss/
[Шорткодов]: /ru/content-management/shortcodes/
[Сортировка контента]: /ru/templates/
[поддерживаемые форматы]: /ru/content-management/formats/
[Подсветка синитаксиса]: /ru/content-management/syntax-highlighting/
[оглавления]: /ru/content-management/toc/
[таксономий]:/ru/content-management/taxonomies/
[URL]: /ru/content-management/urls/
