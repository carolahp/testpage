---
layout: post
title:  "Reporte de avances N°1"
date:   2015-11-16 12:00:00
author: Carolina Hernandez, Francisco Montoto
categories: rostopic GUI progress project web
---

#Resumen del enfoque definitivo del proyecto
Según el ![reporte de la propuesta original]({{site.baseurl}}/_posts/2015-10-22-reporte-de-la-propuesta.md) el objetivo del presente proyecto era implementar una GUI para rostopic, no obstante, debido a que se encontró una herramienta ya integrada a ROS (rqt) que implementaba casi todas las funcionalidades abarcadas en la propuesta original, se tomó la decisión de cambiar los objetivos. Luego de arduas discusiones sobre el camino que debía tomar el proyecto, se decidió cambiar su enfoque radicalmente ( con un poco de suerte por última vez). Tal como se especificó en el ![reporte de la propuesta definitivo]({{site.baseurl}}/_posts/2015-11-02-reporte-de-la-propuesta2.md), finalmente el proyecto atacará el problema del desplazamiento en el espacio del implementador al ejecutar programas usando ROS en un robot móvil. Cuando uno se encuentra testeando la ejecución en un robot que se mueve, tiene básicamente dos opciones para seguir los mensajes y tópicos que se están ejecutando: si el robot cuenta con un monitor uno puede seguir la secuencia desde el mismo robot; de lo contrario, o como otra opción, se puede seguir la ejecución desde otro computador, usualmente el que controla el robot, perdiendo la oportunidad de observar adecuadamente el comportamiento del robot.

El proyecto pretende agregar una tercera opción para observar en tiempo real los mensajes que circulan en el robot, busca ofrecer una interfaz web con un diseño amigable, especialmente orientada a dispositivos móviles, que permita seguir los mensajes, tópicos y nodos del robot incluso desde un teléfono celular u otro dispositivo móvil.

#Descripción del prototipo obtenido en la Primera iteración
En esta primera entrega se presenta el primer prototipo, que consta de un servicio web, visible sólo dentro de la red local, que se ejecuta en el mismo computador que corre ROS, al cual es posible conectarse desde un dispositivo cliente, ya sea móvil (smartphone, tablet) o fijo (notebook, PC). 

La única página funcional que se despliega hasta ahora, permite visualizar un diagrama de los nodos y tópicos que corren en la instancia de ROS del servidor, y que es generado por éste en respuesta a cada petición que el cliente efectúe. 

El diagrama generado corresponde a una imagen en formato svg, que es creada y luego modificada en el servidor a fin de otorgarle características interactivas dinámicas. Estas características se limitan hasta ahora a cambiar el color (de negro a rojo) de las flechas del diagrama mientras el mouse esté posicionado sobre alguna o bien cuando se efectúe un toque desde una pantalla táctil; y a desplegar información sobre el tópico seleccionado en la región inferior de la pantalla, cada vez que el usuario toque o clickee una de las flechas del diagrama. 

#Descripción del proceso de desarrollo
Pese a que el objetivo final del proyecto fue determinado tan sólo una semana antes de la entrega del primer prototipo, no todo el trabajo presentado fue realizado durante esta semana, ya que fueron reutilizadas las funciones creadas para el proyecto rostopic-gui, en específico aquellas que extraían información sobre nodos y tópicos de roscore, y que generaban un archivos svg a partir de ésta.

El desarrollo del proyecto fue dividido en dos partes que se desarrollaron por separado: Frontend y Backend:

##Desarrollo del Backend
AQUI ESPECIFICAR COMO SE IMPLEMENTO EL BACKEND

Es importante mencionar que hubo funciones propias del módulo rostopic de ROS, que no pudieron ser utilizadas simplemente importando el módulo como librería. Para dichos casos, provisionalmente se copiaron y pegaron trozos de código de rostopic al proyecto local. Como una etapa adicional al proyecto, que surge a partir de esta problemática, se agrega el objetivo de remodularizar rostopic, tal que las funciones necesarias para obtener información acerca denodos, tópicos y mensajes, sean accesibles desde proyectos externos. 

##Desarrollo del Frontend
El objetivo principal del frontend para esta iteración era, en primer lugar, ser capaz de desplegar la imagen svg eficientemente, y en segundo lugar, implementar comportamientos interactivos a la misma, a través de los cuales el usuario podría seleccionar las flechas asociadas a los tópicos dentro del diagrama con el mouse (o tocándolas) y revisar información detallada acerca de las mismas. 

El primer paso era generar un nuevo diagrama cada vez que el cliente entrara a la página principal. Esto se logró utilizando las funcionalidades provistas por el backend. 
La renderización eficiente del svg fue lograda sin necesidad de mucho esfuerzo, dado que los browsers de internet (tanto para plataformas móviles como tradicionales) renderizan este tipo de imagenes nativamente.
La implementación de interacciones en el svg demandó mayor labor. Luego de investigar distintas maneras de lograrlo, fue decidida la alternativa de hacerlo con ayuda de javascript. Como es sabido, el formato svg consiste en un xml donde cada elemento del dibujo que se va a renderizar, queda determinado por uno o más tipos de tags que estipulan parámetros para una forma definida. Para implementar comportamientos interactivos en el svg, su xml fue modificado con la ayuda de una función javascript asociada al evento onload del html desplegado. El xml fue recorrido recursivamente, y los tags que formaban parte de alguna flecha en el diagrama, fueron seleccionados. A éstos se les agregaron EventListeners, que reaccionarían ante los eventos: mouseover, mouseout y click.

Los eventos mouseover y mouseout llamarían a funciones que cambiarían parámetros definidos dentro del tag (en este caso el color).
El evento click fue asociado a un función que rescata un atributo del tag (el nombre del tópico) para utilizarlo como parámetro para consultar asíncronamente al servidor, los detalles asociados a este tópico.

#Principales dificultades afrontadas durante el desarrollo
La principal y más grave dificultad encontrada fue no poder utilizar funciones de rostopic simplemente importándolo como librería. Y en cambio, tener que copiar y pegar trozos de código provenientes de este módulo al proyecto local. 
Se propone una remodularización de rostopic para poder usar sus funciones desde el exterior. 

#Objetivos de la siguiente iteración
Para la siguiente iteración se espera contar con un modelo absolutamente funcional de la aplicación, capaz de desplegar un svg que incluya interacciones en cada uno de sus componentes (nodos y tópicos) para conocer los detalles asociados a cada uno de ellos, y ofreciendo la posibilidad de escucha y de publicación de mensajes en el tópico seleccionado. Específicamente se espera:
- Diseñar e implementar una interfaz para despliegue de mensajes por tópico. Esta interfaz debe mostrar inicialmente el último mensaje publicado en ese tópico. Dependiendo del tiempo disponible, se espera que los mensajes anteriores al último rescatado puedan recorrerse con ayuda de un slider.

- Diseñar e implementar una interfaz para publicación de mensajes por tópico. Ésta deberá adaptar sus campos dependiendo del tipo de mensaje y deberá validar el tipo de datos que el usuario haya ingresado en cada campo.

- Diseñar e implementar interfaz orientada a móviles, teniendo en cuenta el reducido espacio de pantalla disponible en este tipo de aparatos.

- Implementar un refactoring de la clase de rostopic para permitir el acceso desde el exterior a funciones que consultan información relativa a tópicos, nodos y mensajes.



