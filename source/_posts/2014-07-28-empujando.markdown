---
layout: post
title: "Empujando"
date: 2014-07-28 08:49:53 +0200
comments: true
categories: tips, push, tags, branches
---

`push` hace muchas cosas, pero no lo hace todo. En principio, sólo sincroniza ramas que están en los dos repositorios. Para que se *entere* de nuevas ramas hay que decírselo a caso hecho.

Si hemos creado una nueva rama con 

```
git checkout -v esa_rama_oe
```

Tras modificar los ficheros, `git push` no hará nada, porque esa rama no existe `upstream`, el lugar de donde nos lo hemos bajado. Para crearla

```
git push -u origin esa_rama_oe
```

que le indica que la rama *upstream* (`-u`) en `origin` se va a llamar de la misma forma. Cada vez que se haga push se hará sobre todas las ramas que se hayan modificado.

Un tipo especial de ramas son las etiquetas o *tags*. En realidad, son como una rama *ligera*: `git tag -a v0.0.1 -m "Primera versión"` etiquetará el último *commit*, pero una vez más la etiqueta será local. El comando anterior no servirá, puesto que estas *ramas* son en realidad notas sobre etiquetas. [Habrá que usar](http://stackoverflow.com/questions/5195859/push-a-tag-to-a-remote-repository-using-git)

```
git push --tags
```

(si quieres que suba todas las etiquetas al repositorio).
