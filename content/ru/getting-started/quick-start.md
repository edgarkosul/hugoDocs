---
title: Быстрый старт
linktitle: Быстрый старт
description: Создание сайта на Hugo, используя красивую тему Ananke.
date: 2013-07-01
publishdate: 2013-07-01
categories: [getting started]
keywords: [quick start,usage]
authors: [Shekhar Gulati, Ryan Watters]
menu:
  docs:
    parent: "getting-started"
    weight: 10
weight: 10
sections_weight: 10
draft: false
aliases: [/quickstart/,/overview/quickstart/]
toc: true
---

{{% note %}}
В этом кратком руководстве в примерах используется `macOS`. Инструкции по установке Hugo в других операционных системах см. в разделе [install](/ru/installation/).

Для  использования этого руководства необходимо [установить Git](https://git-scm.com/downloads).

Другие подходы к изучению Hugo (например, книги или видеоуроки) см. на странице [внешних учебных ресурсов](/getting-started/external-learning-resources/).
{{% /note %}}

## Шаг 1: Установка Hugo

Установите **расширенную версию Hugo** (требуется для  используемой в этом руководстве темы).

{{% note %}}
`Homebrew` и `MacPorts`, менеджеры пакетов для `macOS`, можно установить с [brew.sh](https://brew.sh/) или [macports.org](https://www.macports.org). /) соответственно. См. [установка Hugo](/ru/installation/), если вы используете Windows или Lunux.
{{% /note %}}

```bash
brew install hugo
# или
port install hugo
```

Чтобы проверить корректность установки:

```bash
hugo version
# Example output: hugo v0.104.2+extended darwin/amd64 BuildDate=unknown
```

Должно быть указано, что это `extended` версия. Если это не так, преустаноите  Hugo или попробуйте другой метод установки.

{{< asciicast ItACREbFgvJ0HjnSNeTknxWy9 >}}

## Шаг 2: Создание нового сайта

```bash
hugo new site quickstart
```

Будет создан новый сайт Hugo в директории `quickstart`.

{{< asciicast 3mf1JGaN0AX0Z7j5kLGl3hSh8 >}}

## Шаг 3: Добавление темы

С  доступными к установке на Hugo темами можно ознакомиться на сайте [themes.gohugo.io](https://themes.gohugo.io/). В этом кратком руководстве используется красивая [тема Ananke](https://themes.gohugo.io/gohugo-theme-ananke/).

Сначала загрузите тему с GitHub и добавьте ее в каталог `themes` вашего сайта:

```bash
cd quickstart
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```

Затем добавьте тему в конфигурацию сайта:

```bash
echo theme = \"ananke\" >> config.toml
```

{{< asciicast 7naKerRYUGVPj8kiDmdh5k5h9 >}}

## Шаг 4: Добавление контента

Вы можете вручную создавать файлы с контентом (например, как `content/<CATEGORY>/<FILE>.<FORMAT>`) и создать  в них метаданные, однако вы можете использовать команду `new`, чтобы hugo сделал несколько вещей за вас (например, добавил название страницы (title) и дату):

```txt
hugo new posts/my-first-post.md
```

{{< asciicast eUojYCfRTZvkEiqc52fUsJRBR >}}

Далее можно приступать к редактированию только что созданного файла. Автоматически созданные Hugo параметры в заголовке Front Matter  будут выглядеть примерно так:

```md
---
title: "My First Post"
date: 2019-03-26T08:47:11+01:00
draft: true
---

```

{{% note %}}
Черновики не будут опубликованы, пока в заголовке Front Matter будет параметр `draft: true`.
Для того чтобы страница была опубликавана при сборке необходимо изменить параметр на `draft: false`
Дополнительная информация [здесь](/ru/getting-started/usage/#draft-future-and-expired-content).
{{% /note %}}

## Шаг 5: Запуск сервера Hugo

Теперь запустите сервер Hugo с включенным параметром [`draft`](/ru/getting-started/usage/#draft-future-and-expired-content):

{{< asciicast BvJBsF6egk9c163bMsObhuNXj >}}

```txt
▶ hugo server -D

                   | EN
+------------------+----+
  Pages            | 10
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  3
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Total in 11 ms
Watching for changes in /Users/bep/quickstart/{content,data,layouts,static,themes}
Watching for config changes in /Users/bep/quickstart/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

**Перейдите на свой новый сайт по адресу[http://localhost:1313/](http://localhost:1313/).**

Теперь можно редакитировать или добавлять новый контент, и вы сразу же видеть изменения в браузере во время работы сервера Hugo. (Возможно, вам придется принудительно обновить веб-браузер, обычно работает что-то вроде Ctrl-R.)

## Шаг 6: Настройка темы

Ваш новый сайт уже выглядит не плохо, но вам нужно его немного отредактировать, прежде чем опубликовать.

### Конфигурация сайта

Откройте `config.toml` в текстовом редакторе:

```toml
baseURL = "https://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "ananke"
```

Замените название сайта в параметре 'title' на что-то более индивидуальное. Кроме того, если у вас уже есть свой домен, установите `baseURL`. Обратите внимание, что это значение не требуется при запуске локального сервера разработки.

{{% note %}}
**Совет.**  Bам может потребоваться [очистить кеш браузера]( https://kb.iu.edu/d/ahic) перед изменениями конфигурации сайта или любого другого файл на своем сайте во время работы сервера Hugo, для корректного отображения вносимых изменений в реальном времени.
{{% /note %}}

Параметры конфигурации для конкретной темы см. на [сайте темы](https://github.com/theNewDynamic/gohugo-theme-ananke).

**Для дальнейшей настройки темы см. раздел документации [Настройка темы](/ru/themes/customizing/).**

### Шаг 7: Сборка статического сайта

Сборка запускается простой командой (ключ -D позволяет включить страницы контента, помеченные как черновик `draft: true`):

```txt
hugo -D
```

По умолчанию сайт будет собран в директории `./public/` (флаг `-d`/`--destination`, может изменить директорию). Также изменить директорию можно установив параметр `publishdir` в основном файле конфигурации).
