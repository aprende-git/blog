---
layout: post
title: "Checkout con doble guión"
date: 2014-08-25 12:07:09 +0200
comments: true
categories: tips, checkout, branches
---

Alguna vez nos hemos podido encontrar una expresión de este tipo

```
git checkout una.rama -- un.fichero
```

que tiene por medio el doble guión, *double dash* o *dash dash*. Como
resulta difícil de buscar tal cosa en Google se usa en plan *cargo
cult*, o sea, siempre, o nunca. Lo que es innecesario.

Como explica en
[esta entrada de StackOverflow, sea siempre bendito y alabado](http://stackoverflow.com/questions/13321458/meaning-of-git-checkout-double-dashes),
se trata simplemente de separar los nombres de rama de los nombres de
fichero, o las opciones de línea de órdenes de los nombres de fichero.

Por ejemplo, si hacemos

```
git checkout -b hola.py
```

y luego creamos un fichero `hola.py` dentro, la forma de extraerlo
desde la rama `master` sería

```
git checkout hola.py -- hola.py
```

Si lo hubiéramos hecho de otra forma, habríamos obtenido un error

```
git checkout hola.py hola.py
fatal: ambiguous argument 'hola.py': both revision and filename
Use '--' to separate filenames from revisions
```

De todo esto la conclusión obvia es que no usemos nombres de rama que
parezcan nombres de ficheros, hombre, por favor. Pero si lo hacemos,
`git` nos da la solución.

