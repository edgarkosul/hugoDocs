---
title: BSD
linkTitle: BSD
description: Установите Hugo на операционные системы основанные на BSD.
categories: [установка hugo]
menu:
  docs:
    parent: installation
    weight: 50
toc: true
weight: 50
---
{{% readfile file="/installation/common/01-editions.md" %}}

{{% readfile file="/installation/common/02-prerequisites.md" %}}

{{% readfile file="/installation/common/03-prebuilt-binaries.md" %}}

## Пакеты репозитория

Большинство основанных на BSD ОС  поддерживают репозиторий часто устанавливаемых приложений. Обратите внимание, что эти репозитории могут не содержать [последнюю версию Hugo].

[последнюю версию Hugo]: https://github.com/gohugoio/hugo/releases/latest

### DragonFly BSD

[DragonFly BSD] включает Hugo в свой репозиторий пакетов. Эта команда установит расширенную версию Hugo:

```sh
sudo pkg install gohugo
```

[DragonFly BSD]: https://www.dragonflybsd.org/

### FreeBSD

[FreeBSD] включает Hugo в свой репозиторий пакетов. Эта команда установит расширенную версию Hugo:

```sh
sudo pkg install gohugo
```

[FreeBSD]: https://www.freebsd.org/

### NetBSD

[NetBSD] включает Hugo в свой репозиторий пакетов. Эта команда установит расширенную версию Hugo:

```sh
sudo pkgin install go-hugo
```

[NetBSD]: https://www.netbsd.org/

### OpenBSD

[OpenBSD] включает Hugo в свой репозиторий пакетов. Вам будет предложено выбрать версию Hugo для дальнейшей установки:

```sh
doas pkg_add hugo
```

[OpenBSD]: https://www.openbsd.org/

{{% readfile file="/installation/common/04-docker.md" %}}

{{% readfile file="/installation/common/05-build-from-source.md" %}}

## Сравнение

||Установочные файлы|Пакеты репозитория|Docker|Сборка из исходников
:--|:--:|:--:|:--:|:--:
Простотота установки|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|
Легкость обновления|:heavy_check_mark:|разная|:heavy_check_mark:|:heavy_check_mark:
Легкость понижения версии|:heavy_check_mark:|разная|:heavy_check_mark:|:heavy_check_mark:
Автоматическое обновление|:x:|разная|:x: [^1]|:x:
Доступность последней версии|:heavy_check_mark:|разная|:heavy_check_mark:|:heavy_check_mark:

[^1]: Возможно, но требует дополнительной настройки.
