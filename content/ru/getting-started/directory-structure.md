---
title: Структура директорий 
linktitle: Структура каталогов
description: Интерфейс командной строки Hugo формирует структуру директорий проекта, а далее на основе данных, конфигураций и программ (скриптов) размещенных в этих директориях формирует полноценный статический вебсайт в одной единственной директории.
date: 2017-01-02
publishdate: 2017-02-01
categories: [getting started,fundamentals]
keywords: [source, organization, directories]
menu:
  docs:
    parent: "getting-started"
    weight: 50
weight: 50
sections_weight: 50
aliases: [/overview/source-directory/]
toc: true
---

## New Site Scaffolding

{{< youtube sB0HLHjgQ7E >}}

Запуск генератора нового сайта `hugo new site` из командной строки, создаст структуру директорий со следующими элементами:

```txt
.
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── public
├── static
└── themes
```

## Назначение директорий в структуре

Ниже приведен общий обзор каждой из директорий со ссылками на каждый из соответствующих разделов в документах Hugo.

[`archetypes`](/ru/content-management/archetypes/)
: Вы можете создавать новые файлы контента в Hugo с помощью команды `hugo new`.
По умолчанию Hugo создает новые markdown файлы контента в директории `content`, с [заголовками Front Matter](/ru/content-management/front-matter/) сформированными на основе шаблонов размещенных в этой директории. По умолчанию шаблон содержит как минимум, с `date`, `title` (формируется из имени файла) и `draft = true`. Это экономит время и способствует согласованности для сайтов, использующих несколько типов контента. Вы также можете создавать свои собственные [архетипы][] с предварительно настроенными полями в заголовках Front Matter.

[`assets`][]
: Директория хранит все файлы, которые должны быть обработаны с помощью [Hugo Pipes](/hugo-pipes/). Только файлы, имеющие значения `.Permalink` или `.RelPermalink`, будут опубликованы в директории `public`. Примечание: Директория `assets` не создается по умолчанию.

[`config`](/ru/getting-started/configuration/)
: Hugo поставляется с большим количеством [директив конфигурации][].
[Каталог конфигурации](/getting-started/configuration/#configuration-directory) — это место, где эти директивы хранятся в виде файлов JSON, YAML или TOML. Каждый объект корневых настроек представляет собой отдельный файл, который также может быть размещен в отдельных директориях соответствующих окружениям используемым в Hugo (prodaction, staging или _default). 
Проекты с минимальными настройками и отсутствием требований к окружению могут использовать один файл `config.toml` в своем корне.

Многие сайты могут практически не нуждаться в настройке, но Hugo поставляется с большим количеством [директив конфигурации][] для более подробных указаний о том, как вы хотите, чтобы Hugo создавал сайт. Примечание: каталог `config` не создается по умолчанию.

[`content`][]
: Весь контент для вашего сайта будет находиться внутри этой директории. Каждая директория верхнего уровня в директории `content` считается [разделом контента][]. Например, если на вашем сайте есть три основных раздела — `blog`, `articles` и `tutorials`, — у вас будет три каталога: `content/blog`, `content/articles` и `content/`. учебники`. Hugo использует разделы для назначения [типов контента][] по умолчанию.

[`data`](/ru/templates/data-templates/)
: В дополнение к встроенным переменным Hugo вы можете указать свои собственные данные в шаблонах или шорткодах, которые извлекаются как из локальных, так и из динамических источников.
Этот каталог используется для хранения файлов с этими данными. Вы можете записать эти файлы в формате YAML, JSON или TOML. В дополнение к файлам, которые вы добавляете в эту папку, вы также можете создавать [шаблоны данных][], с динамическим содержимым.

[`layouts`][]
: Хранит шаблоны в виде файлов `.html`, которые определяют, как ваш контент будет отображаться на статическом веб-сайте. Шаблоны включают [страницы списков][lists], вашу [домашнюю страницу][], [шаблоны таксономий][], [шаблоны общих частей страниц][partials], [шаблоны отдельных страниц][singles] и многое другое.

[`static`][]
: Хранит весь статический контент: изображения, CSS, JavaScript и т. д. Когда Hugo создает ваш сайт, все ресурсы внутри вашей директории `static` копируются как есть. Хорошим примером использования директории `static` является [подтверждение права собственности на сайт в Google Search Console][searchconsole], когда вы хотите, чтобы Hugo скопировал полный файл HTML без изменения его содержимого.

{{% note %}}
Начиная с **Hugo 0.31** у вас может быть несколько директорий `static`.
{{% /note %}}

[`resources`][]
: Директория с кэшированными файлами для ускорения генерации. Может также использоваться авторами шаблонов для размщения файлов Sass, поэтому вам не нужно устанавливать препроцессор. Примечание: каталог `resources` по умолчанию не создается.

[архетипы]: /ru/content-management/archetypes/
[`assets`]: /ru/hugo-pipes/introduction#asset-directory/
[директив конфигурации]: /ru/getting-started/configuration/#all-configuration-settings
[`content`]: /ru/content-management/organization/
[разделом контента]: /ru/content-management/sections/
[типов контента]: /ru/content-management/types/
[шаблоны данных]: /ru/templates/data-templates/
[домашнюю страницу]: /ru/templates/homepage/
[`layouts`]: /ru/templates/
[`static`]: /ru/content-management/static-files/
[`resources`]: /ru/getting-started/configuration/#configure-file-caches
[lists]: /ru/templates/list/
[pagevars]: /ru/variables/page/
[partials]: /ru/templates/partials/
[searchconsole]: https://support.google.com/webmasters/answer/9008080#zippy=%2Chtml-file-upload
[singles]: /ru/templates/single-page-templates/
[starters]: /ru/tools/starter-kits/
[taxonomies]: /ru/content-management/taxonomies/
[шаблоны таксономий]: /ru/templates/taxonomy-templates/
[types]: /ru/content-management/types/
