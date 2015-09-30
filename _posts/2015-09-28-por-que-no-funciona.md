---
layout: post
title:  "Week #2"
date:   2015-09-21 17:00:00
author: Francisco Montoto, Carolina Hernandez
categories: progress
---

# Por qué no funciona?
Problema: El comando teleop no funciona para la primera versión del turtlebot.

Como lo solucionamos?
Inicializamos gazebo con la versión 1 del turtlebot y en paralelo lanzamos rqt_graph. Al analizar el grafo de los servicios en ejecución notamos que:

  1.- Teleop publica en /cmd_vel_mux/input/teleop
  
  2.- El nodo mobile_base_nodelet_manager recibe desde teleop y publica en /turtlebot_node/cmd_vel.
  
  3.- cmd_vel_mux no está suscrito a el tópico donde se publica la velocidad (/turtlebot_node/cmd_vel).
  
Por lo que concluimos que a pesar de que teleop estaba funcionando, el turtlebot no estaba suscrito a lo que se publicaba, implicando esto que el turtlebot no recibiera las instrucciones para moverse.

Problemas con las herramientas que notamos mientras se desarrollaba el chequeo:

  1.- Es difícil recordar cuando se debe usar rosrun y cuando roslaunch.
  
  2.- En algunas ocasiones, si gazebo era lanzado sin lanzar el core de ROS, éste fallaba. Esto ocurría de manera no determinística.
  
  3.- Hay ocasiones en que la vista de rqt_graph tiene muchos elementos, por lo que se superponen textos y figuras, es imposible acomodar los elementos en la vista.
