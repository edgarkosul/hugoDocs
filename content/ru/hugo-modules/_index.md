---
title: Модули Hugo
linktitle: Обзор модулей Hugo
description: Как использовать модули Hugo.
date: 2017-02-01
publishdate: 2017-02-01
menu:
  docs:
    parent: "modules"
    weight: 01
weight: 01
sections_weight: 01
categories: [hugo modules]
keywords: [themes,modules]
draft: false
aliases: [/themes/overview/,/themes/]
toc: true
---

**Модули Hugo** — это основные строительные блоки в Hugo. _Модуль_ может быть вашим основным проектом или меньшим модулем, предоставляющим один или несколько из 7 типов компонентов, определенных в Hugo: **static**, **content**, **layouts**, **data**, **assets**, **i18n** и **archetypes**.

Вы можете комбинировать модули в любой комбинации и даже монтировать каталоги из проектов, отличных от Hugo, образуя большую виртуальную объединенную файловую систему.

Модули Hugo наследуют свой функционал от модулей Go. Для получения дополнительной информации о модулях Go см.:

- [https://github.com/golang/go/wiki/Modules](https://github.com/golang/go/wiki/Modules)
- [https://go.dev/blog/using-go-modules](https://go.dev/blog/using-go-modules)

Существует всего несколько примеров проектов, для демонстрации этого относительно нового функционала Hugo:

- [https://github.com/bep/docuapi](https://github.com/bep/docuapi) — это шаблон, который был реализован по новой с использованием Hugo Modules во время тестирования этой функции. Это хороший пример показывающий как не относящийся к Hugo проект, был смонтирован в структуру папок Hugo. Он даже показывает реализацию JS Bundler в обычных шаблонах Go.
- [https://github.com/bep/my-modular-site](https://github.com/bep/my-modular-site) это очень простой сайт, используемый для тестирования.
