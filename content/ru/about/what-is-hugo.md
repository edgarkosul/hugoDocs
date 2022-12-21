---
title: Что такое HUGO
linktitle: Что такое HUGO
description: Hugo — это быстрый и современный генератор статических сайтов, написанный на Go и разработанный, чтобы сделать создание веб-сайтов быстрым и  увлекательным.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-01
layout: single
menu:
  docs:
    parent: "about"
    weight: 10
weight: 10
sections_weight: 10
draft: false
aliases: [/overview/introduction/,/about/why-i-built-hugo/]
toc: true
---

Hugo — это универсальный фреймворк для веб-сайтов. С технической точки зрения, Hugo — это [генератор статических сайтов][]. В отличие от систем, которые динамически создают страницу с каждым запросом посетителя, Hugo создает страницы, когда вы создаете или обновляете свой контент. Поскольку веб-сайты просматриваются гораздо чаще, чем редактируются, Hugo разработан для обеспечения оптимального соотношения удобства для конечных пользователей, авторов и контент менеджеров веб-сайтов.

Веб-сайты, созданные с помощью Hugo, чрезвычайно быстры и безопасны. Сайты Hugo можно размещать где угодно, в том числе [Netlify][], [Heroku][], [GoDaddy][], [DreamHost][], [GitHub Pages][], [GitLab Pages][], [Surge][], [Firebase][], [Google Cloud Storage][], [Amazon S3][], [Rackspace][], [Azure][], and [CloudFront][] и хорошо работает с сервисами [CDN][]. Сайты Hugo работают без базы данных или зависимости от тяжелых сред выполнения, таких как Ruby, Python или PHP.

Пожалуй Hugo является идеальным инструментом для создания веб-сайтов с почти мгновенной сборкой, способной пресобираться сразу после внесения изменений.

## Насколько быстр HUGO?

{{< youtube "CdiDYZ51a2o" >}}

## Как работает HUGO?

С технической точки зрения, Hugo берет исходный каталог файлов и шаблонов и использует их в качестве исходных данных для создания полноценного веб-сайта.

## Кому следует использовать HUGO?

Hugo предназначен для людей, которые предпочитают писать в текстовом редакторе, а не в браузере.

Hugo предназначен для людей, которые хотят вручную кодировать свой собственный веб-сайт, не беспокоясь о настройке сложных сред выполнения, зависимостей и баз данных.

Hugo предназначен для тех, кто создает блог, сайт компании, портфолио, документацию, одну целевую страницу или веб-сайт с тысячами страниц.

[@spf13]: https://twitter.com/spf13
[Amazon S3]: https://aws.amazon.com/s3/
[Azure]: https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website
[CloudFront]: https://aws.amazon.com/cloudfront/ "Amazon CloudFront"
[DreamHost]: https://www.dreamhost.com/
[Firebase]: https://firebase.google.com/docs/hosting/ "Firebase static hosting"
[GitHub Pages]: https://pages.github.com/
[GitLab Pages]: https://about.gitlab.com/features/pages/
[Go language]: https://go.dev/
[GoDaddy]: https://www.godaddy.com/ "GoDaddy.com Hosting"
[Google Cloud Storage]: https://cloud.google.com/storage/
[Heroku]: https://www.heroku.com/
[Jekyll]: https://jekyllrb.com/
[Middleman]: https://middlemanapp.com/
[Nanoc]: https://nanoc.ws/
[Netlify]: https://netlify.com
[Rackspace]: https://www.rackspace.com/cloud/files
[Surge]: https://surge.sh
[contributing to it]: https://github.com/gohugoio/hugo
[rackspace]: https://www.rackspace.com/openstack/public/files
[генератор статических сайтов]: /ru/about/benefits/
[CDN]: https://ru.wikipedia.org/wiki/Content_Delivery_Network