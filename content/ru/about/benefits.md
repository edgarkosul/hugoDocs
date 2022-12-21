---
title: Преимущества генераторов статических сайтов
linktitle: Преимущества статики
description: Улучшенная производительность, безопасность и простота использования — вот лишь некоторые из причин, по которым генераторы статических сайтов так привлекательны.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-01
keywords: [ssg,static,performance,security]
menu:
  docs:
    parent: "about"
    weight: 30
weight: 30
sections_weight: 30
draft: false
aliases: []
toc: false
---

Цель генераторов веб-сайтов — преобразовать контент в HTML-файлы. Большинство из них являются «генераторами динамических сайтов». Это означает, что HTTP-сервер, то есть программа, которая отправляет файлы в браузер для просмотра, запускает генератор для создания нового HTML-файла каждый раз, когда конечный пользователь запрашивает страницу.

Со временем генераторы динамических сайтов были запрограммированы на кэширование своих HTML-файлов, чтобы предотвратить ненужные задержки в доставке страниц конечным пользователям. Кэшированная страница — это статическая версия веб-страницы.

Hugo делает шаг вперед в кэшировании, и все HTML-файлы пред загрузкой на HTTP-сервер генерируются  на локальном компьютере. Можно просмотреть файлы локально, прежде чем копировать их на HTTP-сервер. Поскольку файлы HTML не генерируются динамически, мы говорим, что Hugo является *генератором статических сайтов*.

Это имеет много преимуществ. Наиболее заметным является производительность. HTTP-серверы *очень* быстры при отдаче браузеру статических html файлов — настолько быстры, что вы можете эффективно размещать сайт на сервере с небольшой долей памяти и ЦП, которое необходимы были бы для аналогичного динамически генерируемого сайта. 

## Подробнее о генераторах статических сайтов

* ["An Introduction to Static Site Generators", David Walsh][]
* ["Hugo vs. WordPress page load speed comparison: Hugo leaves WordPress in its dust", GettingThingsTech][hugovwordpress]
* ["Static Site Generators", O'Reilly][]
* [StaticGen: Top Open-Source Static Site Generators (GitHub Stars)][]
* ["Top 10 Static Website Generators", Netlify blog][]
* ["The Resurgence of Static", dotCMS][dotcms]

["An Introduction to Static Site Generators", David Walsh]: https://davidwalsh.name/introduction-static-site-generators
["Static Site Generators", O'Reilly]: https://github.com/gohugoio/hugoDocs/files/1242701/static-site-generators.pdf
["Top 10 Static Website Generators", Netlify blog]: https://www.netlify.com/blog/2016/05/02/top-ten-static-website-generators/
[hugovwordpress]: https://gettingthingstech.com/hugo-vs.-wordpress-page-load-speed-comparison-hugo-leaves-wordpress-in-its-dust/
[StaticGen: Top Open-Source Static Site Generators (GitHub Stars)]: https://www.staticgen.com/
[dotcms]: https://dotcms.com/blog/post/the-resurgence-of-static
