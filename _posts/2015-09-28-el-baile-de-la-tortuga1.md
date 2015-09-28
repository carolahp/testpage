#El baile de la tortuga

1. Los pasos del baile serán:
- girar en 360°
- avanzar 3 segundos
- retroceder 3 segundos
- recorrer trayectoria circular en sentido horario

 2. Se corre gazebo y keyboard teleop. Se hace un rostopic list y se decide publicar en el topic /cmd_vel_mux/input/teleop
Para probar los movimientos se publican mensajes vía rostopic pub sobre el tópico elegido. Se detecta el problema de que los mensajes con parámetro -1 apenas se detectan. Además el comportamiento del robot es el mismo tanto si se agrega el flag -1 como si no.
