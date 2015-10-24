---
layout: post
title: "Rostopic GUI Extension, reporte de la propuesta."
date: 2015-10-22 15:00:00
author: Carolina Hernandez, Francisco Montoto
categories: private
---

##Introducción
En la actualidad, el framework ROS es una de las herramientas más usadas para la programación de software para robots. Su creciente popularidad se debe a su gran poder y alcance, pero además, a que es software de código abierto. Esta característica, además de servir para promover la utilización de ROS en la comunidad, invita a sus usuarios a participar en su desarrollo, contribuyendo con soluciones a problemas que pueden detectar mediante la experiencia y el uso en diversas situaciones.

Una de las herramientas más relevantes dentro de ROS es Rostopic. Ésta corresponde a un conjunto de funcionalidades ejecutadas por línea de comando, que permiten obtener información, monitorear y enviar mensajes a los tópicos disponibles.

##Problema
Ya que rostopic es una herramienta de línea de comandos, tiene dificultades de usabilidad inherentes, sobre todo para usuarios no acostumbrados a este medio de interacción. El tener que hacer múltiples llamadas para conocer los tópicos disponibles y poder interactuar con ellos, tener que leer el manual para conocer las funcionalidades y cómo ejecutarlas, son algunos de estos problemas.

Dos problemas específicos se derivan de lo anterior:

- El comando sub (destinado para publicar mensajes en un tópico definido) es muy verboso debido a que los tipos de mensajes relacionados a un tópico, pueden ser complejos. Esto produce un gran riesgo de cometer un error al tipear el comando en el terminal. Además, en caso de error, la retroalimentación de rostopic no es clara, llevando al usuario a perder tiempo detectando el origen de comportamientos inesperados.

- No es posible tener una visión global del uso de los tópicos y del flujo de mensajes a través de éstos. Ya que para obtener información sobre distintos tópicos, es necesario hacer varias llamadas a funciones de rostopic, a veces inclusive en distintos terminales, lo cual entorpece el proceso de entendimiento del panorama global.

Por todo lo ya mencionado, interactuar y monitorear los tópicos disponibles en ROS es poco intuitivo, dificultoso y lento.

##Solución
Para solucionar la problemática presentada hace falta una manera de acercar al usuario las funcionalidades que brinda Rostopic, haciéndolas más usables, intuitivas y rápidas, y proveyendo mecanismos que presenten la información extraída por Rostopic de manera más legible e interactiva.

La solución propuesta consiste en una interfaz gráfica que permita al usuario ver exactamente lo que está pasando con los tópicos activos y que, además de monitorearlos, sea capaz de asistir al usuario en el envío de mensajes a través de éstos.

En específico, se proveerán las siguientes funcionalidades:

- Un listado de los tópicos activos, el cual podrá ser filtrado según tenga publicadores y/o suscriptores asociados. Se espera que esta lista se actualice en tiempo real y que especifique la tasa a la que se está publicando en cada tópico desplegado.

- Una vista detallada de la información de cada tópico, en la que la información será presentada modularmente, y se desplegará según instrucciones del usuario. En particular se mostrarán detalles sobre: publicadores, suscriptores y tipo de mensajes.

- Una interfaz para publicar mensajes sobre un tópico específico. Esta interfaz deberá adaptarse al tipo de mensaje asociado al tópico, presentando campos independientes para cada componente del mensaje, y deberá validar la información ingresada en cada campo por el usuario.

- Una interfaz para visualizar (echo) los mensajes transmitidos a través de un tópico particular. Esta interfaz incluirá un mecanismo para navegar sobre los mensajes ordenados según momento de publicación. Se proveerá de este modo un método para visualizar la evolución de los mensajes publicados sobre un tópico.

- Gráficos sobre la evolución de la tasa de transmisión de mensajes para cada tópico. Suministrando así una herramienta visual para extraer información global sobre el uso de los tópicos.

##Diseño de la solución

###Diseño general
El diseño de la arquitectura de software de la solución propuesta considera maximizar la reutilización de código desde la clase rostopic. Se tiene esta consideración en parte porque al hacer uso de rostopic, que ya es una herramienta soportada por la comunidad, se disminuye el código nuevo a soportar. Esperamos mantener al mínimo la comunicación directa con ROS sin pasar por funciones de rostopic. Esta forma de comunicación es representada en la Figura 1 mediante una flecha roja.

![Arquitectura]({{site.baseurl}}/assets/reporte/architecture.png)
Figura 1: Arquitectura

El diseño de general de la solución contempla la creación de una interfaz gráfica escrita en python, que sirva de medio exclusivo de comunicación con el usuario, y que posibilite la comunicación con ROS principalmente reutilizando funciones de rostopic.

Uno de los objetivos de la herramienta es permitir interactuar con más de un tópico a la vez, por lo que permitirá la interacción con todos los tópicos que el usuario desee. Es por esto que se ha decidido implementar una ventana principal con una lista de todos los tópicos disponibles y una ventana adicional para cada tópico con el que se esté interactuando.

###Diseño detallado

El detalle de la arquitectura se especifica a continuación en el diagrama de la Figura 2. En éste se observan 3 grandes módulos:
- Roscore (verde): Contiene todo lo relacionado con roscore (núcleo de ROS), en particular la clase Rostopic.
- Rostopic GUI Extension (azul): Contiene todas las clases que deberán ser implementadas para concretar la solución descrita en el presente reporte.
- External módules (rojo): Contiene las librerías externas que se usarán como apoyo para la implementación

Las flechas representan flujo de información sobre los tópicos, mientras que las líneas punteadas indican interacción entre las clases.

![Arquitectura]({{site.baseurl}}/assets/reporte/design.png "Figura 2: Arquitectura")

Dentro del módulo Rostopic GUI Extension, se encuentran tres módulos principales:
- graphic interface: que implementa el front end de la aplicación.
- topics manager: implementa la lógica de la aplicación. Provee funcionalidad a graphic interface. Interactúa además con plotter para implementar gráficos.
- plotter: contiene la lógica para crear gráficos. Interactúa con topics manager.

Con respecto al diseño de las interfaces gráficas, se especifica lo siguiente:

La ventana de principal constará de una barra superior de opciones, con checkboxes y/o botones que permitirán configurar y filtrar la lista de tópicos según publicadores y suscriptores asociados. El resto de la ventana se dividirá en dos, en la sección izquierda se desplegará la lista de tópicos disponibles y en la derecha, información sobre el tópico que se seleccione. Además desde aquí se lanzarán las ventanas para interactuar con el tópico: Una de ellas servirá para escuchar el topic (Echo) y otra para escribir en él (Publish). Las imágenes a continuación muestran un mockup de la ventana principal y las dos ventanas de interación.

![MainWindow]({{site.baseurl}}/assets/reporte/main_window.png)
![InteractionWindows]({{site.baseurl}}/assets/reporte/interaction_windows.png)

<a href="{{site.baseurl}}/assets/reporte/interaction_windows.png" data-lightbox="interaction-large" data-title="Interaction Windows">
	<img src="{{site.baseurl}}/assets/reporte/interaction_windows/png" title="Interaction Windows">
</a>
![InteractionWindows]({{site.baseurl}}/assets/reporte/interaction_windows.png)

##Conclusión

La propuesta descrita solucionaría el problema planteado, haciendo más fácil y sencillo el monitoreo y la interacción con los tópicos. Por lo que de ser implementada se cumpliría el objetivo.

El plazo es acotado por el semestre, al cual le quedan 7 semanas, y la solución es ambiciosa, sin embargo confiamos en que para la fecha de entrega contemos con un software funcional y que agregue valor al ecosistema de desarrollo en ROS. Para esto se establece como mínimo deseable para el fin del semestre lo siguiente:

-La vista principal funcionando con al menos la lista de tópicos.

-La vista de echo permitiendo ver el último mensaje enviado por el topic.

-La vista de publish funcionando y permitiendo enviar mensajes.

Se considera que la funcionalidad descrita como mínima es un avance con respecto a lo que existe hoy y que cumple con el objetivo de mejorar el ecosistema de desarrollo en ROS.
