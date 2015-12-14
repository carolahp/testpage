---
layout: post
title: "Reporte Final del  Proyecto"
date: 2015-12-14 15:00:00
author: Carolina Hernandez, Francisco Montoto
categories: rostopic GUI final webtopic project
---

##Introducción
Este reporte busca retratar el proceso que finalmente llevó al desarrollo de lo que llamamos [Webtopic](https://github.com/carolahp/rostopic-gui).

Tras interiorizarnos con el [turtlebot] (http://www.turtlebot.com) en la primera mitad del semestre, en la cual realizamos varias pruebas y pequeñas rutinas con él, como por ejemplo un [baile](http://carolahp.github.io/testpage/turtlebot/baile/python/script/2015/10/01/el-baile-de-la-tortuga.html). Fuimos notando ciertas cosas en [ROS] (http://www.ros.org) y en sus herramientas de desarrollo que podían hacerse mejor y hacer el proceso más ameno para los desarrolladores.

Algunas de las cosas que llamaron nuestra atención y nuestras ideas para atacarlas se discuten en el reporte, para finalizar con nuestro proyecto final y aporte a la comunidad de desarrollo de ROS.

##Concepción del proyecto

###¿Por qué los tópicos de ROS?
Los tópicos de ROS son buses, o canales, de información que conectan los distintos nodos permitiéndoles intercambiar información.

Quizás no lo notamos en un comienzo, pero nuestras quejas más duras con ROS estuvieron relacionadas a las herramientas para tratar con los tópicos. Es difícil decirlo con certeza, pero probablemente nuestra obsesión vino porque nuestro proyecto de [baile](http://carolahp.github.io/testpage/turtlebot/baile/python/script/2015/10/01/el-baile-de-la-tortuga.html) nunca pudo ejecutarse correctamente en el robot que poseíamos, debido a un comportamiento no esperado de un tópico que simplemente vimos demasiado tarde. Sin entrar en mucho detalle, el problema fue que uno de los tópicos que nuestro programa utilizaba como input publicaba información errónea.

###Las primeras ideas.
Desde la línea de comandos la principal forma de interactuar con los tópicos es [rostopic] (http://wiki.ros.org/rostopic), la cual nos permite publicar, escuchar y obtener información sobre cada uno de los tópicos activos. Lamentablemente posee limitaciones importantes, la que más resentimos fue tener que hacer una llamada distinta para cada operación y para cada tópico distinto con el que desearamos interactuar. Lo cuál es una limitación de gran importancia cuando hay un número no menor de tópicos corriendo en el robot.

Sin embargo ROS incluye heramientas gráficas que para ciertos casos de uso cubren la deficiencia de rostopic. Una de ellas es [rqt_graph](http://wiki.ros.org/rqt_graph) que como su nombre indica es un grafo con las interacciones entre nodos y tópicos ejecutándose en el robot. En esta herramienta vimos un gran potencial que aún no se encontraba desarrollado, pues no es posible interactuar con los nodos para obtener los mensajes publicados o incluso publicar. Esta fue la primera idea que tuvimos y se encuentra documentada en su propio [reporte] (http://carolahp.github.io/testpage/rostopic/gui/progress/project/2015/10/22/reporte-de-la-propuesta.html). Sin embargo, al poco andar descubrimos un plug-in para rqt que hacía exactamente lo que proponíamos agregar a rqt_graph. Después de lamentar no haber conocido la herramienta al debuggear nuestro primer proyecto caímos en cuenta que nuestro proyecto no agregaba mucho valor si es que pretendíamos implementar funcionalidades que ya existían, así fue como el proyecto llegó a un prematuro final.

Luego de esto, y siguiendo con nuestra fijación en los tópicos empezamos a imaginar nuevas visualizaciones y formas de hacer más atractivo y útil el proceso de debuggear lo que sucede en los tópicos. Sin embargo algunas ya existían, [rqt_plot](http://wiki.ros.org/rqt_plot) por ejemplo, y el resto no lograron convencer al profesor e incluso ni a nosotros mismos, en gran parte por su poco valor agregado.

Así fue como la primera semana de trabajo en el proyecto se nos pasaba buscándolo.

###La epifanía
A minutos de finalizar la primera semana, mientras recordábamos lo complicado que fue hacer pruebas con el robot. Pues mientras uno tenía que seguirlo cuidando que no se golpeara o golpeara a alguien o algo más el otro debía permanecer en el computador viendo que sucedía, fue que pensamos en atacar ese problema. En ese momento fue que WebTopic comenzó a tomar forma.
