---
title: "Receta para hacer un mapa electoral simple"
date: 2013-04-18T21:34:44-04:00
lastmod: 2013-04-18T21:34:44-04:00
tags: [tutorial, geomatics, data, qgis, spanish]
---

Muchas veces me preguntan, sobre todo cerca de los resultados de unas
elecciones cómo se puede hacer un mapa electoral. Como el tema electoral
es complejo en sus análisis, supongo inmediatamente que lo que en
realidad me piden es un mapa donde se evidencien los resultados de la
elección y generalmente tengo razón.<!--more-->Eso de votos duros, votos blandos,
tendencia del voto está más allá del interés de muchos.

## Receta

Bueno, entonces manos a la obra. Usted para un mapa de resultados
electorales necesitará:

### Ingredientes

- Una base cartográfica de la zona donde se realizó la elección
  - no tengo una base de que pueda distribuir pero siempre pueden
    buscar algo en google que les sirva.
- Un listado con los resultados electorales
  - tomé los resultados publicados en la prensa nacional →
    [Elecciones\_14\_abril\_2013](https://atmantree.keybase.pub/page/extras/elecciones.csv)
- [Quantum GIS](http://qgis.org) como Sistema de Información
  Geográfica
  - en Linux simplemente usa tu gestor de paquetes para instalar **qgis**
  - en caso de utilizar Windows deberás descargar algunos de los instaladores desde
    [acá](http://qgis.org/downloads/QGIS-OSGeo4W-1.8.0-2-Setup.exe).

### Procedimiento

Abra QuantumGIS y cargue su capa en formato Shapefile con la base de
cartográfica que desea utilizar para este mapa.

![Mapa Electoral 0](/images/mapa_electoral_0.png)

Seguidamente abra la tabla de su capa de información, agregue las
columnas con la información de los resultados electorales.

![Mapa Electoral 1](/images/mapa_electoral_1.png)

Seguidamente complete las columnas con los datos y utilice la
herramienta de calculadora de columnas para crear un indice que permita
mapear la diferencia entre los principales candidatos. En el ejemplo la
fórmula sería para crear una columna llamada índice con 2 decimales que
guarde los calculos de **(TOT\_NMM -TOT\_HCR) / TOT\_ELEC**.

![Mapa Electoral 2](/images/mapa_electoral_2.png)

Finalmente ya tenemos los datos completos. Ahora cierre la ventana de
datos, vuelva a la pantalla principal y proceda a modificar la
simbología de la capa de información. Utilice un estilo graduado,
seleccione la columna correspondiente al índice, seleccione la rampa de
color de su preferencia, presione el botón clasificar y aplique los
cambios.

![Mapa Electoral 3](/images/mapa_electoral_3.png)

Finalmente su mapa debe verse parecido a este (obviamente adaptado a su
mapa base y sus datos).

![Mapa Electoral 4](/images/mapa_electoral_4.png)

Así que hasta acá tiene su mapa electoral simple. No muy complicado
¿cierto?. Ahora usted podrá hacer otros mapas como los que se muestran a
continuación usando la misma herramienta y un poco de imaginación.

![Mapa Electoral 5](/images/mapa_electoral_5.jpg)

![Mapa Electoral 6](/images/mapa_electoral_6.jpg)
