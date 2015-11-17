---
layout: post
title:  "Reporte de avances N°1"
date:   2015-11-16 12:00:00
author: Carolina Hernandez, Francisco Montoto
categories: rostopic GUI progress project web
---

#Resumen sobre la evolución del proyecto y su enfoque definitivo
Luego de arduas discusiones sobre el camino que debía tomar el proyecto, se decidió cambiar su enfoque( con un poco de suerte por última vez). Tal como se especificó en el ![reporte de la propuesta definitivo]({{site.baseurl}}/_posts/2015-11-02-reporte-de-la-propuesta2.md), finalmente el proyecto atacará el problema del desplazamiento en el espacio del implementador al ejecutar programas usando ROS en un robot móvil. Cuando uno se encuentra testeando la ejecución en un robot que se mueve, tiene básicamente dos opciones para seguir los mensajes y tópicos que se están ejecutando: si el robot cuenta con un monitor uno puede seguir la secuencia desde el mismo robot; de lo contrario, o como otra opción, se puede seguir la ejecución desde otro computador, usualmente el que controla el robot, perdiendo la oportunidad de observar adecuadamente el comportamiento del robot.

El proyecto pretende agregar una tercera opción para observar en tiempo real los mensajes que circulan en el robot, busca ofrecer una interfaz web con un diseño amigable, especialmente orientada a dispositivos móviles, que permita seguir los mensajes, tópicos y nodos del robot incluso desde un teléfono celular u otro dispositivo móvil.

#Avances logrados durante la Primera iteración
En esta primera entrega se presenta el primer prototipo, que consta de un servicio web que se ejecuta en el computador que corre ROS, y que es visible dentro de la red local. Actualmente es posible conectarse a este servicio desde un dispositivo cliente. La única página funcional hasta ahora permite visualizar un diagrama de los nodos y tópicos que corren en la instancia de ROS del servidor y que es generado por éste en respuesta a la petición del cliente cada vez que se conecte. El diagrama generado corresponde a una imagen en formato svg, la cual es generada y modificada en el servidor a fin de otorgarle características interactivas dinámicas. 
