---
title: "Migraciones a Software Libre (Parte 1)"
date: 2013-04-16T15:03:33-04:00
lastmod: 2013-04-16T15:03:33-04:00
tags: [collaborations, migration, tubasededatoslibre, spanish]
summary: Este grupo de artículos no pretende ser una guía exhaustiva de cómo hacer una migración a software libre, sin embargo es una serie de recomendaciones basadas en la experiencia como técnico y consultor.
---

Este grupo de artículos no pretende ser una guía exhaustiva de cómo
hacer una migración a software libre, sin embargo es una serie de
recomendaciones basadas en la experiencia como técnico y consultor.
Adicionalmente cualquier aporte será bienvenido y apreciado.

# Antecedentes

![Antecedentes](/images/Alleppey_-_Kollam_6847451428.jpg)

En Venezuela ha habido por muchos años una inquietud creciente por el
uso de las tecnologías libres. Algunos inicialmente lo vimos como el
retorno triunfal de UNIX adaptado para PC, pero luego de un rato metido
de cabeza con Linux al menos yo comprendí que el tema de la libertad del
software tiene un peso fundamental en este éxito. Linux había aterrizado
en mi país, ya un banco lo había usado para una implantación de su
internet banking y [SUSE Linux](http://es.wikipedia.org/wiki/SUSE_Linux)
dominaba el mercado nacional y el [Red Hat
Linux](http://es.wikipedia.org/wiki/Red_Hat_Linux) 6.0 se había
convertido en la marca favorita de los hackers. Poco a poco las
Tecnologías de Información demostraron su primacía en el desarrollo de
los acontecimientos del país, y muy en particular, luego de que se viese
comprometida su principal industria (petróleo), debido en parte, a una
cadena de errores en el manejo de la gerencia de las TI y de la
información sensible para los procesos y funcionamiento de la misma.
Bien sea como reacción o como producto de la maduración de las
iniciativas libres previas surge lo que sería el terreno fértil para la
sorpresa del día como regalo de navidad. El [Libro Amarillo del Software
Libre](https://atmantree.keybase.pub/page/extras/Libro_Amarillo_del_Software_Libre._Uso_y_Desarrollo_en_la_Administracion_Publica.pdf)
y el [Decreto Precidencial Nº
3.390](https://atmantree.keybase.pub/page/extras/decreto3390.pdf)
son los referentes de esas épocas. En fin esa es la historia y desde
entonces ha habido una avalancha de migraciones pequeñas, medianas y
grandes, exitosas y otras no tanto.

## Leyes de Newton en una Migración

![bombillo](/images/Glühlampe_explodiert.jpg)

A veces es complicado explicar todo esto de la migración a software
libre mediante esquemas y recuadros. Es más sencillo tal vez recurrir a
cosas conocidas como las Leyes de Newton, que todos vemos en
bachillerato y que pertenecen a nuestra comunicación diaria, incluso a
veces sin saberlo.

El cambio para muchos es un problema, pues en general, las
organizaciones suelen generar una inercia que actúa exactamente igual
que la [Primera ley de
Newton](http://es.wikipedia.org/wiki/Leyes_de_Newton#Primera_ley_de_Newton_o_Ley_de_la_inercia),
parafraseando a Newton podemos decir que **una organización en reposo o
en movimiento uniforme y rectilíneo (sin cambio), preserva su estado a
menos que sea obligado a cambiar mediante una fuerza que actúe sobre
ella**. Esto significa en otras palabras que las migraciones no se hacen
solas, una organización que cambia responde a una necesidad práctica
(que puede estar o no asociada a costos) o una obligación legal
generalmente producto de un marco jurídico distinto, y la conducción de
dicho cambio. Esto último debe llevarlo a cabo alguien con la visión
clara además de contar con la energía, el compromiso y la autoridad
suficiente cumplir con los objetivos planteados. Esos son los motores
que impulsan la fuerza que puede cambiar la inercia de una organización
y conducirla en un cambio cultural a nivel de Tecnologías de Información
a Tecnologías Libres.

Así mismo, parafraseando esta vez la [Segunda ley de
Newton](http://es.wikipedia.org/wiki/Leyes_de_Newton#Segunda_ley_de_Newton_o_Ley_de_fuerza),
podemos decir que **el cambio observado en una organización es
proporcional a la fuerza aplicada y el cambió irá en el sentido de la
fuerza que se imprima**. Es por ello que podemos inferir muchas veces que
los resultados pobres en una migración a software libre se deben, bajo
la premisa de que el marco jurídico es el mismo para todos, a causa de
problemas relacionados con:

-   **el liderazgo**: muchas veces los planes de migración se ven
    truncados por un liderazgo ineficiente, falto de autoridad o
    simplemente inexistente. Por ello es necesario que el liderazgo del
    cambio se lleve a cabo desde dos áreas principales: la dirección de
    la organización (Presidencia, Dirección, etc) y la dirección técnica
    de la organización (Oficina, Departamento o Coordinación de TIC o su
    equivalente), pero apoyado y apalancado por las unidades que dirigen
    el valor de la organización. Es natural que el liderazgo relacionado
    con la migración a software libre compita con otros liderazgos e
    intereses dentro de la organización. Es común que la ingenuidad de
    algunos entusiastas de las TIL choque con el muro de estas
    realidades y les genera frustración, sin embargo saber reconocer
    estos liderazgos en pugna permite establecer la estrategia más
    adecuada para cada caso y sortear estas dificultades. Hay que
    recordar que los liderazgos en pugna modifican de hecho la dirección
    que lleve la organización, tanto en lo técnico como en los
    rendimientos respecto a otros objetivos.
-   **la visión**: una de las dudas que surge a la hora de migrar a
    software libre es qué se espera de la misma. Obviamente el sustituir
    una suite ofimática no reviste mayor dificultad, de hecho es una
    tarea bastante simple. Sin embargo aquellas aplicaciones que no
    técnico-operativas sino especializadas o inmersas dentro del flujo
    de trabajo de valor de la organización es otra historia. Por lo
    tanto la visión de la organización postmigración es un elemento
    central pues una migración completa a software libre reviste también
    una revisión de los procedimientos y adecuación del "Saber Como" de
    la organización. Es oportuno plantear la migración como el momento
    idóneo para hacer cambios que aumenten la productividad, la
    eficiencia y la renovación de la cultura organizacional hacia
    modelos más adecuados con los nuevos tiempos.
-   **el compromiso**: otros de los sospechosos habituales cuando un
    proceso de migración presenta fallas es la falta de compromiso con
    el proceso de cambio. Usualmente evidencia problemas en la dirección
    y gerencia de las instituciones, lo que constituye sin duda un
    llamado a la revisión interna. Una organización con personal poco
    motivado o con empleados poco identificados con los fines de la
    misma presentan un gran reto para la migración. Realizar un cambio
    sobre algo que no es un tema de nuestro interés es simplemente una
    causa de tedio constante, poca dedicación y finalmente abandono. Una
    de las estrategias para generar compromiso con el proceso de
    migración es forme parte de los objetivos operativos de los
    trabajadores, debe explotar su motivación mediante ventanas de
    oportunidad para hacer de esta eventualidad un motivo para aumentar
    la cohesión de la organización. Sin embargo es importante señalar
    que muchas veces se confunde la retorica y perorata con la
    motivación real de los trabajadores. Por ejemplo, de nada sirve
    seminarios y talleres si lo que requieren los trabajadores son
    soluciones que les facilite su trabajo o cursos de formación en las
    nuevas tecnologías.
-   **la estructura de la organización**: Lamentablemente no son pocas las
    organizaciones que parecen diseñadas por un sastre con la intensión
    de fallar. En general se ha construido la organización de muchas
    instituciones y en particular las públicas respondiendo más a un
    software que a su finalidad. Es vez de adaptar la herramienta a la
    tarea, adaptamos las tareas a la herramienta. Es así como las
    organizaciones se han **\[Nombre una Marca\]**-tizado con el
    agravante de conocer de forma limitada la herramienta, lo que
    conlleva en algunos casos a que no se implementen soluciones óptimas
    por desconocimiento, incompetencia o simplemente debido a que la
    institución está atada a los planes de negocios de los revendedores
    de software. Esto es grave a la hora de planificar una migración a
    sistemas libres, pues en pocas palabras, requerirá una reingeniería
    de sus procesos.
-   **las capacidades técnicas**: una debilidad de muchas organizaciones
    es no poder "retener" el tiempo suficiente al personal
    técnicamente capacitado. No es un problema local pues incluso
    Silicon Valley tienen este inconveniente, pues buena parte de los
    técnicos especializados no se comportan como un empleado común sino
    como un personal flexible, trasladable y que además de un buen
    ingreso toma en cuenta si el trabajo le resulta estimulante. A esto
    hay que sumarle el déficit generalizado de informáticos a nivel
    mundial por lo que sus opciones serán más diversas que las de un
    abogado, por nombrar otra profesión. No pocas veces se forma un
    personal dentro de la organización y cosecha los beneficios otras
    instituciones e incluso el campo laboral internacional. Es por ello
    que el conocimiento que se requiere dentro de la organización para
    realizar la migración muchas veces queda fragmentado e incompleto
    pues durante el proceso pudo haber sucedido una fuga de los talentos
    internos, que son los llamados al final del día a operar y mantener
    los nuevos sistemas. Otras veces el problema de las capacidades
    técnicas es distinto, es el caso en que el personal actual no tiene
    las competencias necesarias por lo que puede actuar como resistencia
    a la migración y en el mejor de los casos requerirá solamente de
    formación en las nuevas tecnologías para poderlas comprender
    y aplicarlas.

Finalmente la [Tercera ley de
Newton](http://es.wikipedia.org/wiki/Leyes_de_Newton#Tercera_ley_de_Newton_o_Ley_de_acci.C3.B3n_y_reacci.C3.B3n)
nos abre el camino lo que puede ser una premisa para establecer las
estrategias a emplear en la migración a software libre. También conocida
como la Ley de Acción y Reacción, podemos asociarla a la respuesta que
se obtiene de las fuerzas ejercidas dentro de la organización.
Parafraseando nuevamente las leyes físicas vemos que **toda fuerza que se
aplique sobre la organización generará una reacción equivalente con la
misma magnitud en sentido contrario**. En otras palabras esta ley nos
pone de manifiesto por un lado la resistencia al cambio dentro de las
organizaciones. La resistencia al cambio es necesario administrarla y
convertir ese impulso en algo positivo.

## Direccionalidad del Cambio

He tenido varias veces la discusión de en qué sentido debe ir la
migración a software libre. Hay quienes argumentan que debe ser una
orden presidencial (de la presidencia de la República para ser más
precisos) y como contraparte en un mundo de blanco y negro hay quienes
promulgan que el cambio debe venir de la gente, desde la comunidad. En
mi opinión si lo ves en blanco y negro estás mal, muy mal. Tomando en
cuenta lo observado hasta ahora, es razonable estimar que en mejor de
los casos de cada conjunto de ordenes presidenciales solo se
instrumenten alrededor de un 30-40% lo que nos deja un buen chance a que
una normativa que venga en ese sentido caiga en el 60-70% que se
convierte en sal y agua.

Por otro lado las comunidades de software no es un cuerpo colegiado,
cohesionado y consistente, nada más lejos de eso. Incluso es fácil ver,
a través de las listas de correos, que abundan sectarismos muy marcados
e incluso una suerte de competencia de personalismos y afanes de
protagonismos. No ahondaré en detalles de la farándula del software
libre, cualquier cosa que se diga en este punto es candidato a un
"flame". Esta característica impide que la comunidad como cuerpo pueda
conducir iniciativas más allá de objetivos muy específicos, como
desarrollo de una distro de linux, una adaptación de un programa a la
legislación o gustos nacionales, en algunos casos incluso programas y
sistemas. En lo anterior no se incluyen las iniciativas llevadas a cabo
por encargo, pues esto no hace comunidades, son proyectos que
generalmente pierden su continuidad cuando desaparece el patrocinante
público o privado.

El cambio debe venir, en mi opinión de un apoyo concertado desde las
iniciativas gubernamentales con los intereses legítimos de las
comunidades de conocimiento. Ello asegura mantener el interés de un
grupo de técnicos especializados interesados en un tema en particular,
que con el apoyo adecuado pueden rendir buenos frutos para el resto de
la sociedad apoyándose en las iniciativas de los entes públicos. Un tema
especialmente delicado es cuando el Estado prioriza los temas de interés
para el desarrollo nacional, pues generalmente la comunidad llega
después que las empresas han explotado parte del nicho de negocio y no
pocas veces erosionando el terreno para iniciativas más sanas para el
país. Es prioridad entonces que desde el Estado exista una claridad en
cuanto a la relevancia de la figura de la comunidad puesto que las
contrataciones vienen y van al ritmo de la disponibilidad
presupuestaria, pero solamente con gente del lugar, con intereses
nacionales legítimos, con competencias probadas en la práctica, es
posible construir un cambio efectivo más allá de las vicisitudes
económicas.

**(Fin de la parte 1)**

Próximamente en la parte 2:

-   Etapas de la Migración a Software Libre
-   Tipos de Migración
-   Estratégias de Migración

(**nota**: Artículo publicado originalmente en [TuBaseDeDatosLibre.org](http://tubasededatoslibre.org))
