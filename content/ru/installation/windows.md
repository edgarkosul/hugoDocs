---
title: Windows
linkTitle: Windows
description: Установка Hugo на Windows.
categories: [установка hugo]
menu:
  docs:
    parent: installation
    weight: 40
toc: true
weight: 40
---
{{% readfile file="/installation/common/01-editions.md" %}}

{{% readfile file="/installation/common/02-prerequisites.md" %}}

{{% readfile file="/installation/common/03-prebuilt-binaries.md" %}}

## Менеджеры пакетов

### Chocolatey

[Chocolatey] — это бесплатный менеджер пакетов с открытым исходным кодом для Windows. Эта команда установит расширенную версию Hugo:

```sh
choco install hugo-extended
```

[Chocolatey]: https://chocolatey.org/

### Scoop

[Scoop] — это бесплатный менеджер пакетов с открытым исходным кодом для Windows. Эта команда установит расширенную версию Hugo:

```sh
scoop install hugo-extended
```

[Scoop]: https://scoop.sh/

{{% readfile file="/installation/common/04-docker.md" %}}

{{% readfile file="/installation/common/05-build-from-source.md" %}}

{{% note %}}
При сборке расширенной версии Hugo из исходного кода в Windows вам также потребуется установить [GCC compiler]. См. эти [подробные инструкции].

[подробные инструкции]: https://discourse.gohugo.io/t/41370
[GCC compiler]: https://gcc.gnu.org/
{{% /note %}}

## Сравнение

||Установочные файлы|Менеджеры пакетов|Docker|Сборка из исходников
:--|:--:|:--:|:--:|:--:|:--:
Простота установки|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|
Простота обновления|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:
Простота понижения версии|:heavy_check_mark:|:heavy_check_mark: [^2]|:heavy_check_mark:|:heavy_check_mark:
Автоматические обновления|:x:|:x: [^1]|:x: [^1]|:x:
Доступность последней версии|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:

[^1]: Возможно, но требует дополнительной настройки.
[^2]: Легко, если установлена ​​предыдущая версия.
