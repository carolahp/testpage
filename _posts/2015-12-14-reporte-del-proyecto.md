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
- La url desde la que webtópic es accesible corresponde a la dirección IP del computador que corre ROS y el servidor de Webtopic
- El elemento central es un gráfico que presenta interacciones entre tópicos y nodos. En éste los rombos representan tópicos, los cuadrados representan nodos, y las flechas representan relación entre nodos y tópicos. Una flecha que parte en un nodo  y finaliza en un tópico indica que tal nodo está publicando en ese tópico. Una flecha en sentido inverso indica que el nodo está escuchando ese tópico.
- La sección inferior muestra los botones echo y publish. Éstos funcionan sólo cuando un tópico ha sido seleccionado y sirven para escuchar o publicar en un tópico. (la funcionalidad de publish está pendiente)


La siguiente interfaz muestra un topico seleccionado del gráfico:  
<a href="{{site.baseurl}}/assets/webtopic-interfaces/topico%20select.png" data-lightbox="topico-select" data-title="Selección de tópico"><img src="{{site.baseurl}}/assets/webtopic-interfaces/topico%20select.png" title="Selección de tópico" style="width:50%;height:50%"></a>
El gráfico contenido en Webtopic es interactivo en cuanto a que sus componentes son seleccionables. Cuando un tópico es seleccionado tanto éste como todas las flechas que parten o terminan en él son coloreados en tonos rojos. Cuando un nodo es seleccionado su figura se colorea de azul.
Es importante notar que cuando un elemento del gráfico es seleccionado, detalles al respecto suyo son desplegados en la sección inferior de la pantalla: Se despliega nombre para el caso de los nodos y para el caso de los tópicos se muestra nombre y tipo de mensaje.


A medida que la cantidad de tópicos y nodos activos crece, también lo hace en tamaño y complejidad el gráfico de Webtopic. Es por eso que se ha incluido la funcionalidad de zoom independiente del resto de la interfaz, lo cual facilita la labor de inspección y selección de los elementos. Esta característica de Webtopic es ilustrada en la siguiente imagen:
<a href="{{site.baseurl}}/assets/webtopic-interfaces/topico%20select%20zoom.png" data-lightbox="topico-select-zoom" data-title="Tópico seleccionado y zoom"><img src="{{site.baseurl}}/assets/webtopic-interfaces/topico%20select%20zoom.png" title="Tópico seleccionado y zoom" style="width:50%;height:50%"></a>


Habiendo seleccionado un tópico, es posible monitorear los mensajes que se están enviando a través suyo. La siguiente pantalla muestra el efecto de presionar el botón "echo" cuando el tópico /turtle1/pose ha sido seleccionado:
<a href="{{site.baseurl}}/assets/webtopic-interfaces/listening.png" data-lightbox="listening" data-title="Escuchando un tópico">
	<img src="{{site.baseurl}}/assets/webtopic-interfaces/listening.png" title="Escuchando un tópico" style="width:50%;height:50%"></a>
En esta imagen se puede ver 

<a href="{{site.baseurl}}/assets/webtopic-interfaces/active%20topics.png" data-lightbox="active-topics" data-title="Tópicos activos">
	<img src="{{site.baseurl}}/assets/webtopic-interfaces/active%20topics.png" title="Tópicos activos" style="width:50%;height:50%"></a>

