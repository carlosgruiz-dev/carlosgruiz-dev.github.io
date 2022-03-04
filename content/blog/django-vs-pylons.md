---
title: "Django vs Pylons"
date: 2010-08-15T17:50:59-04:00
lastmod: 2014-12-16T23:26:00-04:00
tags: [lab, python, framework, spanish]
---

s comparaciones suelen ser odiosas, destapar algún
tipo de polémica o mostrar preferencias más allá del aspecto técnico y
objetivo de una plataforma o programa. Sin embargo, debido a que me toca
hacer una evaluación tecnológica para un proyecto me vi en la necesidad
de poner tratar de comparar las plataformas web disponibles en Python
que pudiesen apoyar mis actividades.

<!--more-->

![Logo de Django](/images/django-logo.png)

Ante todo aclaro que mi herramienta natural suele ser Django, que junto
con las herramientas de Python es lo que doy a conocer como mi "navaja
suiza" para resolver problemas. Pero al momento de una selección
tecnológica creo que esta selección por default puede no ser la mejor,
por ello me puse a revisar en la web los comentarios sobre las
comparaciones de estos dos web frameworks.

![Logo de Pylons](/images/pylons-logo2.gif)

He aquí la comparación y mis comentarios;

1.  **Otros Frameworks**: La primera consideración es por qué no incluir
    TurboGears dentro de mi evaluación. Si lo hice, sin embargo su forma
    de trabajo me resultó algo irritante. La versión 2.0 de TG está
    construida sobre Pylons, que si bien mejora la experiencia, aun no
    me convence. Y por qué no CherryPy? aunque no lo evalué a
    profundidad, me parece que le faltan herramientas para una
    comparación adecuada.
2.  **Popularidad**: La primera conclusión obvia es que Django tiene una
    comunidad muuucho mayor que Pylons. Incluso cuando van a los Google
    Trends, Django tiene 8 o 9 veces más tráfico. Sin embargo esto lo
    que indica es popularidad, lo que no quiere decir que sirva para
    mi app.
3.  **Interfaces Administrativas**: Django tiene mucha magia, y lo que
    me hace muchas veces llorar de alegría es el admin. En verdad pensé
    que me vería indefenso en este sentido con Pylons, pero la buena
    noticia es que hay un equivalente que, si bien no se ve tan pulido
    será de mucha utilidad (ver
    <http://docs.formalchemy.org/current/ext/pylons.html#administration-interface>).
4.  **Codificación**: Al comparar los demos y tutoriales de Django y
    Pylons salta a la vista que generalmente se observa más código
    en Pylons. Ello sin embargo es resultado a 2 razones; primero que
    los tutoriales no tienen comparación, los de Pylons suelen ser
    ejemplos más ambiciosos que los de Django; por otro lado, si.. en
    Pylons se escribe un poco más porque Django hace muchas cosas por
    nosotros y las damos por sentado.
5.  **Documentación y libros**: La documentación de Django es más
    compacta y en cuanto a libros hay más, aun así Pylons tiene no
    solamente la documentación propia sino generalmente una buena
    documentación de los programas que lo componen. En todo caso los
    primeros libros recomendados, además de la documentación oficial
    son, <http://www.djangobook.com/> y <http://pylonsbook.com/>
6.  **Diseño**: Hay que tener en cuenta que Django y Pylons aun cuando
    se diseñaron con el mismo paradigma (MVC aun cuando Django lo
    renombra MTV), ambos responden a visiones distintas, en el primer
    caso viene a ser un método de publicación eficiente de contenidos
    web, y en el segundo caso poner en la web aplicaciones. Esta
    diferencia redundará en cómo se aborda el desarrollo de las apps.
7.  **Reusabilidad**: Django tiene aplicaciones reusables (aunque
    algunas de ellas no son reusables en absoluto). Esto viene de la
    estrategia de hacer plugable las aplicaciones dentro del Framework.
    En Pylons el acercamiento es otro y la reutilización viene como
    implementaciones dentro de la aplicación en la que se
    esté trabajando.
8.  **Opciones y Newbies**: Definitivamente en este punto Pylons tiene
    mucho que decir, tiene muchas opciones, tantas que una persona
    iniciándose puede sentir que tiene mucho que aprender, de hecho la
    curva de aprendizaje es algo más pronunciada que en Django. Django
    por otro lado guía la selección del programador a sus herramientas
    con lo bueno y malo que puedan tener, aprender django puede resultar
    una experiencia gratificante por los rápidos resultados que muestra,
    pero a la hora de buscar opciones para incorporar más poder a las
    apps puede resultar engorroso y en algunos casos una camisa
    de fuerza. Pylons es más flexible en este sentido.
9.  **Plantillas**: Las plantillas en Django son realmente algo muy
    bueno, sin embargo opciones dentro de Pylons como Mako pueden
    resultar muy útiles. Mako se asemeja más a una función de Vista y
    permite introducir código Python dentro de las mismas. (aunque
    siempre que veamos mucho código python en una plantilla puede
    indicarnos que estamos colocando cosas donde no van)
10. **URL's**: no estoy familiarizado con Route (programa usado por
    Pylons para el direccionamiento de las URLs) por lo que no comentaré
    mucho más que funciona bien out-of-the-box. Las URLs en Django,
    lucen un tanto más legibles, funcionan bien y con un poco de
    expresiones regulares uno puede hacer cualquier cosa.
11. **Magia**: Django tiene vistas genéricas, un amplio conjuntos de
    aplicaciones en django.contrib y buenos atajos en django.shortcuts,
    sin nombrar a los decorators que nos facilitan la vida. El interfaz
    de admin realmente es una herramienta de lujo. Pylons no tiene
    muchas de estas cosas.

Cual usar? dependerá ahora de los requerimientos que tengan.. ;-) yo en
particular uso ambos, pues resuelven adecuadamente distintos problemas.
así que según sea el caso, uso uno u otro.

Para más información les dejaré estos links para el debate.

* <http://stackoverflow.com/questions/48681/pros-cons-of-django-vs-pylons>
* <http://stackoverflow.com/questions/1344824/django-vs-pylons>
* <http://www.noise-media.com/blog/pylons-vs-django/>
* <http://www.mutualinformation.org/2010/03/why-i-switched-to-pylons-after-using-django-for-six-months/>
* <http://jordanovski.com/django-vs-pylons>

Anímense a probar ambos Frameworks, realmente son excelentes
herramientas.
