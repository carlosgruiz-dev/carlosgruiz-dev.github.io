---
title: "OpenVE y los \"Kits de arranque\""
date: 2012-10-28T04:24:34-04:00
lastmod: 2015-03-05T23:17:00-04:00
tags: [tutorial, c++, github, guides, python, openve, spanish]
---

Hace unas semanas [Daniel Rodríguez](http://sadasant.com/) y [Osledy
Bazó](http://osledybazo.com/) me invitaron a participar en la iniciativa
[OpenVE](http://openve.github.com/) luego de la entrevista que me
realizaran en su podcast [EchandoCodigo](http://echandocodigo.com/).
Inicialmente no sabía mucho de que trataba, sin embargo me quedó más
claro cuando leí la declaración donde dice que **"es una comunidad libre
para la investigación y el desarrollo de proyectos de computación de
código abierto"** y que uno de sus objetivos es hacer disponible una
biblioteca de código abierto.

<!--more-->

![OpenVE](/images/openve_logo-300x300.jpeg)

Es así que buscando la manera de hacer aprovechables estos recursos se
me ocurrió crear una serie de "kits de arranque". La idea es que en los
primeros 15 minutos un programador pueda llevarse una idea y tomarle el
gusto al lenguaje que esté conociendo. Uno de los aspectos que tomé en
cuenta para construir estas guías es permitir a un programador
identificar puntos de referencia que le permitan ubicarse en el contexto
de la nueva plataforma.

El esqueleto de los kits es bastante estándar:

-   **Kit de Arranque**: con una breve presentación de la guía
-   **Consideraciones Iniciales**: donde se explican los supuestos
    iniciales de la guía. Plataforma donde fue escrito, compilador o
    intérprete utilizado, y en caso de ser necesario una pequeña
    explicación de cómo instalar las herramientas indispensables para
    la guía.
-   **Lo Básico explicado en 15 Minutos**: es el centro de la guía que se
    ocupa de explicar brevemente los aspectos elementales del lenguaje,
    su uso y recursos básicos.
    -   **Uso**: este es el cómo se usa el lenguaje, si es interpretado,
        compilado y como se hace cada una de estas cosas con
        el lenguaje.
    -   **Estructura de un Programa**: estructura de un programa escrito
        en este lenguaje, comenzando por un "Hola Mundo!" hasta un
        pequeño ejemplo de uso de llamados a módulos o uso de archivos
        de cabeceras, archivos de configuración o algún elemento
        equivalente de la plataforma.
    -   **Variables**: cada lenguaje tiene sus particularidades en el uso
        de variables, como la limitaciones en el uso de identificadores
        válidos (comenzarlas por \$, no iniciarlas con números, etc).
        También se describe en este punto si el lenguaje hace referencia
        a los tipos de datos válidos y, en el caso que
        existan, punteros.
    -   **Funciones**: indicando cómo se declaran, el paso de variables, y
        si esta disponible la sobrecarga, si es condicionada o
        simplemente no existe.
    -   **Control de Flujo del Programa**: cómo hacer una toma de
        decisiones en un programa o realizar una tarea repetitiva.
        -   *Alternativas Lógicas*: cómo escribir un *"si-entonces"* o
            un *"selecciona-caso"* dentro de la plataforma.
        -   *Bucles*: cómo realizar una serie de repeticiones mediante
            ciclos *"para"*, *"mientras"* o mediante
            llamados recursivos.
    -   *Otros básicos*: el cómo trabajar con objetos y clases, la
        construcción de estructuras de datos, u otro elemento esencial
        particular de la plataforma.
-   **Lo demás explicado en otros 15 Minutos**: normalmente indica un poco
    qué sigue a partir del momento en que se domine lo básico: librerías
    estándar, librerías recomendadas, herramientas, y nuevas tendencias.
-   **Licencia**: especifica la licencia con la cual se distribuye la
    guía, aunque he pensado que la que mejor se aplica es la cc
    [by-nc-sa](http://creativecommons.org/licenses/by-nc-sa/3.0/).
-   **Colaboradores**: Listado de quienes dedican su tiempo a escribir,
    revisar y mejorar la guía.

Inicié con las guías para C, C++ y Python en un fork a [mi cuenta
GitHub](http://github.com/carlosgruiz-dev) de los [repositorios de
OpenVE](https://github.com/openve), sin embargo la idea es enviar allí
las guías en cuanto estén avanzadas. Si le gusta este modelo de guía,
siéntase confiado en utilizarla para el lenguaje de su preferencia.
