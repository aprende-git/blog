---
layout: post
title: "Fusionar ficheros de otras ramas"
date: 2014-06-09 19:36:07 +0200
comments: true
categories: [Trucos,Tips]
---
¿Te ha sucedido a veces que has modificado un fichero en una rama
pensando que te encontrabas en otra rama?

Supongamos que tenemos el fichero `ese_fishero.pl` en la rama `feature-1` y
que, así por las buenas, hemos hecho los cambios ahí en vez de en la
rama `dev` que es en la que debería ir. Además, hay otros cambios en
esa rama, que, esos, no los quieres incorporar.

Nada más fácil:

``` 
git commit -am "Hala que me cambio"
git checkout dev
git checkout feature-1 ese_fishero.pl
[Resuelve conflictos]
git commit -am "Ya me lo he traido pacá"
```

La tercera línea te fusiona el fichero en la rama donde lo has
modificado (`feature-1`) por
equivocación con el de la rama donde tenías que haberlo
modificado (`dev`, que es en la que estás). Aunque no haya sido por equivocación, sino a caso
hecho. Puedes usarlo además con el número de ficheros qeu te dé la
gana. 
