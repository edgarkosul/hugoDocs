---
title: Linux
linkTitle: Linux
description: Установка Hugo на Linux.
categories: [установка hugo]
menu:
  docs:
    parent: installation
    weight: 30
toc: true
weight: 30
---
{{% readfile file="/installation/common/01-editions.md" %}}

{{% readfile file="/installation/common/02-prerequisites.md" %}}

{{% readfile file="/installation/common/03-prebuilt-binaries.md" %}}

## Package managers

### Snap

[Snap] — это бесплатный менеджер пакетов с открытым исходным кодом для Linux. Пакеты Snap, доступные для [большинства дистрибутивов], просты в установке и автоматически обновляются. Это установит расширенную версию Hugo:

```sh
sudo snap install hugo
```

[большинства дистрибутивов]: https://snapcraft.io/docs/installing-snapd
[Snap]: https://snapcraft.io/

{{% readfile file="/installation/common/homebrew.md" %}}

## Пакеты репозитория

В большинстве дистрибутивов Linux имеется репозиторий часто устанавливаемых приложений. Обратите внимание, что эти репозитории могут не всегда могут содержать [последнюю версию Hugo].

[последнюю версию Hugo]: https://github.com/gohugoio/hugo/releases/latest

### Arch Linux

Дистрибутивы Linux основанные на [Arch Linux] включая [EndeavourOS], [Garuda Linux], [Manjaro] и другие. Эта команда установит расширенную версию Hugo:

```sh
sudo pacman -S hugo
```

[Arch Linux]: https://archlinux.org/
[EndeavourOS]: https://endeavouros.com/
[Manjaro]: https://manjaro.org/
[Garuda Linux]: https://garudalinux.org/

### Debian

Производные [Debian] дистрибутива Linux включая [elementary OS], [KDE neon], [Linux Lite], [Linux Mint], [MX Linux], [Pop!_OS], [Ubuntu], [Zorin OS], и другие. Эта команда установит расширенную версию Hugo:

```sh
sudo apt install hugo
```

Вы также можете загрузить пакеты Debian со страницы [с последними релизами Hugo].

[с последними релизами Hugo]: https://github.com/gohugoio/hugo/releases/latest

[Debian]: https://www.debian.org/
[elementary OS]: https://elementary.io/
[KDE neon]: https://neon.kde.org/
[Linux Lite]: https://www.linuxliteos.com/
[Linux Mint]: https://linuxmint.com/
[MX Linux]: https://mxlinux.org/
[Pop!_OS]: https://pop.system76.com/
[Ubuntu]: https://ubuntu.com/
[Zorin OS]: https://zorin.com/os/

### Fedora

Производные от [Red Hat Enterprise Linux] включаz [CentOS], [Fedora] и другие. Эта команда установит расширенную версию Hugo:


```sh
sudo dnf install hugo
```

[CentOS]: https://www.centos.org/
[Fedora]: https://getfedora.org/
[Red Hat Enterprise Linux]: https://www.redhat.com/

### openSUSE

Производные от [openSUSE] Linux включая [GeckoLinux], [Linux Karmada] и другие. Эта команда установит расширенную версию Hugo:


```sh
sudo zypper install hugo
```

[GeckoLinux]: https://geckolinux.github.io/
[Linux Karmada]: https://linuxkamarada.com/
[openSUSE]: https://www.opensuse.org/

### Solus

Дистрибутив [Solus] Linux включает Hugo в свой репозиторий пакетов. Это установит _стандартную_ версию Hugo:

```sh
sudo eopkg install hugo
```

[Solus]: https://getsol.us/home/

{{% readfile file="/installation/common/04-docker.md" %}}

{{% readfile file="/installation/common/05-build-from-source.md" %}}

## Comparison

||Установочные файлы|Менеджеры пакетов|Пакеты репозитория|Docker|Сборка из исходников
:--|:--:|:--:|:--:|:--:|:--:
Простота установки|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:
Легкость обновления|:heavy_check_mark:|:heavy_check_mark:|разная|:heavy_check_mark:|:heavy_check_mark:
Легкость понижения версии|:heavy_check_mark:|:heavy_check_mark: [^1]|разная|:heavy_check_mark:|:heavy_check_mark:
Автоматическое обновление|:x:|разная [^2]|:x:|:x: [^3]|:x:
Доступность послендней версии|:heavy_check_mark:|:heavy_check_mark:|разная|:heavy_check_mark:|:heavy_check_mark:

[^1]:Легко, если предыдущая версия все еще установлена.
[^2]: Пакеты Snap автоматически обновляются. Homebrew требует дополнительной настройки.
[^3]: Возможно, но требует дополнительной настройки.
