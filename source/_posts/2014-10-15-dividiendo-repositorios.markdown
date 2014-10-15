---
layout: post
title: "Dividiendo repositorios"
date: 2014-10-15 20:04:31 +0200
comments: true
categories: mantenimiento, tips, trucos, ramas, filtros
---

Trabajando con
[este proyecto de un módulo en JS para algoritmos evolutivos](http://github.com/JJ/nodeo)
me he visto en la necesidad de separar por un lado los experimentos y
por otro el código, entre otras cosas para que sea más fácil hacer
*forks* del código sin llevarse todos los datos a la vez. Como todo en
`git`, es posible, pero dentro de un orden. En este caso, eliminar un
montón de ficheros con `git rm` deja toda la historia y múltiples
copias de los mismos en el repositorio, con lo que al final lo único
que tienes es que no estorba, pero te sigues bajando la cantidad de
megas que contienen todos los *commits*, y que continúan en el
repositorio.

La solución se llama
[`filter-branch`](http://git-scm.com/docs/git-filter-branch). Esta
orden te permite eliminar los *commits* que contengan un contenido
determinado. Por ejemplo, si has metido la pata y un fichero con claves se ha
tirado en el árbol durante varios commits, la forma de eliminarlo es
con esta orden. Pero en nuestro caso lo que queríamos eliminar era
varios directorios para "dividir en dos": en uno dejar todos los
directorios menos el que contenía los datos, y en otro dejar sólo el
de los datos.

Para borrar un directorio [se haría de esta forma, más o menos](https://confluence.atlassian.com/display/BITBUCKET/Split+a+repository+in+two):
```
git filter-branch --index-filter 'git rm --cached --ignore-unmatch -f -r noloquiero' -- --all
```
Como muchos otros comandos, es de esos que te hacen reflexionar en qué
diablos estaría pensando quien diseñó `git` para que fuera capaz de
ocurrírsele algo así. Pero despedazándolo va quedando un poco más
claro. Para empezar, miremos el comando de dentro de las comillas

```
git rm --cached --ignore-unmatch -f -r noloquiero
```

Este sería el comando que tendríamos que usar si quisiéramos borrar el
directorio `noloquiero` recursivamente (`-r`), es decir, con todos los
ficheros y otros directorios que haya dentro y a la fuerza, aunque
esté vacío (`-f`) y `--cached`, que lo quita del repositorio cuando se
haga el siguiente commit. Si quieres ver qué haría ese comando, añade
`-n` (que es una *ejecución en seco*, que no hace nada, pero te dice
qué haría). `--ignore-unmatch` es una salvaguarda para que no pete
cuando los ficheros desaparezcan de la historia. 

Lo que va a hacer la orden es ejecutar el resultado de esa en todos
puntos de la historia. Como si fuéramos, poco a poco, rebobinando la
historia y borrando los ficheros en todos los lugares donde
aparezca. Por eso se usa `--` (para separar las opciones de un comando
de los de otro) y `--all`, para hacerlo de todos los
*commits*. `--index-filter` indicará que la orden que vamos a dar
reescribirá el índice, es decir, los ficheros que se van a encontrar
en cada *commit*.

Y todo junto eliminará todo rastro del directorio *noloquiero* y
dejará la historia mucho más ligera. Como queríamos.
