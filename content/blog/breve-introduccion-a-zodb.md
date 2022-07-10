---
title: "Introduccion a ZODB"
date: 2013-07-26T19:31:00-04:00
lastmod: 2015-03-04T20:00:00-04:00
tags: [lab, guides, python, databases, spanish]
---

En concreto ZODB (Zope Object Data Base) es un gestor de bases de datos
orientado a objetos. Esto significa para el usuario nuevo en esta
tecnología que a diferencia de las bases de datos de uso mas frecuente
en ZODB no hallará tablas ni esquemas ni nada parecido, así mismo no
encontrará sentencias SQL en pues el lenguaje de consulta e indexado es
Python.<!--more-->

## Instalación

Instalar ZODB en su computador es bastante sencillo, en caso de tener
instalado [Fedora Linux](http://fedoraproject.org/) deberá escribir el
siguiente comando `$ su -c "yum install python-ZODB"` y en caso de
tener [Debian Linux](http://www.debian.org/) sustituir el comando
anterior por este `$ su -c "aptitude install python-zodb"`. Si es
programador python probablemente prefiera realizar la instalación en un
entorno virtual (virtualenv). Nótese que requerirá tener instalado un
compilador como gcc para compilar ZOBD en este proceso. En este caso la
instrucción será:

```bash
$ virtualenv --no-site-packages env
$ source env/bin/activate
(env) $ pip install ZODB3
...
... (chum chum chum) ...
...
(env) $
```

## ZODB desde el intérprete de Python

Una vez instalado comenzar a utilizar ZODB es bastante directo. Se
incorporan los paquetes necesarios, definimos una fuente de datos,
establecemos una conexión, buscamos la raíz de la Base de Datos y listo.
ZODB funciona entonces como una Base de Datos de llave-valor de objetos
python. Veamos un ejemplo:

```python
>>> # llamado a los paquetes 
>>> from ZODB import DB, FileStorage
>>> import transaction
>>>
>>> # se define la fuente física donde se encuentran los datos
>>> almacen = FileStorage.FileStorage("Datos.fs")
>>> bd = BD(almacen)
>>> con = bd.open()
>>> r = con.root()
>>> 
>>> # ahora a guardar información  
>>> r['saludo'] = 'Hola ZODB' 
>>> r['numero'] = 3 + 7j
>>> r['lista'] = [1, 3, 5.987, True, 'texto']
>>>
>>> # para ver las llaves que tenemos almacenadas
>>> r.keys()
['lista', 'saludo', 'numero']
>>>
>>> # almacenamos los cambios en el archivo de almacén
>>> transaction.commit()
>>>
>>> # cerramos la conexión.
>>> transaction.get()
>>> transaction.abort()
>>> con.close()
>>> bd.close()
>>> almacen.close()
```

## Programa Simple

Una lista de cosas pendientes (ToDo List) es un buen ejemplo de cómo
podemos aprovechar esta base de datos. Acá una aproximación algo rústica
utilizando ZODB como una base de datos de llave-valor (key-value).
Creamos una clase que se encargue de manejar la conexión con el archivo
de datos y operaciones de agregar, listar y borrar tareas. Seguidamente
nos encargamos de manejar los argumentos de líneas de comandos y listo,
tenemos nuestro pequeño programa de lista de cosas pendientes. Vea el
código fuente:

```python
# -*- coding: utf-8 -*-

from ZODB import (DB, FileStorage)
import transaction
import argparse

class ToDo:
    def __init__(self):
        self.store = FileStorage.FileStorage("ToDo.fs")
        self.database = DB(self.store)
        self.connection = self.database.open()
        self.root = self.connection.root()

    def __enter__(self):
        return self

    def __exit__(self, type, value, traceback):
        transaction.get()
        transaction.abort()
        self.connection.close()
        self.database.close()
        self.store.close()

    def add(self, key, value):
        if key != "":
            self.root[key] = value
            transaction.commit()
            print("New task added..")
        else:
            print("A task must have a name")

    def list(self):
        print("Tasks To Do..")
        for k in self.root.keys():
            print("%s\t%s" % (k, self.root[k]))

    def delete(self, key):
        if key in self.root.keys():
            del(self.root[key])
            transaction.commit()
            print("Task deleted..")
        else:
            print("There is no task '%s'.." % key)

if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument('-a', '--add', nargs=2, help="add a tast to the ToDo list")
    parser.add_argument('-d', '--delete', nargs=1, help="delete a task from the ToDo list")
    args = parser.parse_args()
    tasks = ToDo()
    if args.add:
        tasks.add(args.add[0],args.add[1])
    elif args.delete:
        tasks.delete(args.delete[0])
    else:
        tasks.list()
```

Su modo de uso es:

```bash
$ python todo.py -h
usage: todo.py [-h] [-a ADD ADD] [-d DELETE]

optional arguments:
  -h, --help            show this help message and exit
  -a ADD ADD, --add ADD ADD
                        add a tast to the ToDo list
  -d DELETE, --delete DELETE
                        delete a task from the ToDo list
```

Para agregar una tarea escriba:

```bash
$ python todo.py -a "Completar Artículo" "atmantree: Breve Introducción a ZODB"
New task added..

$
```

Para ver las tareas pendientes:

```bash
$ python todo.py
Tasks To Do..
Completar Artículo      atmantree: Breve Introducción a ZODB
Comprar Pan, Jamón y Leche
Llamar al veterinario   Vacunas de Rahula

$
```

## ZODB como Base de Datos Orientada a Objetos

Ahora bien, como se puede sospechar utilizar una base de datos como ZODB
para un programa como el anterior puede ser considerado como matar
moscas con una bazuca. Sin embargo la potencia de ZODB está en su
capacidad de almacenar directamente en una base de datos cualquier
objeto o tipo de datos existente en Python. En particular almacenar
directamente objetos definidos por el programador.

El diseño de una aplicación es un tema complejo y los escenarios son muy
variados. Tal vez alguien quiera crear clases del tipo contenedoras, o
tal vez prefiera agregarlas a la raíz del sistema de persistencia (ZODB
en este caso) o simplemente manejarlo a través de una lista de objetos
de algún tipo, las decisiones de diseño dependerán del contexto y el
espacio de problema donde se inscriba la aplicación.

A efecto del ejemplo se modificará levemente el programa anterior,
convertirán las tareas en objetos de la clase Task y se almacenarán en
una lista.

```python
# -*- coding: utf-8 -*-

from ZODB import (DB, FileStorage)
from persistent import Persistent
import transaction
import argparse

class Task(Persistent):
    def __init__(self):
        self.name = ""
        self.description = ""

class ToDo:
    def __init__(self):
        self.store = FileStorage.FileStorage("ToDo2.fs")
        self.database = DB(self.store)
        self.connection = self.database.open()
        self.root = self.connection.root()
        if not 'Tasks' in self.root:
            self.root['Tasks'] = []
        self.tasks = self.root['Tasks']

    def __enter__(self):
        return self

    def __exit__(self, type, value, traceback):
        transaction.get()
        transaction.abort()
        self.connection.close()
        self.database.close()
        self.store.close()

    def add(self, name, description):
        if name != "":
            new_task = Task()
            new_task.name = name
            new_task.description = description
            self.tasks.append(new_task)
            self.root['Tasks'] = self.tasks
            transaction.commit()
            print("New task added..")
        else:
            print("Tasks must have a name")

    def list(self):
        if len(self.tasks) > 0:
            print("Tasks To Do..")
            for task in self.tasks:
                print("%s\t%s" %(task.name, task.description))
        else:
            print("No pending tasks..")

    def delete(self, name):
        for i in range(len(self.tasks)):
            deleted = False
            if self.tasks[i].name == name:
                del(self.tasks[i])
                deleted = True
            if deleted:
                self.root['Tasks'] = self.tasks
                transaction.commit()
                print("Task deleted..")
            else:
                print("There is no task '%s'.." % name)

if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument('-a', '--add', nargs=2, help="add a tast to the ToDo list")
    parser.add_argument('-d', '--delete', nargs=1, help="delete a task from the ToDo list")
    args = parser.parse_args()
    tasks = ToDo()
    if args.add:
        tasks.add(args.add[0],args.add[1])
    elif args.delete:
        tasks.delete(args.delete[0])
    else:
        tasks.list()
```

En general es el mismo programa, sin embargo las posibilidades aumentan
a partir de acá aprovechando los métodos y opciones que da la superclase
**Persistent**. En adelante lo que queda es invitarles a experimentar,
probar y utilizar ZODB.

## Otros temas sobre ZODB

### ZODB vs ORM

Los Mapeadores Objeto-Relacionales
([ORM](http://es.wikipedia.org/wiki/Mapeo_objeto-relacional)) suelen ser
una alternativa frecuente en esto de lidiar con objetos dentro de la
base de datos, sin embargo no siempre es un camino de rosas pues se
realizan algunas de concesiones de diseño en el proceso. Generalmente se
termina ajustando el diseño al uso del ORM, asumiendo en los costes
asociados al mapeo en el rendimiento de la aplicación. Al final es un
tema de contexto, decisiones de diseño y métricas de desempeño.

### Otros almacenes de ZODB

ZODB permite el uso de diversos tipos de almacenes de datos. Como vimos
en los ejemplos almacenamos los datos en un archivo, sin embargo esta
aproximación tiene la limitante que solo un proceso de Python puede
acceder a los datos. Es por ello que se creó una solución llamada
[ZEO](http://www.zodb.org/en/latest/documentation/guide/zeo.html) para
lidiar con este escenario, permitiendo escalar a una solución en la cual
muchas conexiones y procesos puedan acceder aun un punto de acceso a un
archivo de ZODB.

Otro almacén de datos es
[RelStorage](https://pypi.python.org/pypi/RelStorage), este permite
guardar dentro de una Base de Datos Relacional como PostgreSQL o MySQL
los objetos Python manejados por un programa. En tal sentido esta
solución aprovecha las capacidades de replicación de estos gestores de
bases de datos. Está diseñado para aplicaciones de alta demanda y en
algunas pruebas obtiene mejores resultados en escenarios de alta
concurrencia que la solución típica de ZODB + ZEO.

Tal vez desee utilizar una estructura de directorios para almacenar sus
objetos. Si ese es el caso puede utilizar
[DirectoryStorage](http://dirstorage.sourceforge.net/). Su simplicidad
en cuanto a mecanismo de almacenamiento garantiza que es una solución a
prueba de desastres. Tiene herramientas curiosas como manejo de
réplicas, firmas md5 de los distintos archivos, así como la posibilidad
de trabajar a modo de solo lectura o
[Snapshots](http://en.wikipedia.org/wiki/Snapshot_(computer_storage))
para mantener la consistencia de los datos originales en un momento
determinado del sistema.

Finalmente podemos utilizar ZODB de forma similar a SQLite en cuanto a
crear una base de datos en memoria, en tal sentido puede usar los
almacenes [DemoStorage y
MappingStorage](http://zodb.readthedocs.org/en/latest/api.html#in-memory-for-testing)
que le vendrán muy bien para tareas de pruebas o [migración de
datos](http://www.andreas-jung.com/contents/using-zodb-demostorage-for-migration-testing).

### Visores Gráficos de una Base de Datos

En general siempre se agradece la posibilidad de contar con una
herramienta gráfica que permita conocer los datos almacenados dentro de
un gestor de bases de datos. Sin embargo esta tarea puede ser un poco
críptica para personas habituadas a tratar con bases de datos
relacionales, pues no existen tablas, estructuras o lenguaje SQL que
aplicar. Se está en un espacio completamente lleno de Python. Al momento
de escribir este artículo probé [eye](https://github.com/davisagli/eye)
que me pareció sencillo y bueno para ver el contenido de un archivo, sin
embargo existen foros que recomiendan el uso de
[zodbbrowser](https://pypi.python.org/pypi/zodbbrowser) (basado en Zope
3).

Para usar eye escriba:

```bash
$ eye (suBDdeZODB).fs
serving on http://127.0.0.1:8080
```

Visite la dirección <http://127.0.0.1:8080/> y podrá detallar el
contenido de su base de datos:

![eye, Visualzador de ZODB](/images/zodb.png)

### Para Más Información

La documentación de ZODB en realidad es bastante simple, no tiene muchos
lugares oscuros por lo que una búsqueda en la web le podrá arrojar uno
que otro manual o tutorial adicional. Sin embargo con los siguientes
links podrá avanzar sin problemas:

- <http://www.zodb.org/>
- <http://zodb.readthedocs.org/en/latest/index.html>
- <http://es.slideshare.net/carlos.delaguardia/zodb-tips-and-tricks>
- <http://www.upfrontsystems.co.za/Members/roche/where-im-calling-from/zodb-benchmarks-revisited>

El código fuente de este artículo se encuentra en
[github](https://github.com/carlosgruiz-dev/post-introduccion-zodb).
