---
layout: post
title: "Trabajando en un fork"
date: 2014-09-30 09:32:42 +0200
comments: true
categories: trucos, tips, ramas, branch, fork, pull request, branches
---

Hacer un *fork* es fácil, pero lo *forkeado* tiene la mala costumbre de seguir actualizándose con lo que llega un momento en que la copia se aleja cada vez más del original.

Mantenerse al día es simplemente cuestión de hacer un pull:
```
git pull git@github.com:JJ/GII-2014.git master
```
por ejemplo.

Sin embargo, uno se puede acabar hartando de meter esto, puede que haya desaparecido de la historia del shell o simplemente no recuerde la dirección original. Así que lo más fácil es hacer

```
git remote add upstream git@github.com:JJ/GII-2014.git 
```

Que define el alias `upstream` para el repositorio *original*, dejando *origin* para designar nuestra rama. Con este es simplemente cuestión de hacer, cada ciertotiempo

```
git pull upstream master
```
