---
layout: post
title: "Reporte Final del  Proyecto"
date: 2015-12-14 15:00:00
author: Carolina Hernandez, Francisco Montoto
categories: rostopic GUI final webtopic project
---

##Introducción
Este reporte busca retratar el proceso que finalmente llevó al desarrollo de lo que llamamos [Webtopic](https://github.com/carolahp/rostopic-gui).

Tras interiorizarnos con el uso del [turtlebot](http://www.turtlebot.com) mediante [ROS](http://www.ros.org) en la primera mitad del semestre, durante el cual realizamos varias pruebas y pequeñas rutinas con él, como por ejemplo un [baile](http://carolahp.github.io/testpage/turtlebot/baile/python/script/2015/10/01/el-baile-de-la-tortuga.html); fuimos notando que ciertas características de ROS y de sus herramientas de desarrollo, podían optimizarse y, de este modo el trabajo de los desarrolladores podría volverse más ameno.

Algunas de las características que llamaron nuestra atención, y nuestras ideas para atacarlas, se discuten más adelante en este reporte. Se finaliza con la presentación de nuestro proyecto final, y su calidad de aporte a la comunidad de desarrollo de ROS.

##Concepción del proyecto

###¿Por qué los tópicos de ROS?
Los tópicos de ROS son buses, o canales, de información que conectan los distintos nodos permitiéndoles intercambiar información.

Quizás no lo notamos en un comienzo, pero nuestras quejas más duras respecto a ROS estuvieron casi siempre relacionadas a las herramientas para tratar con los tópicos. Es difícil decirlo con certeza, pero probablemente nuestra fijación surge porque nuestro proyecto de [baile](http://carolahp.github.io/testpage/turtlebot/baile/python/script/2015/10/01/el-baile-de-la-tortuga.html) nunca pudo ejecutarse correctamente en el robot con el que contábamos, debido al comportamiento inesperado de un tópico, situación que simplemente vimos demasiado tarde. Sin entrar en mucho detalle, el problema consistió en que uno de los tópicos que nuestro programa utilizaba como input, publicaba información errónea.

###Las primeras ideas.
Desde la línea de comandos la principal forma de interactuar con los tópicos es la herramienta de ROS [rostopic](http://wiki.ros.org/rostopic), la cual permite publicar, escuchar y obtener información sobre cada uno de los tópicos activos. Lamentablemente posee limitaciones importantes, la que más resentimos fue tener que hacer una llamada distinta para cada operación y para cada tópico distinto con el que deseáramos interactuar. Ésta es una limitación de gran importancia cuando hay un número no menor de tópicos corriendo en el robot.

Sin embargo ROS incluye heramientas gráficas que para ciertos casos de uso cubren la deficiencia de rostopic. Una de ellas es [rqt_graph](http://wiki.ros.org/rqt_graph) que como su nombre indica es un grafo que expone las interacciones entre nodos y tópicos ejecutándose en el sistema. En esta herramienta vimos un gran potencial que aún no se encontraba desarrollado, pues no es posible interactuar con los nodos del gráfico para obtener los mensajes publicados o bien publicar. Esta fue la primera idea que tuvimos y se encuentra documentada en su propio [reporte](http://carolahp.github.io/testpage/rostopic/gui/progress/project/2015/10/22/reporte-de-la-propuesta.html). Sin embargo, al poco andar descubrimos un plug-in para rqt que hacía exactamente lo que proponíamos agregar a rqt_graph. Después de lamentar no haber conocido la herramienta al debuggear nuestro primer proyecto caímos en cuenta que nuestro proyecto no agregaba mucho valor si es que pretendíamos implementar funcionalidades que ya existían. Así fue como el proyecto llegó a un prematuro final.

Luego de esto, y siguiendo nuestro enfoque en los tópicos, empezamos a imaginar nuevas visualizaciones y formas de hacer más atractivo y útil el proceso de monitorear la actividad de los tópicos. Algunas visualizaciones ya existían, [rqt_plot](http://wiki.ros.org/rqt_plot) por ejemplo, y el resto de las ideas que tuvimos no fueron lo suficientemente convincentes tanto para el docente como para nosotros mismos, en gran parte por su poco valor agregado.

Así fue como la primera semana de trabajo en el proyecto se nos pasaba definiéndolo.

###La epifanía
A minutos de finalizar la primera semana, mientras recordábamos lo complicado que fue hacer pruebas con el robot, pues mientras uno tenía que seguirlo cuidando que no se golpeara o golpeara a alguien o algo más, el otro debía permanecer en el computador viendo que sucedía en ROS, fue que identificamos esta situación como un problema y decidimos atacarlo. En ese momento WebTopic comenzó a tomar forma.

##Descripción de Webtopic

###Definición
Webtopic es un Servicio web que permite interactuar con ROS desde dispositivos móviles. Sus funcionalidades más importantes se resumen en tres puntos:
- Visualizar nodos, tópicos y su interacción.
- Escuchar los mensajes publicados en un tópico.
- Publicar mensajes en un tópico. (funcionalidad pendiente)

###Qué ventajas ofrece al desarrollador
Webtopic aborda el problema de movilidad que surge cuando el desarrollador trabaja con robots que se desplazan en el espacio y no puede atender al robot y a ROS a la vez. Al proveer interacción con ROS desde un dispositivo móvil, Webtopic permite al desarrollador desplazarse junto con el robot, sin perder detalle de lo que ocurre a nivel de nodos, tópicos y mensajes. 
Webtopic es una solución que se adadpta a cualquier escenario, ya que no impone requerimientos especiales sobre el dispositivo móvil. Funcionará en cualquier dispositivo móvil que cuente con un explorador web y con conexión WiFi, ya que los procesos de ROS se ejecutarán en un computador convencional que debe estar en red con el dispositivo móvil.

###Funcionalidades e interfaces

La vista principal de Webtopic en un dispositivo móvil es la siguiente:
<a href="{{site.baseurl}}/assets/webtopic-interfaces/portada.png" data-lightbox="portada" data-title="Principal"><img src="{{site.baseurl}}/assets/webtopic-interfaces/portada.png" title="Principal" style="width:50%;height:50%"></a>
En ésta es claro notar lo siguiente:
- La url desde la que Webtopic es accesible corresponde a la dirección IP del computador que corre ROS y el servidor de Webtopic
- El elemento central es un gráfico que presenta interacciones entre tópicos y nodos. En éste los rombos representan tópicos, los cuadrados representan nodos, y las flechas representan relación entre nodos y tópicos. Una flecha que parte en un nodo  y finaliza en un tópico indica que tal nodo está publicando en ese tópico. Una flecha en sentido inverso indica que el nodo está escuchando ese tópico.
- La sección inferior muestra los botones echo y publish. Éstos funcionan sólo cuando un tópico ha sido seleccionado y sirven para escuchar o publicar en éste. (la funcionalidad de publish está pendiente). El botón presente en la sección superior sirve para ver un listado de aquellos tópicos que se están escuchando o sobre los que se está publicando actualmente.


La siguiente interfaz muestra cómo luce un tópico que ha sido seleccionado en el gráfico:  
<a href="{{site.baseurl}}/assets/webtopic-interfaces/topico%20select.png" data-lightbox="topico-select" data-title="Selección de tópico"><img src="{{site.baseurl}}/assets/webtopic-interfaces/topico%20select.png" title="Selección de tópico" style="width:50%;height:50%"></a>
El gráfico contenido en Webtopic es interactivo en cuanto a que sus componentes son seleccionables mediante un toque (touch-event). Cuando un tópico es seleccionado tanto éste como todas las flechas que parten o terminan en él son coloreados en tonos rojos. Cuando un nodo es seleccionado éste se colorea de azul.
Es importante notar que cuando un elemento del gráfico es seleccionado, detalles al respecto suyo son desplegados en la sección inferior de la pantalla: Se despliega nombre para el caso de los nodos y para el caso de los tópicos se muestra nombre y tipo de mensaje.


A medida que la cantidad de tópicos y nodos activos crece, también lo hace en tamaño y complejidad el gráfico generado por Webtopic. Es por eso que se ha incluido la funcionalidad de zoom independiente del resto de la interfaz, lo cual facilita la labor de inspección y selección de los elementos. Esta característica de Webtopic es ilustrada en la siguiente imagen:
<a href="{{site.baseurl}}/assets/webtopic-interfaces/topico%20select%20zoom.png" data-lightbox="topico-select-zoom" data-title="Tópico seleccionado y zoom"><img src="{{site.baseurl}}/assets/webtopic-interfaces/topico%20select%20zoom.png" title="Tópico seleccionado y zoom" style="width:50%;height:50%"></a>
El efecto zoom puede gatillarse de dos modos: mediante eventos de 'pich' o bien utilizando los botones '+', 'RESET' y '-' incorporados en la interfaz.

Habiendo ya seleccionado un tópico, es posible monitorear los mensajes que se están enviando a través suyo. La siguiente pantalla muestra el efecto de presionar el botón "echo" cuando el tópico /turtle1/pose ha sido seleccionado:
<a href="{{site.baseurl}}/assets/webtopic-interfaces/listening.png" data-lightbox="listening" data-title="Escuchando un tópico">
	<img src="{{site.baseurl}}/assets/webtopic-interfaces/listening.png" title="Escuchando un tópico" style="width:50%;height:50%"></a>
Tal como se aprecia en la captura, la información requerida se muestra dentro de un panel desplegable ubicado a la derecha de la pantalla. Como en ROS existen tipos de mensajes con estructuras anidadas complejas, la información correspondiente se presenta dentro de un árbol desplegable interactivo. El mensaje desplegado en pantalla corresponde al último publicado en el tópico y la taza a la que se refresca es de 2 Hz. Así es posible ver en tiempo real qué se está publicando por ese tópico.

La última interfaz muestra el panel de tópicos activos. En éste se muestran aquellos tópicos que se están escuchando y aquellos sobre los que se está publicando (funcionalidad pendiente). 
<a href="{{site.baseurl}}/assets/webtopic-interfaces/active%20topics.png" data-lightbox="active-topics" data-title="Tópicos activos">
	<img src="{{site.baseurl}}/assets/webtopic-interfaces/active%20topics.png" title="Tópicos activos" style="width:50%;height:50%"></a>
El nombre de cada tópico se muestra al interior de un botón, que al ser activado, despliega el panel de escucha o de publicación correspondiente. Además, junto al nombre de cada tópico se muestra un botón 'X' para cesar la actividad de escucha o publicación correspondiente.

###Diseño y Arquitectura de Webtopic
El diseño y arquitectura de Webtopic se han mantenido intactos desde la publicación del [reporte de la propuesta definitivo](http://carolahp.github.io/testpage/rqt_graph/topic/node/msg/progress/proyect/2015/11/08/reporte-de-la-propuesta2.html). 

La arquitectura general del sistema está definida por lo expuesto en la siguiente figura.
<a href="{{site.baseurl}}/assets/gen-architecture.png" data-lightbox="architecture" data-title="Arquitectura">
	<img src="{{site.baseurl}}/assets/gen-architecture.png" title="Arquitectura" style="width:50%;height:50%"></a>
Lo más relevante es que notar que en la máquina donde ROS corre, se levanta un microservidor web: Flask, en el que corre el servicio Webtopic, que rescata la información relativa a ROS desde roscore mediante funciones de roslib, algunas de las cuales debieron ser reimplementadas desde cero por la poca extensibilidad de algunas de las librerías de ROS. Un refactoring del código de rostopic.py queda como trabajo propuesto. Los dispositivos móviles se conectarán con Flask a través de la red local.

El flujo de datos es expuesto en la siguiente figura:
<a href="{{site.baseurl}}/assets/data-flow.png" data-lightbox="data-flow" data-title="Flujo de datos">
	<img src="{{site.baseurl}}/assets/data-flow.png" title="Flujo de datos" style="width:50%;height:50%"></a>
Se puede ver que los formatos más relevantes utilizados por Webtopic son JSON y SVG. Los datos provenientes de roscore son utilizados para conformar la imagen SVG generada por Webtopic, y las funcionalidades de echo y publish se valen de JSONs para funcionar. 

###Funcionalidades que no pudieron ser implementadas
El proyecto Webtopic contempló abarcar tanto la visualización del gráfico de nodos y tópicos, el monitoreo de mensajes mediante escucha y la publicación de mensajes. Esta última funcionalidad no pudo ser implementada por alcances de tiempo, sin embargo, dado el diseño de la solución, implementar esta función no debiese requerir mayor trabajo. Para implementar publish deberá agregarse un endpoint al backend, y un template de interfaz adaptable según el tiempo de mensaje. Este template puede reutilizar la estructura de árbol utilizada para el panel de echo. 

Hubo detalles además que habrían agregado valor, pero que no alcanzaron a ser implementados. Entre ellos se cuenta:

- Permitir al usuario elegir el rate al cual el último mensaje es rescatado y desplegado en la interfaz de escucha. Esta modificación sólo requiere modificar el frontend, agregando un input que determine el valor de la taza de refresco que actualmente se encuentra hardcodeado en 2 Hz. 

- Mostrar la frecuencia a la cual se está publicando sobre el tópico seleccionado, en la interfaz de escucha. Actualmente esta interfaz sólo muestra el último mensaje publicado. Si de pronto cesan todas las publicaciones sobre el tópico, la interfaz de escucha continuará desplegando el último mensaje, lo que puede resultar contraintuitivo para el usuario, que creerá que aún se está publicando sobre ese tópico. 

- Ajustar formato en los campos de la interfaz de ecucha. Actualmente, si los mensajes publicados son muy largos, la interfaz de escucha presenta un overflow. Esta situación puede ser controlada modificando sólamente el frontend.

###Trabajo propuesto
Además de proponer terminar las funcionalidades no implementadas, algunas funciones que no fueron contempladas al momento de la definición del proyecto, cobraron importancia durante su ejecición. Las siguientes tareas agregarían valor a la solución y quedan propuestas para el usuario interesado:
- Implementar mecanismos de autentificación que doten a la solución de seguridad, para así permitir su uso desde redes remotas, y no limitar Webtopic a la red local.
- Rediseñar e implementar una interfaz orientada a dispositivos de escritorio, que aproveche el espacio y los eventos del mouse para sacar más partido a Webtopic si es que se decide utilizarlo desde un dispositivo que no sea móvil.



