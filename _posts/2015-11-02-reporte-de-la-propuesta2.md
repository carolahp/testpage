---
layout: post
title: "Vista dinámica de Nodos, Topics y Flujo de Mensajes, reporte de la propuesta."
date: 2015-10-22 15:00:00
author: Carolina Hernandez, Francisco Montoto
categories: rqt_graph topic node msg progress proyect
---

##Problema
ROS es una herramienta que requiere una máquina con recursos considerables para funcionar de manera óptima. Por ello es utilizado generalmente desde un computador de escritorio o un notebook, lo cual resulta incómodo al momento de trabajar con un robot real, en especial cuando las pruebas que se realizan sobre éste implican tareas de desplazamiento en el espacio.

##Solución
El proyecto propuesto pretende ofrecer un servicio web, accesible desde dispositivos móviles, a través del cual sea posible utilizar funcionalidades específicas de ROS. Este trabajo abarcará las siguientes funcionalidades 3, pero su alcance podrá ampliarse en trabajos futuros:
- Una visualización de tópicos y nodos, estilo rqt_graph.
- Una interfaz para publicar mensajes.
- Una interfaz para ver los mensajes publicados en un tópico.

##Diseño de la solución
Se levantará un micro-servidor web python (flask) en la máquina que ejecute ROS. Su visibilidad será limitada a la red local, para así evitar ataques externos. 

La visualización de tópicos y nodos será creada del siguiente modo:
- La información sobre los nodos, tópicos y mensajes será obtenida utilizando funciones del módulo rosgraph, propio de ROS. 
- La información anterior se utilizará para generar un archivo dot usando la librería pydot. 
- Habiendo obtenido ya el archivo dot, se utilizará pydot nuevamente para generar un archivo svg, en el cual las posiciones correspondientes del diagramas habrán sido determinadas óptimamente gracias a la librería.
- El archivo svg puede ser visualizado en cualquier broqser web, por lo cual no es necesario más procesamiento para lograr visualizarlo. 

La interfaz para publicar mensajes sobre un tópico ofrecerá un input por cada valor requerido, según el tipo de mensaje correspondiente al tópico.

La interfaz para ver los mensajes publicados sobre un tópico desplegará el último mensaje publicado. Idealmente se espera poder mostrar mensajes correspondientes a un intervalo de tiempo determinado, y navegarlos gracias a una slidebar, no obstante la concreción de esta funcionalidad queda sujeta a los plazos establecidos para la finalización de este proyecto.

##Repositorio
[Repositorio GitHub](https://github.com/carolahp/rostopic-gui)
