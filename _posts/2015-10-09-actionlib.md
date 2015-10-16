---
layout: post
title:  "El baile de la tortuga utilizando ActionLib"
date:   2015-10-08 17:00:00
author: Francisco Montoto, Carolina Hernandez
categories: actionlib turtlebot baile
---

#El baile de la tortuga utilizando ActionLib

En primer lugar se estudiaron los tutoriales y ejemplos disponibles en el apartado de ActionLib en la página de ROS. Una vez que hubo un entendimiento del método de funcionamiento de la librería se comenzó la programación como se explica a continuación:

1. El primer paso fue lograr compilar y ejecutar un cliente y servidor. Por lo que creamos un servidor sin ninguna funcionalidad que solo debía imprimir a pantalla un pequeño mensaje cada vez que un cliente se conectara.

2. Luego de establecer comunicación entre el cliente y el servidor se agregó más funcionalidad al servidor, y se logró obtener el valor de retorno del servidor en el cliente. Luego de este paso ya se puede decir que teníamos funcionando todo lo necesario de actionlib para el baile.

3. El paso final fue traducir el baile que hasta este momento funcionaba sin hacer uso de ActionLib hasta un script que se ejecutase en el servidor y que el cliente fuese capaz de llamar para ejecutar la acción. En la implementación sin ActionLib se hacía uso de tres funciones, una que hace girar al robot en su posición, otra que lo mueve hacia delante y atrás y una última que hacía moverse al robot dibujando una circunferencia. Decidimos que el cliente pasaría un string como goal y que a partir de este string el servidor interpretaría lo deseado por el cliente. Para esto definimos un pequeño protocolo en el que la primera palabra del string sería la función a llamar y luego de forma consecutiva se pasarían todos los parámetros, todo separado por espacios. Así, el argumento del goal se vería de la siguiente forma: [método] [arg_0] [..] [arg_n]
4. Con la forma de llamar a los métodos ya definida solo restaba el pasar los métodos desde la primera versión del baile hacia el servidor. Finalmente al pasarlos el baile logró funcionar tal y como estaba antes pero ahora utilizando ActionLib.

Aprendizajes y dificultades.
La librería es bastante simple de utilizar, al menos para el uso que necesitabamos, por lo que no tuvimos grandes dificultades en este proyecto. El único contratiempo que tuvimos fue el de descubrir la forma de parear el servidor con el cliente, pues el donde setear el parámetro no era muy intuitivo. Sin embargo luego de encontrar el parámetro y poder establecer la conexión fue todo directo.
