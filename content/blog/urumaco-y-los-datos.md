---
title: "Urumaco y los datos"
date: 2012-12-03T08:26:45-04:00
lastmod: 2015-02-26T23:28:00-04:00
tags: [lab, data, geomatics, qt, spanish]
summary: Urumaco es de esos proyectos donde comienzas a estudiar una tecnología y poco a poco te involucras en algo más grande. Además es un desarrollo al que le he tomado cariño.
---

![Logo Urumaco](/images/valessiobrito_Hoof_of_Green_Turtle.png)

[Urumaco](https://github.com/carlosgruiz-dev/urumaco) es de esos proyectos
donde comienzas a estudiar una tecnología y poco a poco te involucras en
algo más grande. Además es un desarrollo al que le he tomado cariño. No
está ni cerca de estar terminado por muchas razones: la primera es
tiempo pues siempre cerrar un año de trabajo es complicado, más aun con
una lista de pendientes tan nutrida; otra razón son los datos, y de esto
comentaré un poco.

Pero antes, ¿Qué es Urumaco? bueno, pretende ser un visualizador
cartográfico, orientado principalmente a un propósito educativo pero con
opción a que pueda ser utilizado en otros ámbitos. Para ello parte de
algunas premisas; cargar capas de información a partir de una lista fija
almacenada en forma local, que permita enfocar el programa en los datos
que se desean incorporar y quitando a la aplicación de la necesidad de
conexión para acceder a los mismos; las operaciones básicas de
navegación dentro del mapa como lo son acercar, alejar, mover; consulta
a la base de datos de las capas seleccionadas con una herramienta de
información; y finalmente un componente de modificación de la simbología
del mapa.

Para ello el uso de las bibliotecas de programación de [Quantum
GIS](http://qgis.org) son de gran apoyo, aun cuando la documentación no
sea muy abundante. Tal vez en el proceso de generar esta aplicación
surja algún tutorial de cómo hacer una aplicación de mapas con
[libqgis](http://www.qgis.org/api/) (C++) o con
[PyQGIS](http://www.qgis.org/pyqgis-cookbook/index.html) (Python),
dependerá del tiempo que se tenga disponible. Hasta acá no hay mayor
problema pues las limitantes son internas al producto programado. La
otra cara de la moneda son las limitantes correspondientes a factores no
definidos por el proyecto sino por insumos de terceros y en este sentido
la información cartográfica es un tema interesante de explorar.

Especialmente en las aplicaciones geográficas (georeferenciadas o
cartográficas según sea la jerga que prefiera) la relevancia del dato es
crucial, pues el mejor sistema sin datos es un cascarón vacío. Esto es
un poco lo que ha pasado: el proyecto sucitó interés dentro del equipo
de [Canaima Educativo](http://www.canaimaeducativo.gob.ve/) y ello
conllevó a parte de su equipo a tramitar frente al [Instituto Geográfico
de Venenezuela "Simón Bolivar"](http://igvsb.gob.ve/) un grupo de datos
para este programa y allí comienzan algunos quebraderos de cabezas. Un
aspecto han sido los datos, pues al menos en Venezuela contrasta de
forma resaltante los temas respecto a la libertad del software con la
mezquindad y reserva con que se manejan los datos. No haré de esta
publicación un decálogo de problemas relacionados con la obtención de
datos, sino un apartado para que se comprenda su dificultad. En
principio se solicitó los datos para incorporar al programa, formato
vectorial de la división política territorial del país, vías, ríos,
etcétera. Lo recibido en aquella ocasión fue en resumen un mapa en
formato imagen (específicamente en formato JPEG) de un mapa de
Venezuela. Obviamente no se comprendió lo que se pidió. Posteriormente,
se volvió a solicitar la información y la respuesta fue que sería
despachado "en formato WMS", pero el [Web Map
Service](http://es.wikipedia.org/wiki/Web_Map_Service) es un formato de
servicio de datos vía web que rompe con la premisa de almacenamiento
local.

Seguidamente al tercer intento llegaron los datos, no mentiré al decir
que al recibirlos tuve mis reservas basadas en las entregas anteriores,
pero una vez revisados y cargados en Quantum GIS los datos brillaron. Un
pequeño set de datos ya estaba en manos del proyecto. Pero, si..
aparentemente siempre hay un pero, no entregaron las condiciones de uso.
Es especialmente delicado este tema, pues a falta de una política clara
y transparente respecto al dato, y por ser recibidos no como la norma
sino como una excepción, entonces pregunté por la licencia con la cual
puedo usar los datos. No había tal, no habían condiciones de uso, pero
lo que si estuvo muy claro es que no podía hacer públicos los datos (un
ejemplo que considero interesante de justamente lo contrario es
[GeoGratis](http://geogratis.cgdi.gc.ca/geogratis/en/index.html) de
Canadá). Luego de una llamada telefónica explicando que no puedo hacer
un programa que almacene los datos localmente sin hacer públicos los
datos, como decimos en criollo, lancé la bola a la cancha del IGVSB y
Canaima Educativo. Afortunadamente esto está conllevando a un convenio,
según tengo entendido, entre el IGVSB y el Proyecto Canaima Educativo
(con el [Centro Nacional de Tecnologías de
Información](http://www.cnti.gob.ve/) y el [Ministerio de
Educación](http://www.me.gob.ve/)), lo que permitirá allanar el camino a
acceder a los datos aunque probablemente no tan libremente como se
aspirara, habrá que esperar a ver.

Otro aspecto es que yo no represento, no pertenezco, ni he sido
contratado, ni he recibido donaciones, ni retribución por alguna por
parte de los entes que han manifestado interés en el proyecto. Esto lo
digo en varios sentidos, esta sigue siendo una iniciativa personal e
independiente que desarrollo, por lo que el acceso a la información se
hace un poco más engorrosa, pues como externo debo valerme de
comunicaciones y solicitudes a veces hasta a 3 o 4 niveles de distancia
de comunicación, lo que igualmente me lleva a ser muy cauto en
utilización de la información que se me facilita exigiendo
comunicaciones por escrito donde se me ceda a modo personal los recursos
(datos, equipos, etc). Por otro lado la iniciativa y los comentarios que
de ella surjan o no necesariamente reflejan la posición oficial u
opinión de los entes del estado que se han nombrado, ha habido
acercamientos no oficiales para tratar el asunto del desarrollo desde
dentro de la perspectiva de las Canaimitas, más a modo de buenas
intensiones que otra cosa. Finalmente, debido a que es una iniciativa
personal, debo desarrollarla en los espacios y tiempo que tenga
disponibles fuera de mis horas laborales, por lo que eventualmente no
podré ajustarme a cronogramas y a entregas que puedan necesitarse dentro
de los lanzamientos Canaima Educativo. Sería interesante concretar algún
modo de financiamiento para este proyecto, pero las diligencias en ese
sentido no han sido exitosas.

El próximo artículo sobre Urumaco seguramente tendrá más componentes
técnicos y algunos pantallazos. Hasta la próxima..

