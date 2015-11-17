---
layout: post
title: "Reporte de la propuesta definitivo"
date: 2015-11-08 15:00:00
author: Carolina Hernandez, Francisco Montoto
categories: rqt_graph topic node msg progress proyect
---

##Problema
ROS es una herramienta que requiere una máquina con recursos considerables para funcionar de manera óptima. Por ello es utilizado generalmente desde un computador de escritorio o un notebook, lo cual resulta incómodo al momento de trabajar con un robot real, en especial cuando las pruebas que se realizan sobre éste implican que el robot se desplace de un lugar a otro. Esta situación obliga al implementador a elegir entre observar el comportamiento del robot in situ o bien monitorearlo estáticamente desde el computador que ejecuta ROS. El no poder coordinar bien la ejecución de ambas labores al únisono deriva en la necesidad de aumentar el número de veces que un test necesite realizarse, lo que aumenta el tiempo de desarrollo y disminuye la eficiencia del desarrollador.

##Solución
El proyecto propuesto pretende ofrecer un servicio web, accesible desde dispositivos móviles, a través del cual sea posible utilizar funcionalidades específicas de ROS para así permitir al desarrollador seguir en el espacio y observar el comportamiento del robot a la vez que monitorea su estado mediante la observación del dispositivo móvil. }

El producto final consistirá en un servicio web visible a nivel de red local, a través del cual se proveerá a los clientes las siguientes funcionalidades:
- Visualización tópicos y nodos gráficamente, estilo rqt_graph.
- Interfaz para publicar mensajes a un tópico previamente seleccionado.
- Interfaz para ver los mensajes publicados en un tópico 
- Mecanismo de navegación para recorrer los mensajes publicados en un tópico temporalmente (concreción del requerimiento sujeto a plazos del proyecto)


##Diseño de la solución

#Arquitectura del sistema
En la figura 1 se expone la arquitectura general del sistema. Según ésta, la información extraída y procesada desde roscore, es expuesta al usuario mediante un servicio web levantado por el microservidor Flask cuya visibilidad será limitada a la red local con el fin de disminuir el riesgo de ataques externos. Tanto ROS como Flask serán ejecutados en el mismo computador servidor. 
A través de la red local, diversos clientes podrán conectarse al servicio web ofrecido, accediendo así a la información relativa a la instancia de ROS que se ejecuta en la máquina servidor.
![Figura 1: Arquitectura general]({{site.baseurl}}/assets/gen-architecture.png)

El diseño del sistema comprende la extracción de datos referentes a tópicos, nodos y mensajes desde roscore utilzando funciones provenientes de la clase rostopic de ROS. Estos datos serán utilizados tanto para generar el diagrama estilo rqt_graph de nodos y tópicos, como para implementar los servicios de publicación y escucha de mensajes. Por otro lado, cuando el cliente publique mensajes, éstos serán enviados al servidor en formato JSON y serán comunicados a la instancia de ROS oportunamente. De este modo se implementa un servicio al cliente que es bidireccional en cuanto al envío de mensajes y de información de tópicos y nodos. 
![Figura 2: Flujo de datos]({{site.baseurl}}/assets/data-flow.png)

#Detalles de la implementación
La visualización de tópicos y nodos será creada del siguiente modo:
- La información sobre los nodos, tópicos y mensajes será obtenida utilizando funciones del módulo rosgraph, propio de ROS. 
- La información anterior se utilizará para generar un archivo dot usando la librería pydot. 
- Habiendo obtenido ya el archivo dot, se utilizará pydot nuevamente para generar un archivo svg, en el cual las posiciones correspondientes del diagramas habrán sido determinadas óptimamente gracias a la librería.
- El archivo svg puede ser visualizado en cualquier broqser web, por lo cual no es necesario más procesamiento para lograr visualizarlo. 

La interfaz para publicar mensajes sobre un tópico ofrecerá un input por cada valor requerido, según el tipo de mensaje correspondiente al tópico.

La interfaz para ver los mensajes publicados sobre un tópico desplegará el último mensaje publicado. Idealmete se espera poder mostrar mensajes correspondientes a un intervalo de tiempo determinado, y recorrerlos en orden temporal gracias a una slidebar, no obstante la concreción de esta funcionalidad queda sujeta a los plazos establecidos para la finalización de este proyecto.

##Repositorio
[Repositorio GitHub](https://github.com/carolahp/rostopic-gui)
