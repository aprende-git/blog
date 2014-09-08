---
layout: post
title: "Match y simple"
date: 2014-09-08 18:23:22 +0200
comments: true
categories: versiones, configuración, mensajes
---

Es posible que, cuando habéis actualizado el sistema operativo o instalado por primera vez git, al hacer `git push` os haya salido un mensaje como este:

```
warning: push.default is unset; its implicit value is changing in
Git 2.0 from 'matching' to 'simple'. To squelch this message
and maintain the current behavior after the default changes, use:

  git config --global push.default matching

To squelch this message and adopt the new behavior now, use:

  git config --global push.default simple

```

El mensaje está relacionado con las ramas que va a sincronizar al
usarlo. Como explica en [este artículo sobre el nuevo
comportamiento](http://blog.nicoschuele.com/posts/git-2-0-changes-push-default-to-simple),
`matching` es el comportamiento que tenía en la versión 1.x: cuando se
hace push se trata de emparejar (de ahí el *match*) las ramas remotas
con las locales y se sincronizarán emparejando los nombres. Sin
embargo, con `simple` se hará `push` solamente sobre la rama en la que
se esté en ese momento.

Hay [algunas opciones
más](http://stackoverflow.com/questions/21839651/git-what-is-the-difference-between-push-default-matching-and-simple). Por
ejemplo, en flujos de trabajo distribuidos `current` es el equivalente
a `simple`, aunque el primero trabaja en cualquier tipo de
entorno. Por eso, posiblemente usar `git config --global push.default
current` nos evite sustos de actualizaciones de ramas que, en ese
momento, no quisiéramos actualizar.