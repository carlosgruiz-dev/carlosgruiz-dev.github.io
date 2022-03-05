---
title: "Tutorial \"Introducción a la programacion Qt\" y otros hallazgos en la azotea"
date: 2013-01-25T15:21:49-04:00
lastmod: 2015-03-07T14:31:00-04:00
tags: [tutorial, c++, mercurial, postgresql, python, qt, spanish]
---

En fin, hoy limpiando la wiki que solía utilizar en mi web personal
conseguí algunas curiosidades que valen la pena compartir.

<!--more-->

![tutorial "Getting Started Programming with Qt"](/images/notepad-qt.png)

Para todos los que nos iniciamos con Qt en algún momento nos ha tocado
comenzar por el tutorial ["Getting Started Programming with
Qt"](http://qt-project.org/doc/qt-4.7/gettingstartedqt.html). Sin
embargo quién lo haya realizado también sabrá que el mismo está lleno de
errores, partes incompletas y que normalmente cuando uno lo completa
siente una sensación de alivio al ver que logró superar a quien redactó
el tutorial. En fin, una de las cosas que hallé son los pasos resueltos,
así que para quienes quieran usarlos pueden descargarlos de
[aquí](https://atmantree.keybase.pub/page/extras/tutorial-qt.tar.gz).

## Unir repositorios Mercurial

También conseguí la lista de pasos para unir repositorios mercurial:

```bash
$ hg clone repo1 repo
$ cd repo
$ hg pull -f repo2
$ hg merge
$ hg commit -m "unión de repositorios"
```

## Eliminar espacios en blanco de nombres de archivos

Así mismo se encontraba esta lista de pasos para sustituir los espacios
en blanco de los nombres de los archivos, desde el intérprete de Python:

```python
>>> import os
>>> files = os.listdir(".")
>>> for i in files:
...     os.rename(i,i.replace(" ","_")) # cambia los espacios por guión bajo
...
>>>
```

## Mover una base de Datos PostgreSQL a un nuevo servidor

Otro truco salido del sombrero de un mago es una línea de comandos para
mover una base de datos PostgreSQL a un nuevo servidor.

```bash
$ pg_dump -h [servidor1] -U [usuario1] [base_de_datos1] | psql -h [servidor2] -U [usuario2] [base_de_datos2]
```

Espero a alguien le sean útiles estos trucos como me fueron a mi.
