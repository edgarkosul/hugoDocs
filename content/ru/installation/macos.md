---
title: macOS
linkTitle: macOS
description: Установка Hugo на macOS.
categories: [установка hugo]
menu:
  docs:
    parent: installation
    weight: 20
toc: true
weight: 20
---
{{% readfile file="/installation/common/01-editions.md" %}}

{{% readfile file="/installation/common/02-prerequisites.md" %}}

{{% readfile file="/installation/common/03-prebuilt-binaries.md" %}}

## Менеджеры пакетов

{{% readfile file="/installation/common/homebrew.md" %}}

### MacPorts

[MacPorts] — это бесплатный менеджер пакетов с открытым исходным кодом для macOS. Эта команда установит расширенную версию Hugo:

```sh
sudo port install hugo
```

[MacPorts]: https://www.macports.org/

{{% readfile file="/installation/common/04-docker.md" %}}

{{% readfile file="/installation/common/05-build-from-source.md" %}}

## Сравнение

||Установочные файлы|Менеджеры пакетов|Docker|Сборка из исходников
:--|:--:|:--:|:--:|:--:|:--:
Легко установить?|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|
Легко обновить?|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:
Легко понизить версию?|:heavy_check_mark:|:heavy_check_mark: [^1]|:heavy_check_mark:|:heavy_check_mark:
Автоматические обновления?|:x:|:x: [^2]|:x: [^2]|:x:
Доступна последняя версия?|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:

[^1]: Легко, если предыдущая версия все еще установлена.
[^2]: Возможно, но требует дополнительной настройки.
