---
title: "Manten tu documentacion a mano con Zeal"
date: 2015-03-13T15:50:34-04:00
lastmod: 2015-03-13T15:50:34-04:00
tags: [documentation, dogfooding, spanish]
---

Zeal es una herramienta para explorar la documentación de las API más
populares en modo desconectado. Está inspirado en
[Dash](http://kapeli.com/dash) y está disponible para GNU/Linux y MS
Windows.<!--more--> Está liberado bajo la licencia
[GPL](https://github.com/zealdocs/zeal/blob/master/COPYING) y cuenta
entre sus características:

-   Búsqueda rápida dentro de Zeal usando el atajo Alt+Espacio desde
    cualquier parte de su espacio de trabajo.
-   Búsqueda en múltiples conjuntos de documentación al mismo tiempo.
-   Elimina la dependencia de la conexión a Internet.
-   Se integra con Emacs, Sublime Text y Vim entre otros.

Para cada plataforma Zeal tiene su mecanismo de instalación, binarios
para MS Windows, PPAs para Ubuntu Linux o compilarlo. En todo caso esto
último tampoco es nada complicado, instalar las
[dependencias](http://zealdocs.org/download.html) y luego desde el
terminal:

```bash
$ git clone git@github.com:zealdocs/zeal.git
....
.... (chum chum chum) ...
....
$ cd zeal
$ qmake-qt5
$ make
....
.... (chum chum chum) ...
.... 
$ bin/zeal
```

Una vez que ejecutes Zeal aparecerá:

![Pantalla inicial de Zeal](/images/zeal01.png)

El siguiente paso es agregar las colecciones de documentación que sean
de tu interés. Para ello es necesario ir al menu `Edit > Options` y
en la nueva ventana buscar la pestaña `Docsets` seleccionar la
documentación de los productos que desees.

![Carga de Docsets](/images/zeal02.gif)

Y ahora estará listo para contar con la documentación en todo momento
mientras construyes herramientas asombrosas.

![Interfaz de Zeal](/images/zeal03.png){width="100%"}

![Búsqueda en Zeal](/images/zeal04.png){width="100%"}

Zeal permite integrarse con Emacs, Sublime Text y Vim entre otros,
visita en la página la sección de
[plugins](http://zealdocs.org/usage.html#plugins) para más información.

Para más información
--------------------

-   Sitio oficial de [Zeal](http://zealdocs.org/).
-   Repositorios en [GitHub](https://github.com/zealdocs/).
-   [\#zealdocs](irc://irc.freenode.net/zealdocs) en freenode.
-   En caso de utilizar Mac o iOS la herramienta para ti se
    llama [Dash](http://kapeli.com/dash).

