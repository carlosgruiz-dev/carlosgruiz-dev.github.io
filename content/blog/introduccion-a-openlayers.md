---
title: "Introduccion a Openlayers"
date: 2010-06-09T23:49:35-04:00
lastmod: 2014-12-13T14:35:35-04:00
tags: [lab, geomatics, openlayers, web, spanish]
---

Una de las cosas con las que he trabajado últimamente es con
[OpenLayers](http://www.openlayers.org/). Este es una librería de
JavaScript muy interesante para colocar mapas en una página web. Así que
pues qué más simpático que compartir poco a poco lo que he aprendido en
el camino.
<!--more-->

Primero que todo hay que comprender que pues lo mejor para iniciarse con
[OpenLayers](http://www.openlayers.org/) es ver un poco los ejemplos,
tratar de ver donde calza dentro de la aplicación que estamos desarrollando,
leer un poco de formatos SIG (GIS en inglés) y manos a la obra. Para ver 
los ejemplos haga click
[\[aquí\]](http://dev.openlayers.org/releases/OpenLayers-2.9.1/examples/).

Lo primero que hay que entender para trabajar con OpenLayers es el
concepto de capas dentro de un mapa. Esto se refiere a que tenemos capas
superpuestas una sobre otra como un cuaderno de papel cebolla y ello nos
permitirá visualizar o esconder información dentro del mapa. Estas capas
pueden venir en múltiples formatos (servicios OGC, datos de GoogleMaps,
Yahoo! Maps, Bing Maps, formatos vectoriales como KML, GML entre otros).
Cuando incrustamos dentro de nuestra web un mapa lo que estamos haciendo
es llamar a estas capas de información y visualizarlas en el widget de
mapas que nos provee OpenLayers.

Hagamos un ejemplo sencillo.

Lo primero es crear un archivo HTML vacío para ir completando

```html
<html>
    <head>
        <title>Mi Primer Mapa con OpenLayers</title>
    </head>
    <body>
    </body>
</html>
```

Luego agreguemos OpenLayers a nuestra página, para ello incluimos dentro
de la etiqueta **head** las siguientes líneas para declarar el estilo
que define el tamaño del widget y el llamado a la api de OpenLayers
desde su web (en caso de querer colocar el archivo OpenLayers.js en su
servidor simplemente descargue el paquete comprimido).

```html
<style type="text/css">
  #map {
  width: 700px;
  height: 500px;
  border: 1px solid #ccc;
  }
</style>
<script src="http://www.openlayers.org/api/OpenLayers.js"></script>
```

A continuación pongamos una etiqueta **div** dentro del cuerpo del HTML
para agregar el widget de mapas.

```html
<div id="map" class="map"></div>
```

Ya tenemos listo nuestro HTML, solo basta decirle a OpenLayers que
cargue una capa dentro de el widget de mapas y decirlo que arranque al
iniciar la página. Para ello agregamos el siguiente código:

```html
<script>
  var map, wms;
  function init() {
      map = new OpenLayers.Map("map");
      wms = new OpenLayers.Layer.WMS(
            "Capa Base",
            "http://labs.metacarta.com/wms/wmap0",
             {layers: "basic"});
      map.addLayer(wms);
      map.addControl(new OpenLayers.Control.LayerSwitcher());
      map.zoomToMaxExtent();
  }        
</script>
```

y

```html
<body onload="init()">
```

para que el código se vea así..

```html
<html>
  <head>
      <style type="text/css">
          #map {
          width: 700px;
          height: 500px;
          border: 1px solid #ccc;
          }
      </style>
      <script src="http://www.openlayers.org/api/OpenLayers.js"></script>
      <title>Mi Primer Mapa con OpenLayers</title>
      <script>
          var map, wms;
          function init() {
              map = new OpenLayers.Map("map");
              wms = new OpenLayers.Layer.WMS(
                  "Capa Base",
                  "http://labs.metacarta.com/wms/wmap0",
                  {layers: "basic"});
              map.addLayer(wms);
              map.addControl(new OpenLayers.Control.LayerSwitcher());
              map.zoomToMaxExtent();
          }
      </script>
  </head>
  <body onload="init()">
      <div id="map" class="map"></div>
  </body>
</html>
```

y al abrirlo en tu navegador se verá así..

![Ejercicio Completado](/images/OL.png)


