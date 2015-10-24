---
layout: post
title: "Rostopic GUI Extension, reporte de la propuesta."
date: 2015-10-22 15:00:00
author: Carolina Hernandez, Francisco Montoto
categories: private
---

##Introducción
En la actualidad, el framework ROS es una de las herramientas más usados para la programación de software para robots. Su creciente popularidad se debe a su gran poder y alcance, pero además a que es software de código abierto. Esta característica, además de servir para promover la utilización de ROS en la comunidad, invita a sus usuarios a participar en su desarrollo, contribuyendo con soluciones a problemas que pueden detectar mediante la experiencia y el uso en diversas situaciones.

Una de las funcionalidad más relevantes dentro de ROS es Rostopic. Ésta corresponde a un conjunto de herramientas de línea de comando, que permiten obtener información, monitorear y enviar mensajes a los tópicos disponibles.

##Problema
Ya que rostopic es una herramienta de línea de comandos, tiene dificultades inherentes, sobre todo para usuarios no acostumbrados a este medio de interacción. El tener que hacer múltiples llamadas para conocer los tópicos disponibles y poder interactuar con ellos, tener que leer el manual para saber las funcionalidades y como ejecutarlas son algunas de éstas dificultades.
El interactuar y monitorear los tópicos disponibles en ROS es poco intuitivo y lento.

##Solución
La solución que proponemos es una interfaz gráfica que permita al usuario ver exactamente lo que está pasando con los tópicos activos. Además de monitorear cada uno de los tópicos debe ser capaz de enviar información a través de éstos.

##Diseño de la solución

###Diseño general
El diseño de general de la solución es una interfaz gráfica escrita en python que haga todo el uso posible de rostopic para la comunicación con ROS:

![Arquitectura]({{site.baseurl}}/assets/reporte/architecture.png)

Al hacer uso de rostopic, que ya es una herramienta soportada por la comunidad disminuimos el código nuevo a soportar. Esperamos mantener al mínimo la comunicación con ROS que no hace uso de rostopic, representada en la figura con la flecha roja.

Uno de los objetivos de la herramienta es permitir interactuar con más de un tópico a la vez, por lo que permitirá la interacción con todos los tópicos que el usuario desee. Es por esto que se ha decidido tener una ventana con una lista de todos los tópicos disponibles y otra ventana para cada tópico con el que se esté interactuando.

###Diseño detallado
La ventana de principal constará de una barra superior con checkbox y/o botones que permitirán ciertas configuraciones y filtros. Luego la ventana se divide en dos, en la izquierda se desplegará la lista de tópicos disponibles y a la derecha información sobre el tópico que se seleccione, además desde aquí se lanzarán las ventanas para interactuar con el tópico. Una ventana para escuchar el topic (Echo) y otra para escribir en él (Publish). Las imágenes a continuación muestran un mockup de la ventana principal y las dos ventanas de interación.

![MainWindow]({{site.baseurl}}/assets/reporte/main_window.png)
![InteractionWindows]({{site.baseurl}}/assets/reporte/interaction_windows.png)



##Conclusión
