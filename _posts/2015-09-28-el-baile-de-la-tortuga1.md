---
layout: post
title:  "El baile de la tortuga"
date:   2015-10-01 17:00:00
author: Francisco Montoto, Carolina Hernandez
categories: progress
---

#El baile de la tortuga

1. Los pasos del baile serán:
- girar en 360° en sentido antihorario
- avanzar 
- retroceder la misma distancia avanzada
- recorrer trayectoria semicircular en sentido antihorario


 2. Se corre gazebo y keyboard teleop. Se hace un rostopic list y se decide publicar en el topic /cmd_vel_mux/input/teleop
Para probar los movimientos se publican mensajes vía rostopic pub sobre el tópico elegido. Se detecta el problema de que los mensajes con parámetro -1 apenas tienen efecto. Además el comportamiento del robot es el mismo tanto si se agrega el flag -1 como si no.

3. Se crea un package de ros llamado baile_tortuga1. En éste se crea un script en python que envía sólo un mensaje. Éste se ejecuta junto con turtlebot_gazebo y se verifica que el turtlebot se mueve. 

Surgió el siguiente problema: Gazebo dejo de publicar y no nos percatamos dado que no lazó ningun mensaje de error. En consecuencia dejó de publicarse en el tópico joint_states y por ello el script parecía no funcionar cuando en realidad tan sólo no recibía mensajes. 

4. Se implementa el script según la siguiente lógica:
- Se evita el uso de variables globales y/o compartidas. 
- Se relega la lógica de cada movimiento a las funciones callback.

5. Al intentar correr el script en el robot, éste se comportó de forma inesperada, su movimiento era intermitente. Este hecho nos hizo pensar que la manera en que abordamos el problema (implementando la lógica del movimiento dentro de las funciones callback) no era la correcta. Por esto decidimos hacer un refactoring de nuestro código. El nuevo diseño implicó hace busy waiting y limitar la funcionalidad de las callbacks a actualizar una variable de posición. Pese a todo lo anterior, cuando probamos el nuevo script en el robot, obtuvimos el mismo resultado. Esto fue debido a que ,  los mensajes en el tópico joint_states eran publicados por el robot a una frecuencia muy baja, cercana a 1Hz. 
