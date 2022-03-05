---
title: "\"Hola PostgreSQL\" (con Python)"
date: 2013-02-18T12:39:00-04:00
lastmod: 2015-03-07T16:24:00-04:00
tags: [tutorial, guides, postgresql, python, tubasededatoslibre, spanish]
---

Una de las tareas más frecuentes cuando iniciamos con las bases de datos
es cómo conectamos las mismas con nuestros programas. En particular
conectarse con PostgreSQL es una tarea bastante simple con Python. <!--more-->Como
sabrá en Python buena parte de los elementos del lenguaje se encuentran
en las [PEP](http://www.python.org/dev/peps/) (Python Enhancement
Proposals), y en cuanto a las bases de datos esto no es la excepción y
la [DB API 2.0](http://www.python.org/dev/peps/pep-0249/) se especifica
en la PEP-249, siga el vínculo para conocer los detalles. Una de las
consecuencias directas de esta normalización del lenguaje es que muy
probablemente lo que use para PostgreSQL con este tutorial sea válido
para otro gestor de base de datos relacional cuyo conector implemente
esta API.

## Instalando Psycopg2


Si utiliza Linux prefiera instalar la versión de psycopg2
correspondiente a su distribución, por ejemplo para
[Fedora](http://fedoraproject.org/) sería:

```bash
$ yum install python-psycopg2
```

y para [Debian](http://www.debian.org/) sería:

```bash
$ aptitude install python-psycopg2
```

Sin embargo, también puede hacer uso del instalador de Python llamado
[pip](http://www.pip-installer.org/en/latest/). Este instalador es muy
potente, pero debido a que psycopg2 necesitará compilar unos fuentes
durante la instalación asegúrese que su computador tenga instaladas las
bibliotecas de desarrollo de PostgreSQL y obviamente un compilador. Si
todo está bien y tiene los permisos adecuados, bastará escribir en su
terminal:

```bash
$ pip install psycopg2
```

Si utiliza Windows descargue la versión correspondiente para la versión
de su Sistema Operativo, su Python y de su PostgreSQL en la página de
[win-psycopg](http://www.stickpeople.com/projects/python/win-psycopg/).

## Conectando Python con PostgreSQL

Si todo fue bien con la instalación entonces será sencillo comunicarse
con PostgreSQL. Para probar la instalación y la conexión con su gestor
de base de datos escriba lo que sigue en su terminal:

```bash
$ python
Python 2.7.3 (default, Jan 2 2013, 16:53:07)
[GCC 4.7.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import psycopg2
>>> exit()
$
```

En caso de no haber ningun mensaje de error entonces ha instalado
correctamente psycopg2. El siguiente paso será conectar con su base de
datos, para ello crearemos una base de datos para pruebas.

```bash
$ su - postgres
$ createdb prueba
$ exit
```

y luego procedemos a conectar con PostgreSQL desde Python:

```bash
$ python
Python 2.7.3 (default, Jan 2 2013, 16:53:07)
[GCC 4.7.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import psycopg2
>>> conexion = psycopg2.connect("dbname=prueba user=postgres")
>>> conexion.close()
>>>
```

Recuerde hacer de su string de conexión (o dsn) adecuado para su
configuración: los parámetros de conexión aceptados son: `dbname`,
`user`, `password`, `host` y `port`, para más detalles ver:
[psycopg2.connect](http://pythonhosted.org/psycopg2/module.html#psycopg2.connect).
En caso de recibir algún error, verifique con su cliente PostgreSQL que
la configuración que utilizó para Python esté correcta.

## Conversando con PostgreSQL al estilo Python

Dado por sentado que no tuvo problemas de conexión entonces retomamos la
sesión interactiva y pasaremos a crear una tabla y llenarla con datos,
de modo de mostrar cómo se envían instrucciones mediante la DB API 2.0
de Python al gestor de base de datos:

```python
>>> conexion = psycopg2.connect("dbname=prueba user=postgres") # se crea la conexión
>>> cursor = conexion.cursor() # se crea un cursor
>>> query1 = """CREATE TABLE la_vinotinto (id serial primary key, goles integer,
                    nombres varchar(100), apellidos varchar(100));""" # consulta para crear la tabla
>>> cursor.execute(query1)
>>> query2 = "INSERT INTO la_vinotinto(goles, nombres, apellidos) VALUES (%, %, %)"
>>> cursor.execute(query2, (22, "Giancarlo", "Maldonado"))
>>> cursor.execute(query2, (21, "Juan", "Arango"))
>>> cursor.execute(query2, (14, "Ruberth", "Moran"))
>>> cursor.execute(query2, (11, "Jose Manuel", "Rey"))
```

Ahora vamos a preguntarle algunas cosas a nuestra tabla de goleadores de
la vinotinto:

```python
>>> query3 = "SELECT * FROM la_vinotinto"
>>> cursor.execute(query3)
>>> cursor.fetchone()
(1, 22, "Giancarlo", "Maldonado")
>>> query4 = "SELECT apellidos, nombre FROM la_vinotinto ORDER BY goles;"
>>> cursor.execute(query4)
>>> resultados = cursor.fetchall()
>>> for i in resultados:
...    print i
...
('Rey', 'Jose Manuel')
('Moran', 'Ruberth')
('Arango', 'Juan')
('Maldonado', 'Giancarlo')
>>>
```

Finalmente con Python debe dejar claro a PostgreSQL que la comunicación
se ha terminado, por lo que es necesario cerrar le cursor y la conexión.
Es importante este paso, así liberará recursos en su programa y
permitirá al gestor de bases de datos liberar la conexión dedicada al
programa y usarla para otro usuario.

```python
>>> 
>>> cursor.close()
>>> conexion.close()
```

## Pequeño Script de Python con PostgreSQL

Ahora vamos a escribir un pequeño programa con lo aprendido en el
diálogo anterior, copie el siguiente programa en un archivo llamado
`hola_postgres.py`:

```python
#/usr/bin/env python
# -*- coding: utf-8 -*-

import psycopg2
DSN = "dbname=prueba user=postgres"

def leer_datos():
    con = psycopg2.connect(DSN)
    cur = con.cursor()
    query = "SELECT * FROM la_vinotinto;"
    cur.execute(query)
    for jugador in cur.fetchall():
        print(jugador)
    cur.close()
    con.close()

if __name__== "__main__":
   leer_datos();
```

El programa realiza en la función leer\_datos() un despliegue de los
jugadores almacenados en la tabla la\_vinotinto, en si no reviste de
mucha complejidad. Finalmente para ejecutar el programa escriba en su
terminal:

```bash
$ python hola_postgres.py
(1, 22, 'Maldonado', 'Giancarlo')
(2, 21, 'Arango', 'Juan')
(3, 14,'Moran', 'Ruberth')
(4, 11'Rey', 'Jose Manuel')
$
```

## Recomendado leer

Obviamente esto es un pequeño abreboca, para profundizar un poco más en
las posibilidades que ofrecen estas herramientas es necesario leer un
poco más. Sugiero como lecturas complementarias las siguientes páginas.

- [PEP-249](http://www.python.org/dev/peps/pep-0249/)
- [Documentación de Psycopg2](http://pythonhosted.org/psycopg2/)
- [Documentación de PostgreSQL](http://www.postgresql.org/docs/)
- [Documentación de pip](http://www.pip-installer.org/)

