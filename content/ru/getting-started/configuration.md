---
title: Настройка Hugo
linktitle: Конфигурация
description: Как настроить сайт и среду разработки Hugo.
date: 2013-07-01
publishdate: 2017-01-02
categories: [getting started,fundamentals]
keywords: [configuration,toml,yaml,json]
menu:
  docs:
    parent: "getting-started"
    weight: 60
weight: 60
sections_weight: 60
aliases: [/overview/source-directory/,/overview/configuration/]
toc: true
---

## Файл конфигурации

Hugo использует файлы `config.toml`, `config.yaml` или `config.json` (если они находятся в
корне сайта) в качестве файла конфигурации сайта по умолчанию.

Пользователь может переопределить используемый по умолчанию файл конфигурации с помощью параметра командной строки `--config`.

Например:

```txt
hugo --config debugconfig.toml
hugo --config a.toml,b.toml,c.toml
```

{{% note %}}
Несколько файлов конфигурации сайта можно указать в виде строки, разделенной запятыми, после флага командной строки `--config`.
{{% /note %}}

## Каталог конфигурации

В дополнение к использованию одного файла конфигурации сайта, можно использовать каталог `configDir` (по умолчанию `config/`), для более простой организации и настройки, специфичной для среды.

- Каждый файл представляет корневой объект, например  `params.toml` для `[Params]`, `menu(s).toml` для `[Menu]`, `languages.toml` для `[Languages]` и т. п. ...
- Содержимое каждого файла представляющего раздел конфигурации (корневой объект) должно быть, перемещено на корневой уровень, например:

{{< code-toggle file="config" >}}
[Params]
  foo = "bar"
{{< /code-toggle >}}

{{< code-toggle file="params" >}}
foo = "bar"
{{< /code-toggle >}}

- Каждый каталог содержит группу файлов, содержащих настройки, уникальные для среды (default, prodaction, staging).
- Файлы могут быть локализованы, чтобы они соответствовали языку.


```txt
├── config
│   ├── _default
│   │   ├── config.toml
│   │   ├── languages.toml
│   │   ├── menus.en.toml
│   │   ├── menus.zh.toml
│   │   └── params.toml
│   ├── production
│   │   ├── config.toml
│   │   └── params.toml
│   └── staging
│       ├── config.toml
│       └── params.toml
```

Учитывая приведенную выше структуру, при запуске `hugo --environment staging`, Hugo будет использовать все настройки из `config/_default` и объединять `staging` поверх них.

Давайте возьмем пример, чтобы понять это лучше. Допустим, вы используете Google Analytics для своего веб-сайта. Для этого необходимо указать `googleAnalytics = "G-XXXXXXXX"` в `config.toml`.Теперь рассмотрим следующий сценарий:
- Вы не хотите, чтобы код Analytics загружался в процессе разработки, т.е. на вашем `localhost`
– Вы хотите использовать отдельные идентификаторы Google Analytics для рабочей и тестовой сред (скажем):
  - `G-PPPPPPPP` для рабочей среды (prodaction)
  - `G-SSSSSSSS` для тестовой среды (staging)

Вот как вам нужно настроить файлы `config.toml`, учитывая описанный выше сценарий:
1. В `_default/config.toml` вообще не нужно указывать параметр googleAnalytics. Это гарантирует, что код Google Analytics не будет загружен на ваш сервер разработки, например, когда вы запускаете `hugo server`. Это работает, поскольку по умолчанию Hugo устанавливает `Environment=development`, когда вы запускаете `hugo server`, который использует файлы конфигурации из папки `_default`.
2.В `production/config.toml` вам просто нужно иметь одну строку:

    ```googleAnalytics = "G-PPPPPPPP"```

  Вам не нужно снова упоминать все другие параметры, такие как `title`, `baseURL`, `theme` и т. д. в этом файле конфигурации. Вам нужно указать только те параметры, которые отличаются или являются новыми для рабочей среды. Это связано с тем, что Hugo __объединит__ эту настройку поверх `_default/config.toml`. Теперь, когда вы запускаете `hugo` (команда сборки), по умолчанию Hugo устанавливает `Environment=production`, поэтому код аналитики `G-PPPPPPPP` будет присутствовать на вашем рабочем веб-сайте.
3. Точно так же в `staging/config.toml` вам просто нужно иметь одну строку:

    ```googleAnalytics = "G-SSSSSSSS"```

  Теперь вам нужно сообщить Хьюго, что вы используете тестовую среду (staging). Таким образом, ваша команда сборки должна быть `hugo --environment staging`, которая загрузит код аналитики `G-SSSSSSSS` на вашем тестовом веб-сайте.

{{% note %}}
Средами по умолчанию являются __development__ c командой `hugo server` и __production__ с командой `hugo`.
{{%/ note %}}

## Объединение с конфигурацией  из директории темы

Значение конфигурации `_merge` может быть одним из:

none
: Нет слияния.

shallow
: Добавляются значения только новых параметров.

deep
: Добавляются значения новых параметров и объединяются существующие.

Обратите внимание, что вам не нужно указывать все праметры из приведенных значений по умолчанию, значение `_merge` будет унаследовано, если не установлено.
  After scanning selected spans, do NOT read-scan remainder of disk.
If Selective self-test is pending on power-up, resume after 0 minute delay.
Значения по умолчанию:

{{< code-toggle config="mergeStrategy" skipHeader=true />}}

## Все параметры конфигурации

Ниже приведен полный список определенных Hugo переменных с их значениями по умолчанию.
значение в скобках. Пользователи могут переопределить эти значения на своем сайте в файлах конфигурации.

### archetypeDir

**Значение по умолчанию** "archetypes"

Директория, в которой Hugo находит файлы c шаблонами заголовков Front Matter. {{% module-mounts-note-ru %}}

### assetDir

**Значение по умолчанию** "assets"

Каталог, в котором Hugo находит файлы активов (css, jpg, csv и пр.) , используемые в обработчиках [Hugo Pipes](/ru/hugo-pipes/). {{% module-mounts-note-ru %}}

### baseURL

Имя хоста (и путь) к корню, например: https://www.siteko.net/

### build

См. [Конфигурация сборки](#configure-build)

### buildDrafts (false)

**Значение по умолчанию** false

Если параметр установлен в значение `true` в сборку будут включен контент не имеющий в заголовках Front Matter параметра `draft: true`

### buildExpired

**Значение по умолчанию** false

Включить контент с истекшим сроком `expiryDate` в настройках Front Matter.

### buildFuture

**Значение по умолчанию** false

Включить контент с датой публикации в будущем `publishDate` в настройках Front Matter.

### caches

См. [Настройка кеширования файлов](#configure-file-caches)

### cascade

Передает значения конфигурации в заголовках Front Matter на страницы глубже в дереве содержимого. Параметры в конфигурации сайта такие же, как и в заголовках Front Matter, см. [Front Matter Cascade](/ru/content-management/front-matter#front-matter-cascade).

### canonifyURLs

**Значение по умолчанию** false

Enable to turn relative URLs into absolute.

### contentDir

**Значение по умолчанию** "content"

The directory from where Hugo reads content files. {{% module-mounts-note-ru %}}

### copyright

**Значение по умолчанию** ""

Copyright notice for your site, typically displayed in the footer.

### dataDir

**Значение по умолчанию** "data"

The directory from where Hugo reads data files. {{% module-mounts-note-ru %}}

### defaultContentLanguage

**Значение по умолчанию** "en"

Content without language indicator will default to this language.

### defaultContentLanguageInSubdir

**Значение по умолчанию**  false

Render the default content language in subdir, e.g. `content/en/`. The site root `/` will then redirect to `/en/`.

### disableAliases

**Значение по умолчанию**  false

Will disable generation of alias redirects. Note that even if `disableAliases` is set, the aliases themselves are preserved on the page. The motivation with this is to be able to generate 301 redirects in an `.htaccess`, a Netlify `_redirects` file or similar using a custom output format.

### disableHugoGeneratorInject

**Значение по умолчанию**  false

Hugo will, by default, inject a generator meta tag in the HTML head on the _home page only_. You can turn it off, but we would really appreciate if you don't, as this is a good way to watch Hugo's popularity on the rise.

### disableKinds

**Значение по умолчанию**  []

Enable disabling of all pages of the specified *Kinds*. Allowed values in this list: `"page"`, `"home"`, `"section"`, `"taxonomy"`, `"term"`, `"RSS"`, `"sitemap"`, `"robotsTXT"`, `"404"`.

### disableLiveReload

**Значение по умолчанию**  false

Disable automatic live reloading of browser window.

### disablePathToLower

**Значение по умолчанию**  false

: Do not convert the url/path to lowercase.

### enableEmoji

**Значение по умолчанию**  false

Enable Emoji emoticons support for page content; see the [Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet/).

### enableGitInfo

**Значение по умолчанию**  false

Enable `.GitInfo` object for each page (if the Hugo site is versioned by Git). This will then update the `Lastmod` parameter for each page using the last git commit date for that content file.

### enableInlineShortcodes

**Значение по умолчанию**  false

Enable inline shortcode support. See [Inline Shortcodes](/templates/shortcode-templates/#inline-shortcodes).

### enableMissingTranslationPlaceholders

**Значение по умолчанию**  false

Show a placeholder instead of the default value or an empty string if a translation is missing.

### enableRobotsTXT

**Значение по умолчанию**  false

Enable generation of `robots.txt` file.

### frontmatter

See [Front matter Configuration](#configure-front-matter).

### googleAnalytics

**Значение по умолчанию**  ""

Google Analytics tracking ID.

### hasCJKLanguage

**Значение по умолчанию** false

If true, auto-detect Chinese/Japanese/Korean Languages in the content. This will make `.Summary` and `.WordCount` behave correctly for CJK languages.

### imaging

See [Image Processing Config](/content-management/image-processing/#imaging-configuration).

### languageCode

**Значение по умолчанию**  ""

A language tag as defined by [RFC 5646](https://datatracker.ietf.org/doc/html/rfc5646). This value is used to populate:

- The `<language>` element in the internal [RSS template](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/rss.xml)
- The `lang` attribute of the `<html>` element in the internal [alias template](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/alias.html)

### languages

See [Configure Languages](/content-management/multilingual/#configure-languages).

### disableLanguages

See [Disable a Language](/content-management/multilingual/#disable-a-language)

### markup

See [Configure Markup](/getting-started/configuration-markup).

### mediaTypes

See [Configure Media Types](/templates/output-formats/#media-types).

### menus

See [Add Non-content Entries to a Menu](/content-management/menus/#add-non-content-entries-to-a-menu).

### minify

See [Configure Minify](#configure-minify)

### module

Module config see [Module Config](/hugo-modules/configuration/).

### newContentEditor

**Значение по умолчанию** ""

The editor to use when creating new content.

### noChmod

**Значение по умолчанию** false

Don't sync permission mode of files.

### noTimes

**Значение по умолчанию** false

Don't sync modification time of files.

### outputFormats

See [Configure Output Formats](#configure-additional-output-formats).

### paginate

**Значение по умолчанию** 10

Default number of elements per page in [pagination](/templates/pagination/).

### paginatePath

**Значение по умолчанию** "page"

The path element used during pagination (`https://example.com/page/2`).

### permalinks

See [Content Management](/content-management/urls/#permalinks).

### pluralizeListTitles

**Значение по умолчанию** true

Pluralize titles in lists.

### publishDir

**Значение по умолчанию** "public"

The directory to where Hugo will write the final static site (the HTML files etc.).

### related

: See [Related Content](/content-management/related/#configure-related-content).

### relativeURLs

**Значение по умолчанию** false

Enable this to make all relative URLs relative to content root. Note that this does not affect absolute URLs.

### refLinksErrorLevel

**Значение по умолчанию** "ERROR"

When using `ref` or `relref` to resolve page links and a link cannot be resolved, it will be logged with this log level. Valid values are `ERROR` (default) or `WARNING`. Any `ERROR` will fail the build (`exit -1`).

### refLinksNotFoundURL

URL to be used as a placeholder when a page reference cannot be found in `ref` or `relref`. Is used as-is.

### removePathAccents

**Значение по умолчанию** false

Removes [non-spacing marks](https://www.compart.com/en/unicode/category/Mn) from [composite characters](https://en.wikipedia.org/wiki/Precomposed_character) in content paths.

```text
content/post/hügó.md --> https://example.org/post/hugo/
```

### rssLimit

**Значение по умолчанию** -1 (unlimited)

Maximum number of items in the RSS feed.

### sectionPagesMenu

See ["Section Menu for Lazy Bloggers"](/templates/menu-templates/#section-menu-for-lazy-bloggers).

### security

See [Security Policy](/about/security-model/#security-policy)

### sitemap

Default [sitemap configuration](/templates/sitemap-template/#configuration).

### summaryLength

**Значение по умолчанию** 70

The length of text in words to show in a [`.Summary`](/content-management/summaries/#automatic-summary-splitting).

### taxonomies

See [Configure Taxonomies](/content-management/taxonomies#configure-taxonomies).

### theme

: See [Module Config](/hugo-modules/configuration/#module-config-imports) for how to import a theme.

### themesDir

**Значение по умолчанию**  "themes"

The directory where Hugo reads the themes from.

### timeout

**Значение по умолчанию** "30s"

Timeout for generating page contents, specified as a [duration](https://pkg.go.dev/time#Duration) or in milliseconds. *Note:*&nbsp;this is used to bail out of recursive content generation. You might need to raise this limit if your pages are slow to generate (e.g., because they require large image processing or depend on remote contents).

### timeZone

The time zone (or location), e.g. `Europe/Oslo`,  used to parse front matter dates without such information and in the [`time` function](/functions/time/). The list of valid values may be system dependent, but should include `UTC`, `Local`, and any location in the [IANA Time Zone database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

### title

Site title.

### titleCaseStyle

**Значение по умолчанию**  "AP"

See [Configure Title Case](#configure-title-case)

### uglyURLs

**Значение по умолчанию** false

When enabled, creates URL of the form `/filename.html` instead of `/filename/`.

### watch

**Значение по умолчанию** false

Watch filesystem for changes and recreate as needed.

{{% note %}}
If you are developing your site on a \*nix machine, here is a handy shortcut for finding a configuration option from the command line:
```txt
cd ~/sites/yourhugosite
hugo config | grep emoji
```

which shows output like

```txt
enableemoji: true
```
{{% /note %}}

## Configure Build

The `build` configuration section contains global build-related configuration options.

{{< code-toggle file="config">}}
[build]
useResourceCacheWhen="fallback"
writeStats = false
noJSConfigInAssets = false
{{< /code-toggle >}}


useResourceCacheWhen
: When to use the cached resources in `/resources/_gen` for PostCSS and ToCSS. Valid values are `never`, `always` and `fallback`. The last value means that the cache will be tried if PostCSS/extended version is not available.

writeStats
: When enabled, a file named `hugo_stats.json` will be written to your project root with some aggregated data about the build, e.g. list of HTML entities published to be used to do [CSS pruning](/hugo-pipes/postprocess/#css-purging-with-postcss). If you're only using this for the production build, you should consider placing it below [config/production](/getting-started/configuration/#configuration-directory). It's also worth mentioning that, due to the nature of the partial server builds, new HTML entities will be added when you add or change them while the server is running, but the old values will not be removed until you restart the server or run a regular `hugo` build.

**Note** that the prime use case for this is purging of unused CSS; it is built for speed and there may be false positives (e.g., detection of HTML elements that are not HTML elements).

noJSConfigInAssets
: Turn off writing a `jsconfig.json` into your `/assets` folder with mapping of imports from running [js.Build](https://gohugo.io/hugo-pipes/js). This file is intended to help with intellisense/navigation inside code editors such as [VS Code](https://code.visualstudio.com/). Note that if you do not use `js.Build`, no file will be written.

## Configure Server

This is only relevant when running `hugo server`, and it allows to set HTTP headers during development, which allows you to test out your Content Security Policy and similar. The configuration format matches [Netlify's](https://docs.netlify.com/routing/headers/#syntax-for-the-netlify-configuration-file) with slightly more powerful [Glob matching](https://github.com/gobwas/glob):


{{< code-toggle file="config">}}
[server]
[[server.headers]]
for = "/**"

[server.headers.values]
X-Frame-Options = "DENY"
X-XSS-Protection = "1; mode=block"
X-Content-Type-Options = "nosniff"
Referrer-Policy = "strict-origin-when-cross-origin"
Content-Security-Policy = "script-src localhost:1313"
{{< /code-toggle >}}

Since this is "development only", it may make sense to put it below the `development` environment:


{{< code-toggle file="config/development/server">}}
[[headers]]
for = "/**"

[headers.values]
X-Frame-Options = "DENY"
X-XSS-Protection = "1; mode=block"
X-Content-Type-Options = "nosniff"
Referrer-Policy = "strict-origin-when-cross-origin"
Content-Security-Policy = "script-src localhost:1313"
{{< /code-toggle >}}

You can also specify simple redirects rules for the server. The syntax is again similar to Netlify's.

Note that a `status` code of 200 will trigger a [URL rewrite](https://docs.netlify.com/routing/redirects/rewrites-proxies/), which is what you want in SPA situations, e.g:

{{< code-toggle file="config/development/server">}}
[[redirects]]
from = "/myspa/**"
to = "/myspa/"
status = 200
force = false
{{< /code-toggle >}}

Setting `force=true` will make a redirect even if there is existing content in the path. Note that before Hugo 0.76  `force` was the default behavior, but this is inline with how Netlify does it.

## 404 Server Error Page

{{< new-in "0.103.0" >}}

Hugo will, by default, render all 404 errors when running `hugo server` with the `404.html` template. Note that if you have already added one or more redirects to your [Server Config](#configure-server), you need to add the 404 redirect explicitly, e.g:

```toml
[[redirects]]
    from   = "/**"
    to     = "/404.html"
    status = 404
```

## 404 Server Error Page

{{< new-in "0.103.0" >}}

Hugo will, by default, render all 404 errors when running `hugo server` with the `404.html` template. Note that if you have already added one or more redirects to your [Server Config](#server-config), you need to add the 404 redirect explicitly, e.g:

```toml
[[redirects]]
    from   = "/**"
    to     = "/404.html"
    status = 404
```

## Configure Title Case

Set `titleCaseStyle` to specify the title style used by the [title](/functions/title/) template function and the automatic section titles in Hugo. It defaults to [AP Stylebook](https://www.apstylebook.com/) for title casing, but you can also set it to `Chicago` or `Go` (every word starts with a capital letter).

## Configuration Environment Variables

HUGO_NUMWORKERMULTIPLIER
: Can be set to increase or reduce the number of workers used in parallel processing in Hugo. If not set, the number of logical CPUs will be used.

## Configuration Lookup Order

Similar to the template [lookup order][], Hugo has a default set of rules for searching for a configuration file in the root of your website's source directory as a default behavior:

1. `./config.toml`
2. `./config.yaml`
3. `./config.json`

In your `config` file, you can direct Hugo as to how you want your website rendered, control your website's menus, and arbitrarily define site-wide parameters specific to your project.


## Example Configuration

The following is a typical example of a configuration file. The values nested under `params:` will populate the [`.Site.Params`][] variable for use in [templates][]:

{{< code-toggle file="config">}}
baseURL: "https://yoursite.example.com/"
title: "My Hugo Site"
permalinks:
  posts: /:year/:month/:title/
params:
  Subtitle: "Hugo is Absurdly Fast!"
  AuthorName: "Jon Doe"
  GitHubUser: "spf13"
  ListOfFoo:
    - "foo1"
    - "foo2"
  SidebarRecentLimit: 5
{{< /code-toggle >}}

## Configure with Environment Variables

In addition to the 3 config options already mentioned, configuration key-values can be defined through operating system environment variables.

For example, the following command will effectively set a website's title on Unix-like systems:

```txt
$ env HUGO_TITLE="Some Title" hugo
```

This is really useful if you use a service such as Netlify to deploy your site. Look at the Hugo docs [Netlify configuration file](https://github.com/gohugoio/hugoDocs/blob/master/netlify.toml) for an example.

{{% note "Setting Environment Variables" %}}
Names must be prefixed with `HUGO_` and the configuration key must be set in uppercase when setting operating system environment variables.

To set config params, prefix the name with `HUGO_PARAMS_`
{{% /note %}}

If you are using snake_cased variable names, the above will not work. Hugo determines the delimiter to use by the first character after `HUGO`. This allows you to define environment variables on the form `HUGOxPARAMSxAPI_KEY=abcdefgh`, using any [allowed](https://stackoverflow.com/questions/2821043/allowed-characters-in-linux-environment-variable-names#:~:text=So%20names%20may%20contain%20any,not%20begin%20with%20a%20digit.) delimiter.

{{< todo >}}
Test and document setting params via JSON env var.
{{< /todo >}}

## Ignore Content and Data Files when Rendering

To exclude specific files from the `content` and `data` directories when rendering your site, set `ignoreFiles` to one or more regular expressions to match against the absolute file path.

To ignore files ending with `.foo` or `.boo`:

{{< code-toggle copy="false" >}}
ignoreFiles = ['\.foo$', '\.boo$']
{{< /code-toggle >}}

To ignore a file using the absolute file path:

{{< code-toggle copy="false" >}}
ignoreFiles = ['^/home/user/project/content/test\.md$']
{{< /code-toggle >}}

## Configure Front Matter

### Configure Dates

Dates are important in Hugo, and you can configure how Hugo assigns dates to your content pages. You do this by adding a `frontmatter` section to your `config.toml`.

The default configuration is:

{{< code-toggle file="config" >}}
[frontmatter]
date = ["date", "publishDate", "lastmod"]
lastmod = [":git", "lastmod", "date", "publishDate"]
publishDate = ["publishDate", "date"]
expiryDate = ["expiryDate"]
{{< /code-toggle >}}

If you, as an example, have a non-standard date parameter in some of your content, you can override the setting for `date`:

{{< code-toggle file="config" >}}
[frontmatter]
date = ["myDate", ":default"]
{{< /code-toggle >}}

The `:default` is a shortcut to the default settings. The above will set `.Date` to the date value in `myDate` if present, if not we will look in `date`,`publishDate`, `lastmod` and pick the first valid date.

In the list to the right, values starting with ":" are date handlers with a special meaning (see below). The others are just names of date parameters (case insensitive) in your front matter configuration.  Also note that Hugo have some built-in aliases to the above: `lastmod` => `modified`, `publishDate` => `pubdate`, `published` and `expiryDate` => `unpublishdate`. With that, as an example, using `pubDate` as a date in front matter, will, by default, be assigned to `.PublishDate`.

The special date handlers are:


`:fileModTime`
: Fetches the date from the content file's last modification timestamp.

An example:

{{< code-toggle file="config" >}}
[frontmatter]
lastmod = ["lastmod", ":fileModTime", ":default"]
{{< /code-toggle >}}


The above will try first to extract the value for `.Lastmod` starting with the `lastmod` front matter parameter, then the content file's modification timestamp. The last, `:default` should not be needed here, but Hugo will finally look for a valid date in `:git`, `date` and then `publishDate`.


`:filename`
: Fetches the date from the content file's filename. For example, `2018-02-22-mypage.md` will extract the date `2018-02-22`. Also, if `slug` is not set, `mypage` will be used as the value for `.Slug`.

An example:

{{< code-toggle file="config" >}}
[frontmatter]
date  = [":filename", ":default"]
{{< /code-toggle >}}

The above will try first to extract the value for `.Date` from the filename, then it will look in front matter parameters `date`, `publishDate` and lastly `lastmod`.


`:git`
: This is the Git author date for the last revision of this content file. This will only be set if `--enableGitInfo` is set or `enableGitInfo = true` is set in site config.

## Configure Additional Output Formats

Hugo v0.20 introduced the ability to render your content to multiple output formats (e.g., to JSON, AMP html, or CSV). See [Output Formats][] for information on how to add these values to your Hugo project's configuration file.

## Configure Minify

Default configuration:

{{< code-toggle config="minify" />}}

## Configure File Caches

Since Hugo 0.52 you can configure more than just the `cacheDir`. This is the default configuration:

{{< code-toggle >}}
[caches]
[caches.getjson]
dir = ":cacheDir/:project"
maxAge = -1
[caches.getcsv]
dir = ":cacheDir/:project"
maxAge = -1
[caches.getresource]
dir = ":cacheDir/:project"
maxAge = -1
[caches.images]
dir = ":resourceDir/_gen"
maxAge = -1
[caches.assets]
dir = ":resourceDir/_gen"
maxAge = -1
[caches.modules]
dir = ":cacheDir/modules"
maxAge = -1
{{< /code-toggle >}}

You can override any of these cache settings in your own `config.toml`.

### The keywords explained

`:cacheDir`
: This is the value of the `cacheDir` config option if set (can also be set via OS env variable `HUGO_CACHEDIR`). It will fall back to `/opt/build/cache/hugo_cache/` on Netlify, or a `hugo_cache` directory below the OS temp dir for the others. This means that if you run your builds on Netlify, all caches configured with `:cacheDir` will be saved and restored on the next build. For other CI vendors, please read their documentation. For an CircleCI example, see [this configuration](https://github.com/bep/hugo-sass-test/blob/6c3960a8f4b90e8938228688bc49bdcdd6b2d99e/.circleci/config.yml).

`:project`
: The base directory name of the current Hugo project. This means that, in its default setting, every project will have separated file caches, which means that when you do `hugo --gc` you will not touch files related to other Hugo projects running on the same PC.

`:resourceDir`
: This is the value of the `resourceDir` config option.

maxAge
: This is the duration before a cache entry will be evicted, -1 means forever and 0 effectively turns that particular cache off. Uses Go's `time.Duration`, so valid values are `"10s"` (10 seconds), `"10m"` (10 minutes) and `"10h"` (10 hours).

dir
: The absolute path to where the files for this cache will be stored. Allowed starting placeholders are `:cacheDir` and `:resourceDir` (see above).

## Configuration Format Specs

- [TOML Spec][toml]
- [YAML Spec][yaml]
- [JSON Spec][json]

[`.Site.Params`]: /variables/site/
[directory structure]: /getting-started/directory-structure
[json]: https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf "Specification for JSON, JavaScript Object Notation"
[lookup order]: /templates/lookup-order/
[Output Formats]: /templates/output-formats/
[templates]: /templates/
[toml]: https://github.com/toml-lang/toml
[yaml]: https://yaml.org/spec/
[static-files]: /content-management/static-files/
