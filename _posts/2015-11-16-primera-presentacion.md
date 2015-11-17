---
layout: post
title:  "Reporte de avances N°1"
date:   2015-11-16 12:00:00
author: Carolina Hernandez, Francisco Montoto
categories: rostopic GUI progress project web
---

#Resumen el enfoque definitivo del proyecto
Según el ![reporte de la propuesta original]({{site.baseurl}}/_posts/2015-10-22-reporte-de-la-propuesta.md) el objetivo del presente proyecto era implementar una GUI para rostopic, no obstante, debido a que se encontró una herramienta ya integrada a ROS (rqt) que implementaba casi todas las funcionalidades abarcadas en la propuesta original, se tomó la decisión de cambiar los objetivos. Luego de arduas discusiones sobre el camino que debía tomar el proyecto, se decidió cambiar su enfoque radicalmente ( con un poco de suerte por última vez). Tal como se especificó en el ![reporte de la propuesta definitivo]({{site.baseurl}}/_posts/2015-11-02-reporte-de-la-propuesta2.md), finalmente el proyecto atacará el problema del desplazamiento en el espacio del implementador al ejecutar programas usando ROS en un robot móvil. Cuando uno se encuentra testeando la ejecución en un robot que se mueve, tiene básicamente dos opciones para seguir los mensajes y tópicos que se están ejecutando: si el robot cuenta con un monitor uno puede seguir la secuencia desde el mismo robot; de lo contrario, o como otra opción, se puede seguir la ejecución desde otro computador, usualmente el que controla el robot, perdiendo la oportunidad de observar adecuadamente el comportamiento del robot.

El proyecto pretende agregar una tercera opción para observar en tiempo real los mensajes que circulan en el robot, busca ofrecer una interfaz web con un diseño amigable, especialmente orientada a dispositivos móviles, que permita seguir los mensajes, tópicos y nodos del robot incluso desde un teléfono celular u otro dispositivo móvil.

#Avances logrados durante la Primera iteración
En esta primera entrega se presenta el primer prototipo, que consta de un servicio web, visible sólo dentro de la red local, que se ejecuta en el mismo computador que corre ROS, al cual es posible conectarse desde un dispositivo cliente, ya sea móvil (smartphone, tablet) o fijo (notebook, PC). 

La única página funcional que se despliega hasta ahora, permite visualizar un diagrama de los nodos y tópicos que corren en la instancia de ROS del servidor, y que es generado por éste en respuesta a cada petición que el cliente efectúe. 

El diagrama generado corresponde a una imagen en formato svg, la que es creada y luego modificada en el servidor a fin de otorgarle características interactivas dinámicas. Estas características se limitan hasta ahora a cambiar el color (de negro a rojo) de las flechas del diagrama mientras el mouse esté posicionado sobre alguna o bien cuando se efectúe un toque desde una pantalla táctil; y a desplegar información sobre el tópico seleccionado en la región inferior de la pantalla, cada vez que el usuario toque o clickee una de las flechas del diagrama. 


