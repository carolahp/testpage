---
layout: post
title: "Rostopic GUI Extension, reporte de la propuesta."
date: 2015-10-22 15:00:00
author: Carolina Hernandez, Francisco Montoto
categories: private
---

###Introducción
Rostopic es un conjunto de herramientas de línea de comando disponibles en ROS. Permite obtener información, monitorear y enviar mensajes a los tópicos disponibles. Sin embargo el ser una herramienta de línea de comandos tiene dificultades inherentes sobre todo para usuarios no acostumbrados a la línea de comandos. El tener que hacer múltiples llamadas para conocer los tópicos disponibles y poder interactuar con ellos, tener que leer el manual para saber las funcionalidades y como ejecutarlas son algunas de éstas dificultades.

##Problema
El interactuar y monitorear los tópicos disponibles en ROS es poco intuitivo y lento.

##Solución
La solución que proponemos es una interfaz gráfica que permita al usuario ver exactamente lo que está pasando con los tópicos activos. Además de monitorear cada uno de los tópicos debe ser capaz de enviar información a través de éstos.

##Diseño de la solución
###Diseño general
El diseño de general de la solución es una interfaz gráfica escrita en python que haga todo el uso posible de rostopic para la comunicación con ROS:

![Arquitectura]({{site.baseurl}}/assets/reporte/architecture.png)

Al hacer uso de rostopic, que ya es una herramienta soportada por la comunidad disminuimos el código nuevo a soportar. Esperamos mantener al mínimo la comunicación con ROS que no hace uso de rostopic, representada en la figura con la flecha roja.



##Conclusión
