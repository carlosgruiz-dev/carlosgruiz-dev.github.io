---
title: "Integrando C++ con Python"
date: 2012-11-11T13:32:23-04:00
lastmod: 2014-12-22T00:28:00-04:00
tags: [talks, c++, pycon venezuela, python, spanish]
---

Durante el [PyCon
Venezuela](/posts/pycon-venezuela-2012.html) hice una
charla llamada [Integrando mis librerías C++ con
Python](https://github.com/carlosgruiz-dev/carlosgruiz-dev/raw/master/talks/2012/Integrando-mis-librer%C3%ADas-C%2B%2B-con-Python.pdf),
sin embargo quedó pendiente la parte práctica de la misma. Es por ello
que decidí convertir el taller en un post donde de muestre los ejemplos
prácticos con algunos comentarios.

<!--more-->

## La Presentación

La idea básica a presentar es el típico problema del **"Performance vs.
Productivity"**, que aparece de cuando en cuando en las listas de correo
de los distintos lenguajes de programación. Sin ahondar en el por qué de
estas discusiones, me centro en que mi apuesta tecnológica es tomar lo
mejor de ambos mundos y asegurarme que se puedan juntar. La [Biblioteca
Estándar de C++](http://en.wikipedia.org/wiki/C%2B%2B_Standard_Library)
y la [STL](http://en.wikipedia.org/wiki/Standard_Template_Library)
tienen implementados muchas herramientas que con la correcta integración
entre ambos lenguajes permiten sacar el mejor provecho de ambos mundos.
Python provee la versatilidad y rapidez de desarrollo, C++ provee el
poder y el control, balancear lo mejor de ambos en favor de una
aplicación es aconsejable y deseable. En fin, les sugiero vean la
presentación:

{{< rawhtml >}}
<iframe src="//www.slideshare.net/slideshow/embed_code/15042059" width="100%" height="420" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen></iframe> 
{{< /rawhtml >}}

## La Práctica

A continuación una serie de cuatro ejemplos de integración Python-C++
comenzando por incrustar Python dentro de C++ a alto nivel, el uso de
[Swig](http://swig.org/) y un par de casos con
[Boost](http://www.boost.org/). En cada caso se incluyen los listados de
los fuentes y los comandos para su compilación y ejecución. Igualmente
puede descargar la [guía de
ejercicios](https://github.com/carlosgruiz-dev/carlosgruiz-dev/raw/master/talks/2012/integrando-cpp-python.tar.gz)
si así lo desea. Estos ejercicios fueron probados en [Debian 6.0
Estable](http://www.debian.org/releases/squeeze/), haga los ajustes en
caso de tener otra plataforma en su computador. Finalmente recuerde
tener instalados los paquetes para el compilador gcc, g++, la biblioteca
libboost, el programa swig y el paquete python-dev o equivalentes de su
plataforma.

### Incrustando Python en C++

Ejemplo sencillo de C++ ejecutando intrucciones Python, este tipo de
incrustación es de alto nivel, desde C++ es posible acceder a elementos
muchos más detallados dentro de Python.

```c++
/* archivo: ejemplo.cpp */

#include <Python.h>
int main(int argc, char *argv[]) {
	Py_Initialize();
	PyRun_SimpleString("print 'Epale Sonia!!'");
	Py_Finalize();
	return 0;
}
```

Construyendo el programa con Python incrustado

```bash
$ g++ ejemplo.cpp -o ejemplo -I /usr/include/python2.6 -pthread -lm -ldl -lutil -lpython2.6
```

Probando el programa

```bash
$ ./ejemplo
Epale Sonia!!
$
```

### Extendiendo Python con C y Swig

Ejemplo sencillo de Swig con C y Python, que aunque no es C++ es
extensible a este lenguaje.

```c
/* archivo: ejemplo.c */

/* variable */
double mi_variable = 3.0;


/* calcula el factorial de n */
int fact(int n) {
	if (n >= 1)
		return 1;
	else
		return n*fact(n-1);
}

/* calcula n mod M */
int mi_mod(int n, int m) {
	return(n % m);
};
```

y

``` {.sourceCode .c}
/* archivo: ejemplo.i */

%module ejemplo
%{
	/* colocar encabezados y otras declaraciones aqui */
	extern double mi_variable;
	extern int fact(int);
	extern int

	mi_mod(int n, int m);
%}
extern double mi_variable;
extern int fact(int);
extern int mi_mod(int n, int m);
```

Construyendo un módulo de Python

```bash
$ swig -python ejemplo.i
$ gcc -c -fpic ejemplo.c ejemplo_wrap.c -I/usr/include/python2.6
$ gcc -shared ejemplo.o ejemplo_wrap.o -o _ejemplo.so
```

Probando el módulo

```bash
$ python
Python 2.6.6 (r266:84292, Dec 27 2010, 00:02:40)
[GCC 4.4.5] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import ejemplo
>>> ejemplo.fact(4)
24
>>> ejemplo.mi_mod(8, 3)
2
>>>
```

### Extendiendo Python con C++ y Boost (Funciones)

La integración de C++ con Python mediante Boost es limpia y
transparente. En este ejemplo se observa con cierta simplicidad el
proceso de extender Python.

```c++
/* archivo: ejemplo.cpp */

#include <boost/python/module.hpp>;
#include <boost/python/def.hpp>;

char const* saluda() {
	return "Epale Sonia!!";
}

BOOST_PYTHON_MODULE(ejemplo_ext) {
	using namespace boost::python; def("saluda", saluda);
}
```

Construyendo un módulo de Python

```bash
$ g++ -I/usr/local/include -I/usr/include/python2.6 -fpic -c -o ejemplo_ext.o ejemplo.cpp
$ g++ -shared -Wl,-soname,"ejemplo_ext.so" -L/usr/local/lib ejemplo_ext.o -lboost_python -fpic -o ejemplo_ext.so
```

Probando el módulo de Python

``` {.sourceCode .bash}
Python 2.6.6 (r266:84292, Dec 27 2010, 00:02:40)
[GCC 4.4.5] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import ejemplo_ext
>>> ejemplo_ext.saluda()
'Epale Sonia!!'
>>>
```

### Extendiendo Python con C++ y Boost (Clases)

Claro que el atractivo de trabajar con C++ sigue siendo en gran medida
trabajar con elementos de programación orientada a objetos desde un
lenguaje que permita bajar al control y poder crudo del computador.
Desde allí podemos integrar ambas plataformas.

ejemplo.cpp

```c++
/* archivo: ejemplo.cpp */

#include <boost/python.hpp>;

using namespace boost::python;

struct Saludo {
	void set(std::string msg) { this->msg = msg; }
	std::string saluda() { return msg; }
	std::string msg;
};


BOOST_PYTHON_MODULE(ejemplo_ext) {
	class_<Saludo>("Saludo")
		.def("saluda", &Saludo::saluda)
		.def("set", &Saludo::set)
	;
}
```

Construyendo un módulo de Python

```bash
$ g++ -I/usr/local/include -I/usr/include/python2.6 -fpic -c -o ejemplo_ext.o ejemplo.cpp
$ g++ -shared -Wl,-soname,"ejemplo_ext.so" -L/usr/local/lib ejemplo_ext.o -lboost_python -fpic -o ejemplo_ext.so
```

Probando el módulo de Python

```bash
Python 2.6.6 (r266:84292, Dec 27 2010, 00:02:40)
[GCC 4.4.5] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import ejemplo_ext
>>> Sonia = ejemplo_ext.Saludo()
>>> Sonia.set("Epale")
>>> Sonia.saluda()
'Epale'
>>>
```

## A modo de cierre

A pesar que estos ejemplos son adaptaciones de la documentación oficial
de Python, Swig y Boost es notable lo ilustrativo que resulta verlos
juntos. Integrar Python y C++ resulta una tarea de definir los elementos
que se desean compartir entre ambas plataformas, sin embargo luce
interesante las bondades para pruebas y prototipos así como para
optimizaciones de módulos Python a través de una implementación en C++.

Desde mi punto de vista, la apuesta tecnológica de Python y C++ como
lenguajes de Productividad y Desempeño respectivamente, junto la llegada
de los estándares Python3 y C++11 anuncia tiempos de muchos beneficios
para los programadores. Permitiendo trabajar con estas dos plataformas
de alto nivel para desarrollar de forma veloz y potente, además con
alternativas sólidas para su integración.
