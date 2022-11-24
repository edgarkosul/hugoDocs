---
title: Многоязычный режим
linkTitle: Многоязычность
description: Hugo поддерживает создание веб-сайтов одновременно на нескольких языках.
categories: [content management]
keywords: [multilingual,i18n, internationalization]
menu:
  docs:
    parent: content-management
    weight: 230
toc: true
weight: 230
aliases: [/content/multilingual/,/tutorials/create-a-multilingual-site/]
---

Доступные на сайте языки необходимо указать в разделе `languages` основной конфигурации сайта.

> Так же ознакомьтесь со статьёй [Hugo Multilingual Part 1: Content translation]

## Настройка языков

Ниже приведен пример конфигурации сайта для многоязычного сайта  Hugo:

{{< code-toggle file="config" >}}
defaultContentLanguage = "en"
copyright = "Everything is mine"

[params]
[params.navigation]
help  = "Help"

[languages]
[languages.en]
title = "My blog"
weight = 1
[languages.en.params]
linkedin = "https://linkedin.com/whoever"

[languages.fr]
title = "Mon blogue"
weight = 2
[languages.fr.params]
linkedin = "https://linkedin.com/fr/whoever"
[languages.fr.params.navigation]
help  = "Aide"

[languages.ar]
title = "مدونتي"
weight = 2
languagedirection = "rtl"

[languages.pt-pt]
title = "O meu blog"
weight = 3
{{< /code-toggle >}}

Значения параметров которые не определены в разделе `languages` сбрасываются до глобального значения этого параметра (в приведенном примере все языки будут использовать значение  `copyright` : Everything is mine). Это также работает и для `params`, в приведенном примере, для парметра `help` для французкого языка будет использоваться значение `Aide` и значение  `Help`  для всех остальных языков у которых этот параметр не указан.

С указанной в примере конфигурацией весь контент, карта сайта, лента RSS, пагинации и страницы таксономий будут отображаться ниже `/` для языка по умолчанию, в данном случае это английский, и ниже директории `/fr` для французкого языка.

При использовании `Params` в заголовках Front Matter [шаблона одиночной страницы], не указывайте ключ `params` в основной конфигурации сайта в разделе конфигурации для перевода.

`defaultContentLanguage` устанавливает язык по умолчанию для сайта. Если параметр не указан языком по умолчанию будет `en`.

Если необходимо чтобы весь контент сайта для языка по умолчанию отображался ниже директории (`/en`) в данном случае для английского языка по умолчанию, так же как и у других языков сайта, используйте параметр `defaultContentLanguageInSubdir: true`.

Для каждого языка можно переопределить только очевидные не глобальные параметры. Примеры глобальных параметров, например `buildDrafts`. Глобальный параметр `baseURL` является исключением, см. [насройка отдельного хоста для каждого из переводов сайта]

**Обратите внимание:** Используйте коды языков в нижнем регистре, даже при использовании региональных языков (например используйте ru-ru вместо ru-RU). При использовании в параметре `defaultContentLanguage` кода не в нижнем регистре могут возникать конфликты. Пожалуйста, отслеживайте решение этой проблемы тут [Hugo repository issue tracker](https://github.com/gohugoio/hugo/issues/7344)

### Отключить язык

Вы можете отключить один или несколько языков. Это может быть полезно при работе над новым переводом.

{{< code-toggle file="config" >}}
disableLanguages = ["fr", "ja"]
{{< /code-toggle >}}

Обратите внимание, что вы не можете отключить язык по умолчанию.

Эту настройку также можно активировать через переменную окружения операционной системы - [OS environment]:

```bash
HUGO_DISABLELANGUAGES="fr ja" hugo
```

Если у вас уже есть список отключенных языков в `config.toml`, вы можете включить их в режиме разработки через переменную окружения, следующим образом:

```bash
HUGO_DISABLELANGUAGES=" " hugo server
```

### Насройка отдельного хоста для каждого из переводов сайта

Начиная с версии **Hugo 0.31** в конфигурации поддерживается настройка мультихоста. См. [решение проблемы на DitHub](https://github.com/gohugoio/hugo/issues/4027) для подробностей.

Это означает что теперь есть возможность настройки `baseURL` для каждого языка (раздела конфигурации `language`):

> Если `baseURL` установлен на уровне `language`, тогда все языки должны иметь эту настройку и каждый `baseURL` должен быть уникальным.

Пример:

{{< code-toggle file="config" >}}
[languages]
[languages.fr]
baseURL = "https://example.fr"
languageName = "Français"
weight = 1
title = "En Français"

[languages.en]
baseURL = "https://example.com"
languageName = "English"
weight = 2
title = "In English"
{{</ code-toggle >}}

С такой конфигурацией два сайта на разных языках будут созданы в директории `public` каждый в своей директории:

```text
public
├── en
└── fr
```

**Все URL-адреса ( `.Permalink` и т. п.) будут созданы из этого корня. Таким образом, указанная выше домашняя страница на английском языке будет иметь для `.Permalink` значение `https://example.com/`.**

Когда вы запускаете `hugo server`, Hugo запускает несколько HTTP-серверов. Вы увидите что-то вроде этого в консоли:

```text
Web Server is available at 127.0.0.1:1313 (bind address 127.0.0.1)
Web Server is available at 127.0.0.1:1314 (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Перезагрузка на лету и настройка `--navigateToChanged` между серверами будет работать как обычно.

## Перевод контента

Есть два способа управлять переводами контента. Оба гарантируют, что каждой странице назначается язык и она связана с переводами этой страницы на другие языки.

### Переводы в отдельных файлах

Рассмотрим следующий пример:

1. `/content/about.en.md`
2. `/content/about.fr.md`

Первому файлу назначается английский язык, и он связан со вторым.
Второму файлу назначается французский язык, и он связан с первым.

Их язык __назначается__ в соответствии с кодом языка, добавленным в качестве __суффикса к имени файла__.

Файлы контента имеющие одинаковые **директории и базовые имена** связываются вместе как преводы друг друга.

{{< note >}}
Если файл не имеет кода языка (суффикса), ему будет назначен язык по умолчанию.
{{</ note >}}

### Переводы в отдельных директориях

Этот подход использует разные каталоги контента для каждого из языков. Каталог содержимого каждого языка задается с помощью параметра `contentDir`.

{{< code-toggle file="config" >}}
languages:
  en:
    weight: 10
    languageName: "English"
    contentDir: "content/english"
  fr:
    weight: 20
    languageName: "Français"
    contentDir: "content/french"
{{< /code-toggle >}}

Значение `contentDir` может быть любым допустимым путем, даже абсолютным путем. Единственное ограничение состоит в том, что директории с переведенным контентом не могут перекрываться.

Рассмотрим следующий пример в сочетании с приведенной выше конфигурацией:

1. `/content/english/about.md`
2. `/content/french/about.md`

Первому файлу назначается английский язык, и он связан со вторым.
Второму файлу назначается французский язык, и он связан с первым.

Их язык __назначен__ в соответствии с директорией контента, в которой они __размещены__.

Имея один и тот же **путь и базовое имя** (относительно их языкового каталога контента), части контента __связаны__ вместе как переведенные страницы.

### Преназначение связывания переведенных страниц

Любые страницы с одним и тем же значением `translationKey` в заголовках Front Matter будут связаны как переведенные страницы независимо от базового имени или местоположения.

Рассмотрим следующий пример:

1. `/content/about-us.en.md`
2. `/content/om.nn.md`
3. `/content/presentation/a-propos.fr.md`

{{< code-toggle >}}
translationKey: "about"
{{< /code-toggle >}}

Установив в заголовках Front Matter `translationKey` в значение `about` на всех трех страницах, они будут __связаны__ как переведенные страницы.

### Локализация постоянных ссылок *(permalinks)*

Поскольку для формирования ссылок используются пути и имена файлов, все переведенные страницы будут иметь один и тот же URL-адрес (кроме языкового подкаталога).

Чтобы локализовать URL адреса передодов, [`slug`]({{< ref "/content-management/organization/index.md#slug" >}}) или [`url`]({{< ref "/content-management/organization/index.md#url" >}}) в заголовках Front Matter могут быть назначены любыми отличными от значения по умолчанию.

Например, Французкий перевод (`content/about.fr.md`) может иметь свой локализированный `slug`.

{{< code-toggle >}}
Title: A Propos
slug: "a-propos"
{{< /code-toggle >}}

В процессе сборки, Hugo разместит переводы в директориях `/about/` и `/fr/a-propos/` соответственно и сохранит их связь как переведенных страниц.

{{% note %}}
Если используете `url`, не забудьте включить в путь языковую поддиректорию: `/fr/compagnie/a-propos/`.
{{%/ note %}}

### Группы страниц - Page Bundles

Чтобы избежать дублирования файлов, каждая группа страниц наследует ресурсы связанных с ней группы переведенных страниц, за исключением файлов контента (файлы Markdown, файлы HTML и т. д.).

Таким образом, в пределах шаблона страница будет иметь доступ к файлам из всех групп связанных страниц.

Если в связанных группах два или более файла имеют одно и то же базовое имя, только один будет использован и выбран следующим образом:

* Файл из текущего языкового пакета, если он есть.
* Первый файл, найденный среди связанных групп согласно параметру `Weight` указаному в основной конфигурации.

{{% note %}}
Файлы в группах страниц следуют той же логике привязки к языку, что и файлы с контентом. По имени файла  (`image.jpg`, `image.fr.jpg`) и по директории (`english/about/header.jpg`, `french/about/header.jpg`).
{{%/ note %}}

## Ссылка на переведенный контент

Чтобы создать список ссылок на переведенный контент, используйте в шаблоне код, подобный следующему:

{{< code file="layouts/partials/i18nlist.html" >}}
{{ if .IsTranslated }}
<h4>{{ i18n "translations" }}</h4>
<ul>
  {{ range .Translations }}
  <li>
    <a href="{{ .Permalink }}">{{ .Lang }}: {{ .Title }}{{ if .IsPage }} ({{ i18n "wordCount" . }}){{ end }}</a>
  </li>
  {{ end }}
</ul>
{{ end }}
{{< /code >}}

Это код можно поместить в  `partial` (т. е. в директорию `layouts/partials/`) и включить в любой шаблон, или в шаблон [single content page][contenttemplate] или в [homepage]. Он ничего не выведет, если для данной страницы нет переводов.

В приведенном выше примере также используется функция [`i18n`][i18func] описанная в следующем разделе.

### Список всех доступных языков

`.AllTranslations` на странице можно использовать для отображения всех переводов. На главной странице его можно использовать для построения языкового навигатора:

{{< code file="layouts/partials/allLanguages.html" >}}
<ul>
{{ range $.Site.Home.AllTranslations }}
<li><a href="{{ .Permalink }}">{{ .Language.LanguageName }}</a></li>
{{ end }}
</ul>
{{< /code >}}

## Перевод строк

Hugo использует библиотеку [go-i18n] для поддержки перевода строк. [См. исходный репозиторий проекта][go-i18n-source] чтобы найти инструменты, которые помогут управлять рабочими процессами перевода.

Переводы собираются из директории `themes/<THEME>/i18n/` (встроенной в тему), а также из директории `i18n/`в корне вашего проекта. Переводы будут объединены и  преводы из корневой директории будут иметь приоритет над тем, что находится в папке темы. Языковые файлы должны быть названы в соответствии с [RFC 5646] такими именами, как `en-US.toml`, `fr.toml` и т. д.

Также поддерживаются артефициальные языки с подтегами частного использования, как определено в [RFC 5646 &#167; 2.2.7](https://datatracker.ietf.org/doc/html/rfc5646#section-2.2.7). Вы можете опустить префикс art-x- для краткости. Например:

```text
art-x-hugolang
hugolang
```

Подтеги частного использования не должны превышать 8 буквенно-цифровых символов.

### Запрос перевода

Внутри ваших шаблонов используйте функцию `i18n` следующим образом:

```go-html-template
{{ i18n "home" }}
```

Функция будет искать идентификатор `"home"`:

{{< code-toggle file="i18n/en-US" >}}
[home]
other = "Home"
{{< /code-toggle >}}

Результат будет

```text
Home
```

### Запрос гибкого перевода с переменными

Часто вы захотите использовать переменные страницы в строках перевода. Для этого передайте контекст `.` при вызове `i18n`:

```go-html-template
{{ i18n "wordCount" . }}
```

Функция передаст контекст `.` идентификатору `"wordCount":

{{< code-toggle file="i18n/en-US" >}}
[wordCount]
other = "This article has {{ .WordCount }} words."
{{< /code-toggle >}}

Предположим, что `.WordCount` в контексте имеет значение 101. Результат будет таким:

```text
This article has 101 words.
```

### Запросить перевод в единственном/множественном числе

Запросить варианты перевода можно предав функции `i18n` объект словаря (map) со свойством `.Count`. В следующем примере используется переменная  `.ReadingTime` со свойством `.Count`, в которую попадает вычисляемое Hugo время чтения страницы.

```go-html-template
{{ i18n "readingTime" .ReadingTime }}
```

Функция считывает `.Count` из `.ReadingTime` и оценивает, является ли число единственным (one) или множественным (other). После этого онa обратится  к `readTime` id в файле `i18n/en-US.toml`:

{{< code-toggle file="i18n/en-US" >}}
[readingTime]
one = "One minute to read"
other = "{{.Count}} minutes to read"
{{< /code-toggle >}}

Предполагая, что `.ReadingTime.Count` в контексте имеет значение 525600. Результат будет таким:

```text
525600 minutes to read
```

Если `.ReadingTime.Count` в контексте имеет значение 1. Результат:

```text
One minute to read
```

В случае если нужно передать функции пользовательские данные минимальное требование это предача объекта словаря (map) со свойством `.Count`: (`(dict "Count" numeric_value_only)`:

```go-html-template
{{ i18n "readingTime" (dict "Count" 25 "FirstArgument" true "SecondArgument" false "Etc" "so on, so far") }}
```

## Локализация

В следующих примерах локализации предполагается, что основным языком вашего сайта является английский с переводами на французский и немецкий языки.

{{< code-toggle file="config" >}}
defaultContentLanguage = 'en'

[languages]
[languages.en]
contentDir = 'content/en'
languageName = 'English'
weight = 1
[languages.fr]
contentDir = 'content/fr'
languageName = 'Français'
weight = 2
[languages.de]
contentDir = 'content/de'
languageName = 'Deutsch'
weight = 3

{{< /code-toggle >}}

### Даты

С этим значением в заголовках Front Matter:

{{< code-toggle >}}
date = 2021-11-03T12:34:56+01:00
{{< /code-toggle >}}

И этим кодом в шаблоне:

```go-html-template
{{ .Date | time.Format ":date_full" }}
```

На странице выведется:

Language|Value
:--|:--
English|Wednesday, November 3, 2021
Français|mercredi 3 novembre 2021
Deutsch|Mittwoch, 3. November 2021

Подробнее см. [time.Format].

### Валюты

С этим кодом шаблона:

```go-html-template
{{ 512.5032 | lang.FormatCurrency 2 "USD" }}
```

На странице выведется:

Language|Value
:--|:--
English|$512.50
Français|512,50 $US
Deutsch|512,50 $

Подробности см. в [lang.FormatCurrency] и [lang.FormatAccounting].

### Числа

С этим кодом шаблона:

```go-html-template
{{ 512.5032 | lang.FormatNumber 2 }}
```

На странице выведется:

Language|Value
:--|:--
English|512.50
Français|512,50
Deutsch|512,50

Подробности см. в [lang.FormatNumber] и [lang.FormatNumberCustom].

### Проценты

С этим кодом шаблона:

```go-html-template
{{ 512.5032 | lang.FormatPercent 2 }} ---> 512.50%
```

На странице выведется:

Language|Value
:--|:--
English|512.50%
Français|512,50 %
Deutsch|512,50 %

Подробнее см. [lang.FormatPercent].

## Меню

Вы можете определить свои меню для каждого языка независимо. Создание многоязычных меню работает так же, как [создание обычных меню][menus], за исключением того, что они определены в блоках для конкретных языков в файле конфигурации:

{{< code-toggle file="config" >}}
defaultContentLanguage = "en"

[languages.en]
weight = 0
languageName = "English"

[[languages.en.menu.main]]
url    = "/"
name   = "Home"
weight = 0

[languages.de]
weight = 10
languageName = "Deutsch"

[[languages.de.menu.main]]
url    = "/"
name   = "Startseite"
weight = 0
{{< /code-toggle >}}

Рендеринг основной навигации работает как обычно. `.Site.Menus` будет просто содержать меню на текущем языке. Обратите внимание, что `absLangURL` ниже будет ссылаться на правильную локаль вашего веб-сайта. Без него пункты меню на всех языках будут ссылаться на английскую версию, поскольку это язык содержимого по умолчанию, который находится в корневом каталоге.

```go-html-template
<ul>
    {{- $currentPage := . -}}
    {{ range .Site.Menus.main -}}
    <li class="{{ if $currentPage.IsMenuCurrent "main" . }}active{{ end }}">
        <a href="{{ .URL | absLangURL }}">{{ .Name }}</a>
    </li>
    {{- end }}
</ul>
```

### Динамическая локализация меню с i18n

Хотя настройка меню для каждого языка полезна, ваш конфигурационный файл может стать сложным в обслуживании, если у вас много языков.

Если ваши меню одинаковы на всех языках (т. е. если единственное, что меняется, это переведенное имя), вы можете использовать `.Identifier` в качестве ключа перевода для имени меню:

{{< code-toggle file="config" >}}
[[menu.main]]
name = "About me"
url = "about"
weight = 1
identifier = "about"
{{< /code-toggle >}}

Теперь вам нужно указать переводы для пунктов меню в файлах i18n:

{{< code file="i18n/pt.toml" >}}
[about]
other="Sobre mim"
{{< /code >}}

И внесите соответствующие изменения в код меню, чтобы использовать тег `i18n` с `.Identifier` в качестве ключа. Вы также заметите, что здесь мы используем значение по умолчанию для возврата к `.Name`, если ключ `.Identifier` также отсутствует на языке, указанном в конфигурации `defaultContentLanguage`.

{{< code file="layouts/partials/menu.html" >}}
<ul>
    {{- $currentPage := . -}}
    {{ range .Site.Menus.main -}}
    <li class="{{ if $currentPage.IsMenuCurrent "main" . }}active{{ end }}">
        <a href="{{ .URL | absLangURL }}">{{ i18n .Identifier | default .Name}}</a>
    </li>
    {{- end }}
</ul>
{{< /code >}}

## Отсутствующие переводы

Если у строки нет перевода на текущий язык, Hugo будет использовать значение из языка по умолчанию. Если значение по умолчанию не установлено, будет показана пустая строка.

При переводе веб-сайта Hugo может быть удобно иметь визуальный индикатор отсутствующих переводов. [Параметр конфигурации `enableMissingTranslationPlaceholders`][config] пометит все непереведенные строки плейсхолдером `[i18n] identifier`, где `identifier` это идентификатор отсутствующего перевода.

{{% note %}}
Hugo создаст ваш веб-сайт с этими отсутствующими заполнителями перевода. Это скорее всего не подойдет для режима продакшн.
{{% /note %}}

Для слияния контента с другими языками (т. е. отсутствующих переводов контента) см. [lang.Merge].

Чтобы отследить отсутствующие строки перевода, запустите Hugo с флагом `--printI18nWarnings`:

```bash
hugo --printI18nWarnings | grep i18n
i18n|MISSING_TRANSLATION|en|wordCount
```

## Поддержка многоязычных тем

Для поддержки многоязычного режима в ваших темах необходимо учитывать некоторые особенности URL-адресов в шаблонах. Если используется более одного языка, URL-адреса должны соответствовать следующим критериям:

* Соответствовать встроенным `.Permalink` или `.RelPermalink`
* Быть построенным с [`relLangURL` template function][rellangurl] или [`absLangURL` template function][abslangurl] **ИЛИ** иметь префикс`{{ .LanguagePrefix }}`

Если определено более одного языка, переменная `LanguagePrefix` будет равна `/en` (или тому, что является `CurrentLanguage`). Если языки не определены, это будет пустая строка (поэтому она безвредна для одноязычных веб-сайтов Hugo).


## Создание многоязычного контента с помощью `hugo new`

Если вы размещаете контент с переводами в одном каталоге:

```text
hugo new post/test.en.md
hugo new post/test.de.md
```

Если вы упорядочиваете контент с переводами по разным каталогам:

```text
hugo new content/en/post/test.md
hugo new content/de/post/test.md
```

[abslangurl]: /ru/functions/abslangurl
[config]: /ru/getting-started/configuration/
[contenttemplate]: /ru/templates/single-page-templates/
[go-i18n-source]: https://github.com/nicksnyder/go-i18n
[go-i18n]: https://github.com/nicksnyder/go-i18n
[homepage]: /ru/templates/homepage/
[Hugo Multilingual Part 1: Content translation]: https://regisphilibert.com/blog/2018/08/hugo-multilingual-part-1-managing-content-translation/
[i18func]: /ru/functions/i18n/
[lang.FormatAccounting]: /ru/functions/lang/#langformataccounting
[lang.FormatCurrency]: /ru/functions/lang/#langformatcurrency
[lang.FormatNumber]: /ru/functions/lang/#langformatnumber
[lang.FormatNumberCustom]: /ru/functions/lang/#langformatnumbercustom
[lang.FormatPercent]: /ru/functions/lang/#langformatpercent
[lang.Merge]: /ru/functions/lang.merge/
[menus]: /ru/content-management/menus/
[OS environment]: /ru/getting-started/configuration/#configure-with-environment-variables
[rellangurl]: /ru/functions/rellangurl
[RFC 5646]: https://tools.ietf.org/html/rfc5646
[шаблона одиночной страницы]: /ru/templates/single-page-templates/
[time.Format]: /ru/functions/dateformat
[Насройка отдельного хоста для каждого из переводов сайта]: #насройка-отдельного-хоста-для-каждого-из-переводов-сайта
