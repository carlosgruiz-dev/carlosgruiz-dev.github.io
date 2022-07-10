---
title: "Introducció a Pyramid"
date: 2013-08-20T08:18:00-04:00
lastmod: 2014-12-12T16:14:00-04:00
tags: [tutorial, python, pyramid, framework, sqlalchemy, spanish]
summary: En el mundo de los Frameworks de Python para aplicaciones en la web por años han resaltado algunos nombres Django, Pylons, CherryPy, TurboGears, Flask y Bottle entre otros. En medio de este conjunto de excelentes herramientas surge del proyecto Pylons el desarrollo llamado Pyramid.
---

Como es sabido, es posible escribir una aplicación web con Python sin
necesidad de un Framework, sin embargo estos han ganado popularidad pues
facilitan el trabajo a través de métodos y armazones que simplifican las
tareas más frecuentes. En el mundo de los Frameworks de Python para
aplicaciones en la web por años han resaltado algunos nombres:
[Django](https://www.djangoproject.com/),
[Pylons](http://www.pylonsproject.org/),
[CherryPy](http://www.cherrypy.org/),
[TurboGears](http://turbogears.org/), [Flask](http://flask.pocoo.org/) y
[Bottle](http://bottlepy.org/) entre otros, todos buenos, con sus
ventajas particulares para cada tipo de aplicación. En medio de este
conjunto de excelentes herramientas surge del proyecto Pylons el
desarrollo llamado
[Pyramid](http://www.pylonsproject.org/projects/pyramid/), que a mi
juicio es un sucesor con muy buenas perspectivas. Dejemos entonces la
conversación y comencemos a ver un poco de que trata este programa.

![image](/images/pyramid.biglogo.png)

## ¿Qué es Pyramid?

Pyramid es un framework ligero para desarrollo web hecho en Python, es
de uso general, así que no importa que tan grande o pequeña sea su
aplicación Pyramid puede ser su mejor solución. En su pagina web exponen
los principios de diseño en que se basa, vale la pena echarles un
vistazo:

- **Simplicidad**: con Pyramid usted *"paga lo que va a consumir"*,
  usted requerirá de un grupo de conceptos básicos y en adelante usted
  es libre de utilizar la tecnología de su preferencia para crear
  su aplicación.
- **Minimalismo**: Pyramid le proveerá de soluciones rápidas y de alta
  calidad para los aspectos esenciales de cualquier aplicación web moderna.
- **Documentación**: el aspecto anterior permite que la documentación de
  Pyramid pueda estar completamente actualizada y que no queden
  aspectos sin documentar. En tal sentido es un valor que no exista
  aspecto de Pyramid desactualizado.
- **Velocidad**: Pyramid está diseñado para mejorar el desempeño en
  tareas comunes como el uso de plantillas y en manejo de respuestas.
  Aunque el mantra de *"el hardware es barato"* parece ofrecer una
  solución rápida al desempeño, suele ser un penoso despertar cuando
  aparecen las evidentes limitaciones de este enfoque al conseguirse
  administrando un gran número de equipos.
- **Confiabilidad**: Para el equipo de desarrollo de Pyramid esta frase
  es un mantra: *"Si no ha sido probado, está roto"*. Cada lanzamiento
  de Pyramid ha sido 100% probado vía pruebas unitarias.
- **Apertura**: de forma similar a Python, Pyramid es distribuido con
  una [licencia abierta permisiva](http://www.pylonsproject.org/about/license).

Pasemos ahora a la acción.

## Calentando Motores

![image](/images/pyramid-tee-banner.png)

Lo primero que debemos hacer es instalar Pyramid, sin embargo
normalmente cuando trabajamos con Python procuramos utilizar un entorno
virtual antes que colocar los programas en nuestra instalación de
Python. Incluso muchas veces se mantiene así en ambientes compartidos
como los servicios de hosting comerciales.

### Creación de un Entorno Virtual

Aunque existen varios programas para el manejo de entornos virtuales,
nos concentraremos en el uso de uno de ellos. Su nombre es
[virtualenv](http://www.virtualenv.org/) (y en caso de querer
simplificar su trabajo puede usar
[virtualenvwrapper](http://virtualenvwrapper.readthedocs.org/)). Este
ambiente aislado permite instalar los programas python desde PYPI sin
necesidad de alterar la configuración de PC y dándole a usted la
capacidad de probar múltiples versiones de múltiples programas. Usar
virtualenv es realmente sencillo, para crear un entorno virtual escriba.

```bash
$ virtualenv --no-site-packages env
(env) $
```

Para activar su entorno virtual puede escribir:

```bash
$ source [/ruta/a/la/carpteta/]env/bin/activate
(env) $
```

y para desactivarlo:

```bash
(env) $ deactivate
$
```

Esta es una introducción rápida a virtualenv, si no lo ha usado
anteriormente es recomendable darse una visita a la página
[virtualenv.org](http://www.virtualenv.org/).

### Instalando Paquetes

Una vez instalado y activado el entorno virtual instalar pyramid es
sumamente sencillo, basta con escribir

```bash
(env) $ pip install pyramid
....
.... (chum chum chum) ...
....
Cleaning up...
(env) $
```

y si en el proceso no envió ningún mensaje de error puede entrar a
Python para probarlo.

```bash
>>> import pyramid
>>>
```

## Primera Aplicación de Prueba

¿Ansioso por comenzar? bueno entonces no esperemos más, dentro del
entorno virtual que acabas de iniciar crea un archivo llamado
`holapyramid.py` y copia el siguiente código fuente:

```python
from wsgiref.simple_server import make_server from pyramid.config
import Configurator from pyramid.response import Response

def hello_world(request):
    return Response('Hola Pyramid')

def main():
    config = Configurator()
    config.add_route('hello', '/')
    config.add_view(hello_world, route_name='hello')
    app = config.make_wsgi_app()
    return app

if __name__ == '__main__':
    app = main()
    server = make_server('0.0.0.0', 8080, app)
    print ('Iniciando servidor en http://localhost:8080')
    server.serve_forever()
```

(ejemplo adaptado de
[pyramid\_tutorials](https://github.com/Pylons/pyramid_tutorials))

El funcionamiento de este programa es bastante simple, incorporamos a
nuestro programa la función `make_server` del módulo `wsgiref`
además de los componentes `Configurator` y `Response` de Pyramid. Lo
siquiente que hacemos es declarar una función llamada `hello_world`
que toma una solicitud por argumento y devuelve el texto `Hola
Pyramid` como respuesta. Hasta allí todo muy sencillo.

Parte del corazón de Pyramid es el `Configurator` que permite
gestionar los aspectos que controlan la aplicación. En tal sentido en la
función `main` creamos un objeto `Configurator`, definimos una ruta
llamada `hello` y que apunta a la raíz del sitio web, y seguidamente
asignamos la función `hello_world` a modo de una vista llamable
([View Callable](http://docs.pylonsproject.org/projects/pyramid/en/1.4-branch/narr/views.html#view-callables))
a la ruta `hello`. Finalmente, a través del objeto `Configurator`
creamos una aplicación `wsgi` y la devolvemos como resultado de la
función.

La última parte del script se ejecuta cuando hacemos el llamado desde la
línea de comandos y es que entonces con la función `main()` creamos
una aplicación que enviamos a `wsgi` para publicar desde nuestro equipo
por el puerto `8080`. Enviamos un mensaje al usuario indicando la
dirección de la página, cuando seguidamente iniciamos el servidor `wsgi`
para recibir solicitudes.

## Otra Aplicación de Prueba

Pyramid permite simplificar el proceso de crear una aplicación mediante
el uso de un armazón (scaffold). Incluso podrá crear sus propios
esquemas que se adapten a su estilo y preferencias. Para efecto de este
ejemplo utilizaremos uno de los armazón de los que trae Pyramid por
defecto. Para ver los disponibles escriba en su terminal.

```bash
(env) $ pcreate -l
Available scaffolds:
alchemy: Pyramid SQLAlchemy project using url dispatch
starter: Pyramid starter project
zodb: Pyramid ZODB project using traversal
(env) $
```

las opciones son `alchemy` que crea un esquema que utiliza [SQL
Alchemy](http://www.sqlalchemy.org/) para gestionar la persistencia y un
despachador de direcciones URL, `starter` para un andamiaje simple y
finalmente `zodb` para gestionar la persistencia de datos con la base
de datos orientada a objetos [ZODB](http://www.zodb.org/) y resolución
de URL mediante
[transversal](http://docs.pylonsproject.org/projects/pyramid/en/latest/api/traversal.html).

### Crear Aplicación usando un Armazón (scaffold)

Para crear un armazón dentro de Pyramid tendrá que ejecutar el siguiente
comando:

```bash
(env) $ pcreate -s alchemy MyApp
....
.... (chum chum chum) ...
....
===================================================================
Tutorials: http://docs.pylonsproject.org/projects/pyramid_tutorials
Documentation: http://docs.pylonsproject.org/projects/pyramid

Twitter (tips & updates): http://twitter.com/pylons
Mailing List: http://groups.google.com/group/pylons-discuss

Welcome to Pyramid.  Sorry for the convenience.
===================================================================

(env) $
```

Ahora tendrá un sistema como resultado del comando ‘pcreate‘ el
andamiaje listo para su aplicación mediante esta estructura de archivos.

```bash
MyApp/
    myapp/
        scripts/
            __init__.py
            initializedb.py
        static/
            (....)
        templates/
            mytemplate.pt
        __init__.py
        models.py
        tests.py
        views.py
    CHANGES.txt
    MANIFEST.in
    README.txt
    development.ini
    production.ini
    setup.cfg
    setup.py
```

Esta estructura de directorios componen ahora su proyecto, el directorio
`MyApp` es su distribución de Python (tal y como los consigue en
[PyPI](https://pypi.python.org)), el directorio `myapp` contiene
nuestra aplicación web, con su código fuente y archivos estáticos.

El archivo setup.py puede ser usado para distribuir su aplicación, o
instalarla en su ambiente de producción, los archivos .ini se utilizan
para almacenar configuraciones. Dentro de la aplicación podrá notar que
se encuentran las carpetas `scripts`, `static` y `templates` que son
para colocar diálogos (generalmente para configuraciones), contenidos
estáticos y plantillas respectivamente. Finalmente los archivos
`__init__.py`, `models.py`, `test.py` y `view.py` se encargan de
definir un módulo de python, almacenar la información de los modelos en
SQL Alchemy, las pruebas del código y las vistas que se encargarán de
tramitar las solicitudes realizadas a la aplicación.

### Instalando la Aplicación

El siguiente paso que toca realizar es instalar la nuestra aplicación.
Para ello escribimos el siguiente comando:

```bash
(env) $ cd MyApp
(env) $ python setup.py develop
....
.... (chum chum chum) ...
....
Finished processing dependencies for MyApp==0.0
(env) $
```

Posteriormente inicializamos la base de datos mediante el comando:

```bash
(env) $ initialize_MyApp_db development.ini
....
.... (chum chum chum) ...
....
(env) $
```

### Probando el Armazón

Para probar nuestra aplicación escribamos el siguiente comando:

```bash
(env) $ pserve development.ini --reload
Starting subprocess with file monitor
Starting server in PID 16536.
serving on http://0.0.0.0:6543
```

Proceda a abrir su navegador en la dirección <http://localhost:6543/> y
podrá ver la aplicación por defecto que viene con el armazón `alchemy`
de Pyramid. A continuación se muestran unos pantallazos de la aplicación
de muestra junto con los datos que muestra la barra de depuración.

Note lo siguiente, como Pyramid publica por la dirección
<http://0.0.0.0:6543> otros equipos podrán acceder a su aplicación a
través de su dirección IP, sin embargo la barra de depuración sólo está
disponible para los usuarios locales.

![pyramid](/images/pyramid.gif)

## Modificando el Armazón

Ahora avancemos con los cambios para hacer nuestra aplicación, pero
primero comencemos por definir qué es lo que queremos que haga. Una de
las tareas más comunes es el llenado de formularios web, así que hagamos
un ejemplo con esto. Acá una salvedad, Pyramid es bastante extenso y tal
vez lo propuesto acá sea rudimentario en comparación a una solución del
mundo real, concretamente hablo del manejo de formulario, validaciones,
pruebas y control de usuarios (este último no se tomó en cuenta). Sin
embargo es un ejemplo para ilustrar el proceso básico de capturar una
información a través de una planilla y poder ver los resultados.

Acorde a esto el sitio web deberá tener la siguiente estructura:

  URL            Acción                                                                                                           Vista   Planitilla
  -------------- ---------------------------------------------------------------------------------------------------------------- ------- ------------
  /              Mostrar planilla de recolección de información.                                                                   home    home.pt
  /data          Desplegar la lista de planillas recibidas.                                                                        list    list.pt
  /data/numero   Mostrar la planilla con el id igual a `numero`. Si el registro `numero` no existe redirigir la página a `/data`.  show    show.pt
  -------------- ---------------------------------------------------------------------------------------------------------------- ------- ------------

A continuación, agregaremos dentro del archivo `myapp/__init__.py`
las rutas (urls) de nuestra aplicación:

```python
from pyramid.config import Configurator
from sqlalchemy import engine_from_config

from .models import (
     DBSession,
     Base,
)

def main(global_config, **settings):
    """ This function returns a Pyramid WSGI application.
    """
    engine = engine_from_config(settings, 'sqlalchemy.')
    DBSession.configure(bind=engine)
    Base.metadata.bind = engine
    config = Configurator(settings=settings)
    config.add_static_view('static', 'static', cache_max_age=3600)
    config.add_route('home', '/')           # para el inicio de la app
    config.add_route('list','/data')        # para visualizar el listado
    config.add_route('show','/data/{uid}')  # para ver el detalle
    config.scan()
    return config.make_wsgi_app()
```

Saltemos por un momento al modelo, la tabla que utilizaremos para
nuestra aplicación tendrá los siguientes campos; un identificador, un
título y el texto para cada título. Para ello modificaremos nuestro
archivo `myapp/models.py` para que coincida con el siguiente texto:

```python
from sqlalchemy import (
    Column,
    Integer,
    Text,
    Sequence,
)

from sqlalchemy.ext.declarative import declarative_base

from sqlalchemy.orm import (
    scoped_session,
    sessionmaker,
)

from zope.sqlalchemy import ZopeTransactionExtension

DBSession = scoped_session(sessionmaker(extension=ZopeTransactionExtension()))
Base = declarative_base()

class WebFormData(Base):
    __tablename__ = 'webformdata'
    id = Column(Integer, Sequence('webformdata_seq'), primary_key=True)
    title = Column(Text, unique=True)
    comment_text = Column(Text)

    def __init__(self, title, comment_text):
        self.title = title
        self.comment_text = comment_text
```

Para que sus cambios surtan efecto, modifique igualmente el archivo
`myapp/scripts/initializedb.py` con el siguiente contenido:

```python
import os
import sys
import transaction

from sqlalchemy import engine_from_config

from pyramid.paster import (
    get_appsettings,
    setup_logging,
)

from ..models import (
    DBSession,
    WebFormData,
    Base,
)

def usage(argv):
    cmd = os.path.basename(argv[0])
    print('usage: %s &amp;lt;config_uri&amp;gt;\n'
          '(example: "%s development.ini")' % (cmd, cmd))
    sys.exit(1)

def main(argv=sys.argv):
    if len(argv) != 2:
        usage(argv)
    config_uri = argv[1]
    setup_logging(config_uri)
    settings = get_appsettings(config_uri)
    engine = engine_from_config(settings, 'sqlalchemy.')
    DBSession.configure(bind=engine)
    Base.metadata.create_all(engine)
```

En este punto ejecute de nuevo `initialize\MyApp\db` como hizo
anteriormente actualizar su base de datos.

Pasemos ahora a trabajar con las plantillas. Para las plantillas haremos
uso de una de las bibliotecas de plantillas que nos propone inicialmente
Pyramid, llamada [Chameleon](http://chameleon.readthedocs.org/) (el otro
propuesto de entrada es [Mako](http://www.makotemplates.org/), sin
embargo usted es libre de seleccionar otro sistema de plantillas, como
[Jinja2](http://jinja.pocoo.org/) o
[Genshi](http://genshi.edgewall.org/), si lo desea). De la lista del
diseño se contemplan tres plantillas, que son a saber:

**home.pt**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Pyramid App</title>
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8"/>
  </head>
  <body>
    <h1>Tell me something...</h1>
    <form action="${save_form}" method="post">
       <input type="text" name="title"></input><br />
       <textarea name="comment_text"></textarea><br />
       <input type="submit" name="form.submitted" value="Send">
    </form>
        <br />
        <a href="${save_form}">other comments..</a>
  </body>
</html>
```

**list.pt**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Pyramid App</title>
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8"/>
  </head>
  <body>
    <h1>You have said..</h1>
    <ul>
      <tal:block repeat="item data">
      <li><a href="/data/${item.id}">${item.title}</a></li>
      </tal:block>
    </ul>
    <a href="/">home</a>
  </body>
</html>
```

y **show.pt**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Pyramid App</title>
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8"/>
  </head>
  <body>
    <h1>${comment.title}</h1>
    <hr />
    <p>${comment.comment_text}</p>
    <p><a href="/">home</a></p>
  </body>
</html>
```

Para finalizar completemos el código de nuestras vistas transcribiendo
lo siguiente:

```python
from pyramid.view import view_config
from pyramid.httpexceptions import HTTPFound    
from sqlalchemy.exc import DBAPIError

from .models import (
    DBSession,
    WebFormData,
)

@view_config(route_name='home', renderer='templates/home.pt')
def home(request):
    save_form = request.route_url('list')
    return {'save_form':save_form}

@view_config(route_name='list', renderer='templates/list.pt')
def list(request):
    if 'form.submitted' in request.params:
        title = request.params['title']
        comment_text = request.params['comment_text']
        comment = WebFormData(title, comment_text)
        DBSession.add(comment)
    data = DBSession.query(WebFormData).all()
    return {'data':data}

@view_config(route_name='show', renderer="templates/show.pt")
def show(request):
    uid = request.matchdict['uid']
    comment = DBSession.query(WebFormData).filter_by(id=uid).first()
    if comment is None:
        return HTTPFound(request.route_url('list'))
    return {'comment': comment}
```

Para completar inicie su aplicación y vea los cambios, si observa algún
error compare su código con el del repositorio en
[GitHub](https://github.com/carlosgruiz-dev/post-intro-pyramid) que acompaña
este artículo.

### Mi primera aplicación

Que hace nuestra aplicación, en pocas palabras, despachamos una
aplicación wsgi. Esta aplicación tiene su configuración en el archivo
`myapp/__init__.py` donde definimos el motor de base de datos
(línea 13) y las rutas (líneas 18 al 20). Con ayuda de [SQL
Alchemy](http://www.sqlalchemy.org/) (en el archivo `models.py`)
definimos un modelo llamado `WebFormData`, nótese que este modelo es
equivalente a la tabla `webformdata`. Al ejecutar el script
`initialize_MyApp_db` lo que sucede es que creamos en el gestor de
base datos (en el caso del parámetro development.ini es un archivo
[SQLite](http://sqlite.org/)) la tabla `webformdata`.

Seguidamente cuando el servidor web está en ejecución (en los ejemplo
con la instrucción `pserve`), al ingresar a la dirección
<http://localhost:6543/> la aplicación le mostrará la plantilla
correspondiente a la ruta `home`, si agrega un comentario le mostrará
a continuación el listado de los comentarios recibidos y finalmente al
hacer click en el vínculo asociado a alguno de los comentarios listados
verá el texto completo del comentario. A continuación unos pantallazos.

![pyramid app](/images/pyramid_app.gif)

Hay muchos detalles convenientes en el uso de Pyramid, en especial me ha
sido útil para dar representación web a proyectos generados en otros
contextos, la invitación es pues a explorar las alternativas que ofrece
a sus necesidades.

## ¿Donde continuar?

Existen abundantes y muy buenos recursos para aprender e implementar
Pyramid, sin embargo estos son algunos de los recursos a los cuales vale
la pena echarles un vistazo:

- Página del proyecto Pylons:
  [pylonsproject.org](http://www.pylonsproject.org/)
- Documentación de Pyramid:
  [docs.pylonsproject.org](http://docs.pylonsproject.org/en/latest/docs/pyramid.html)
- Presentación de Keith Yang “Use Pyramid Like a Pro”:
  [keitheis.github.io](http://keitheis.github.io/use-pyramid-like-a-pro/?full#Cover)
- Presentación de Daniel Nouri en el EuroPython 2012:
  [danielnouri.org](http://danielnouri.org/notes/2012/08/16/pyramid-europython-tutorial-video/)
  [github.com/dnouri](https://github.com/dnouri/pyramid-tutorial)
- Tutoriales de Pyramid:
  [github.com/Pylons/pyramid\_tutorials](https://github.com/Pylons/pyramid_tutorials)
- Comparativa de rendimiento con otros frameworks:
  <http://blog.curiasolutions.com/the-great-web-framework-shootout/>
