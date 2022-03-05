---
title: "Frameworks de C++ para la web"
date: 2012-04-03T03:34:14-04:00
lastmod: 2015-03-03T00:17:00-04:00
tags: [lab, c++, web, framework, spanish]
summary: Normalmente al pensar en la web inmediatamente viene a la mente los nombres de lenguajes como Python, PHP, Perl o Ruby, Sin embargo haciendo una pequeña investigación podemos hacer un desmentido de esta idea. No solamente hay herramientas potentes sino que las hay con paradigmas bien variados.
---

![C/C++](/images/c-cpp.jpg)

Normalmente al pensar en la web inmediatamente vienen a nuestra mente
los nombres de lenguajes interpretados,
[Python](http://es.wikipedia.org/wiki/Python),
[PHP](http://es.wikipedia.org/wiki/PHP),
[Perl](http://es.wikipedia.org/wiki/Perl) o
[Ruby](http://es.wikipedia.org/wiki/Ruby), en otros casos los
“semi-compilados” como
[Java](http://es.wikipedia.org/wiki/Java_(lenguaje_de_programaci%C3%B3n))
o [.NET](http://es.wikipedia.org/wiki/.NET), en ese contexto se ha
creado un prejuicio según el cual
[C](http://es.wikipedia.org/wiki/Lenguaje_de_programaci%C3%B3n_C)/[C++](http://es.wikipedia.org/wiki/C%2B%2B)
como soluciones para servicios mediante
[CGI](http://es.wikipedia.org/wiki/Interfaz_de_entrada_com%C3%BAn). Sin
embargo haciendo una pequeña investigación podemos hacer un desmentido
de esta idea. No solamente hay herramientas potentes sino que las hay
con paradigmas bien variados. El fin de este artículo es más a modo
informativo que de prueba de cada tecnología, lo que no quiere decir que
a posteriori no desarrolle algunas de ellas en la wiki, sino que de
momento listaré las que consideré relevantes y sobre todo alternativas
vivas. Otra consideración es que a fin de facilitar la comprensión
compararé las soluciones con otras tecnologías existentes.

## Al estilo PHP, JSP, ASP y otros terminados en P

![tntnet](/images/tntnet-logo.png)

| | |
|-----------------|------------------------------------------------------|
| Nombre          | tntnet                                               |
| Website         | http://www.tntnet.org/                               |
| Licencia        | LGPL                                                 |
| Comenzar con    | http://www.tntnet.org/download/quick-start-guide.pdf |
| Paquetes Ubuntu | tntnet, tntnet-demos, tntnet-doc, tntnet-runtime     |


Es un concepto interesante pues es replicar la experiencia exitosa de
lenguajes que en plantillas HTML embeben código del lenguaje de
programación, aun cuando la diferencia fundamental en este caso es que
el C++ Server Pages permite (al compilar nativamente las páginas) evitar
la presencia del código fuente en el servidor. Adicionalmente, y
probablemente uno de los atractivos de usar C++ es incorporar la
variedad de librerías de esta plataforma a nuestras páginas, ello es
posible con todas las tecnologías que se nombran acá. Un detalle
interesante es que aun cuando no incluye un manejador para conexión a
base de datos ofrece un layer de abstracción que puede resultar
conveniente.

Una de las razones para desarrollar esta solución es pues que es un
estilo de programación web, permitiendo que los elementos programados de
la páginas se incorporen al diseño visual que alguien haya hecho
previamente. En general es una plataforma interesante y al menos en
apariencia bastante sencilla para incorporar el poder de C++ a sus
páginas web.

## Si lo quieres como MVC también hay quien te lo de

![TreeFrog Framework](/images/tff-logo.jpg)

| | |
|-----------------|-----------------------------------------------------|
| Nombre          | TreeFrog Framework                                  |
| Website         | http://www.treefrogframework.org/                   |
| Licencia        | BSD                                                 |
| Comenzar con    | http://www.treefrogframework.org/documents/tutorial |
| Paquetes Ubuntu | no disponibles                                      |

Una de las cosas que me gustó de este Framework es su concepto MVC, que
luce muy al estilo de [Ruby on
Rails](http://es.wikipedia.org/wiki/Ruby_on_Rails), tiene un demo
bastante decente de como hacer un blog y su web está bastante bien,
salvo por el hecho que se requiere que Google Chrome se haga cargo de
las secciones que aun se encuentran sin traducir desde el japonés. Aun
así es muy interesante el concepto y tal vez haga falta esperar a que
madure un poco.

Al mejor estilo de Rails tiene la generación del CRUD para las tablas de
su base de datos, detalle coqueto y que sin duda endulza el paladar de
más de uno. Por cierto, ¿comenté que está basado en Qt? pues si, lo que
facilita el trabajo en aspectos como el acceso a las bases de datos pues
simplemente hace falta habituarse al uso del módulo QtSQL que está muy
bien documentado. Comparativamente tiene algunas ventajas pues al
replicar las estrategias de otros Frameworks ofrece una solución
bastante completa (del tipo Full Stack). Aunque me parece promisorio en
muchos sentidos aun no diré que probarlo es comprarlo.

## Toolkit para GUI’s web, también hay

![Wt](/images/wt-logo.png)

| | |
|-----------------|------------------------------------------------------------|
| Nombre          | Wt (se pronuncia witty)                                    |
| Website         | http://www.webtoolkit.eu/                                  |
| Licencia        | Dual (posee licencia GPL y también una Licencia Comercial) |
| Comenzar con    | http://www.webtoolkit.eu/wt/doc/tutorial/wt.html           |
| Paquetes Ubuntu | witty, witty-dbg, witty-dev, witty-doc, witty-examples     |

Confieso que este acercamiento al desarrollo web desde C++ me gustó, les
explico por qué. En primera instancia se parece mucho más al paradigma
de programación de interfaces de usuarios implementado generalmente en
C++. Normalmente un programador en esta plataforma delega una buena
parte de la GUI a la librería encargada de eso y se concentra en el que
hace el programa, por lo que dedicar mucho tiempo a integraciones
JavaScript y otros vericuetos luce como un dolor de cabeza adicional. Un
Framework (en este caso un Toolkit) que se encargue de eso se agradece
mucho. Esto permite que su aplicación programada originalmente con otra
GUI, digamos Qt o GTK+, pueda ser portada con mayor facilidad a la web.
En otras palabras convertir el desarrollo web en una tarea similar al
desarrollo de GUI’s es un acercamiento deseable.

Uno de los detalles interesantes también es que una vez desarrollada la
solución se implementa mediante
[FastCGI](http://es.wikipedia.org/wiki/FastCGI), lo cual luce sumamente
conveniente. Incluso su website está programado con el Toolkit y es uno
de los ejemplos incluídos. Finalmente, es uno de los pocos que incluye
una descripción extensa del proceso de implantación (ver
[link](http://redmine.webtoolkit.eu/projects/wt/wiki/Wt_Deployment)).
Para ver la galería de Widgets con los que cuenta este toolkit basta con
mirar el siguiente [ejemplo](http://www.webtoolkit.eu/widgets/). En fin,
de las herramientas examinadas hasta el momento es quizá la solución más
completa.

## Pensado en altas cargas de trabajo..

![CppCMS](/images/cpp-cms-logo.png)


| | |
|-----------------|-----------------------------------------------------------------|
| Nombre          | CppCMS                                                          |
| Website         | http://cppcms.com/                                              |
| Licencia        | Dual (posee licencia LGPL y también una Licencia Comercial)     |
| Comenzar con    | http://cppcms.com/wikipp/en/page/cppcms_1x#Tutorials            |
| Paquetes Ubuntu | a través del repositorio http://cppcms.com/wikipp/en/page/apt   |

Curiosamente el nombre de este Framework es confuso pues pudiese
pensarse que corresponde a un
[CMS](http://es.wikipedia.org/wiki/Sistema_de_gesti%C3%B3n_de_contenidos),
sin embargo se define como una plataforma para abordar grandes volúmenes
de trabajo, incluso animan a quienes no tienen una plataforma estresada
por cargas de trabajo que utilicen herramientas como
[Django](http://es.wikipedia.org/wiki/Django) o
[Drupal](http://es.wikipedia.org/wiki/Drupal) (ver
[rationale](http://cppcms.com/wikipp/en/page/rationale), los
[benchmark](http://cppcms.com/wikipp/en/page/benchmarks_all) y la
[comparación de
desempeño](http://cppcms.com/wikipp/en/page/benchmarks_php)). La
escalabilidad del servicio con esta plataforma es uno de sus grandes
valores, pues permite que en vez de crecer en granjas de servidores o
soluciones, un cambio tecnológico permita sacar mejor provecho de los
recursos disponibles.

Es del estilo de entornos MVC, sin embargo no es tan a lo Rails como
TreeFrog. Es un Framework rico en detalles, sin embargo sus opciones no
son guiadas por herramientas que “hacen todo” sino más bien dando
libertad a los programadores de desarrollar la solución más adecuada
para su problema. Una ventaja comparativa es que posee un par de
proyectos desarrollados con CppCMS,
[Wiki++](http://cppcms.com/wikipp/en/page/install_wikipp) y
[CppBlog](http://cppcms.com/wikipp/en/page/install_cppblog) que en casos
de alta demanda pueden ser soluciones muy prácticas. En fin, una
alternativa más con un objetivo particular.

## Notas Finales

Al escribir este artículo se me presentó la idea que tal vez no lucen
muchas alternativas para C++ ante la avalancha que puedan mostrarse
con PHP o Python por solamente nombrar dos. Sin embargo, debo
aclarar que sólo incluí aquellos que me parecieron pertinentes y
relevantes, pues al igual que pasa con los demás lenguajes siempre habrá
un referente para estas tecnologías dentro de cada uno
([Rails](http://es.wikipedia.org/wiki/Ruby_on_Rails) en Ruby, Django
en Python, [Symfony](http://es.wikipedia.org/wiki/Symfony) en PHP). En
todo caso queda a sus necesidades y curiosidad el que pueda usar alguno
de estos frameworks o no. Salud!
