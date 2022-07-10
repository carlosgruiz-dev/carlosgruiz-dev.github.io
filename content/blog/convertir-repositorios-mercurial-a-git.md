---
title: "Convertir repositorios Mercurial a git"
date: 2013-02-04T16:04:00-04:00
lastmod: 2014-12-22T12:25:00-04:00
tags: [git, mercurial, guides, spanish]
summary: Recientemente he comenzado una mudanza de los repositorios de mis proyectos abiertos en Bitbucket a GitHub, esto ha hecho necesario que migre algunos de ellos que se encuentran en Mercurial a git.
---

Recientemente he comenzado una mudanza de los repositorios de mis
proyectos abiertos en Bitbucket a
[GitHub](https://github.com/carlosgruiz-dev), esto ha hecho necesario que
migre algunos de ellos que se encuentran en Mercurial a git. Las
soluciones que había conseguido hasta ahora eran cuando menos
engorrosas, pero hoy di con una que funciona de maravillas. Y se las
comento por acá, se llama
[fast-export](http://repo.or.cz/w/fast-export.git) y es muy simple de
utilizar, el paso a paso se describe sólo:

```bash
$ git clone git://repo.or.cz/fast-export.git
$ git init nuevo_repositorio
$ cd nuevo_repositorio
$ /ruta/para/hg-fast-export.sh -r /ruta/para/repositorio_hg
$ git checkout HEAD
```

Pocos segundos después obtuve una copia de mi repositorio en formato git
junto con un resumen de las operaciones realizadas.