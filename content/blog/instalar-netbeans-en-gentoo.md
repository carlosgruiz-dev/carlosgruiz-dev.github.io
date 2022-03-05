---
title: "Instalar Netbeans en Gentoo"
date: 2014-02-02T21:41:00-04:00
lastmod: 2014-02-02T21:41:00-04:00
tags: [guides, gentoo, ide, spanish]
---

Esta entrada es una bitácora para mi instalación de Gentoo Linux, así
que a lo que voy. Mi requerimiento era de una IDE que me ayudase a
trabajar más cómodamente con unas tareas con PHP. Luego de buscar un
poco decidí aprovechar las bondades de NetBeans y no solo tener un IDE
para PHP sino poder usarlo con C/C++, Ruby y veremos que tal con la
programación visual de la web.

<!--more-->

Al hacer emerge a NetBeans trae por defecto soporte para java, sin
embargo si desea agregarle más funcionalidades deberá ver módulos en la
variable "netbeans\_modules", para una lista completa vea el archivo
`/usr/portage/profiles/desc/netbeans_modules.desc`.

```bash
# Copyright 2008 Gentoo Foundation.
# Distributed under the terms of the GNU General Public License v2
# $Header: /var/cvsroot/gentoo-x86/profiles/desc/netbeans_modules.desc,v 1.5 2013/10/16 09:36:55 fordfrog Exp $

# This file contains descriptions of NETBEANS_MODULES USE_EXPAND flags.

apisupport - enables apisupport module
cnd - enables C/C++ development support
dlight - enables framework for creation of Observability Tools using DTrace
enterprise - enables enterprise development support
ergonomics - enables ergonomics features
extide - enables extide module
groovy - enables Groovy and Grails development support
gsf - enables support for web client development
harness - enables harness support
ide - enables Netbeans IDE
identity - enables identity module
j2ee - enables J2EE development support
java - enables Java development support
javacard - enables cluster for JavaCard development
javafx - enables JavaFX development support
mobility - enables support for development of mobile applications
nb - enables Netbeans branding
php - enables PHP development support
profiler - enables Java profiler
ruby - enables Ruby development support
soa - enables SOA development support
visualweb - enables visual web development support
webcommon - enables javascript libraries and web client tools
websvccommon - enables common support for web services development
xml - enables XML related development support (schema, validation, WSDL, etc.)
```

Tenga en cuenta que deberá incluir siempre el módulo nb si quiere una
versión funcional de la IDE. Agregue a su archivo
`/etc/portage/make.conf` la línea con la lista de sus módulos
seleccionados:

```bash
NETBEANS_MODULES="nb cnd php ..."
```

o en el caso de querer seleccionarlos todos usar:

```bash
NETBEANS_MODULES="*"
```

Ajuste las dependencias generadas y proceda a instalar. Luego de aceptar
las licencias correspondientes estará listo para usar NetBeans.

![image](/images/netbeans.png)
