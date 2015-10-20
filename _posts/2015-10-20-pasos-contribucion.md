---
layout: post
title:  "Pasos para contribuir"
date:   2015-09-21 17:00:00
author: Francisco Montoto, Carolina Hernandez
categories: private
---

Pasos a seguir para contribuir en ROS:
http://wiki.ros.org/Get%20Involved

###Pasos Generales
1. [join the community](http://answers.ros.org/questions/)
2. [open issues and provide patches](http://wiki.ros.org/Tickets)
3. [desarrollar y compartir a traves de la mailing list](http://lists.ros.org/lurker/list/ros-users.en.html)
4. mantener los paquetes desarrollados 


###Pasos Especificos
  * suscribirse al mailing list 
  * [revisar las buenas practicas para escribir codigo publicadas por ROS](http://wiki.ros.org/ROS/Patterns)
  * [leer la ROS developer's guide[(http://wiki.ros.org/DevelopersGuide)
  * hacer los tutoriales para [test-driven-development en ROS](https://docs.google.com/presentation/d/1eraurS9rlMXyN0kbQMJdCyWOxRC5JTBV7FskyMaYNpM/present#slide=id.p)
  * instalar ROS jade (en ubuntu 15.04) -> no es necesario bajar los sources para compilar en la maquina, ya que python no se compila
  * hacer un fork del repositorio de ROS en github
  * una vez el proyecto este listo, indexar el reposotorio para generar documentacion
  * informar los avances del desarrollo y en especial el final del proyecto a traves de la mailing list
  
  
###Detalles tecnicos
  * Instalar ROS jade
    * targeted to Ubuntu 15.04 (actualizar ubuntu de ser necesario)
    * [instrucciones](http://wiki.ros.org/jade/Installation/Ubuntu)
  * [Tutorial para aprender a contribuir a los repositorios de ROS](http://wiki.ros.org/RecommendedRepositoryUsage)
  * [Tutorial para indexar repositorio y generar documentacion](http://wiki.ros.org/rosdistro/Tutorials/Indexing%20Your%20ROS%20Repository%20for%20Documentation%20Generation)
  * location de la clase rostopic en repositorio de ROS en Github https://github.com/ros/ros_comm/blob/indigo-devel/tools/rostopic/src/rostopic/__init__.py
  * path de la clase rostopic en la instalacion de ROS en PC robotica /opt/ros/indigo/lib/python2.7/dist-packages/rostopic
