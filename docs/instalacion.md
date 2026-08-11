# Instalación y Condfiguración de Arduboy

Vamos a instalar y configurar el entorno de desarrollo Arduino IDE para poder programar nuestro dispositivo Arduboy. A continuación, se detallan los pasos necesarios para llevar a cabo esta tarea.

En primer lugar si no se ha instalado el Arduino IDE, se debe descargar e instalar desde la página oficial de Arduino en [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software). Asegúrate de seguir las instrucciones de instalación específicas para tu sistema operativo.

Una vez instalado, vamos a configurar el entorno de desarrollo para trabajar con Arduboy. Para ello, debemos agregar el soporte para Arduboy y las diferentes librerías necesarias. A continuación, se detallan los pasos para realizar esta configuración:

1. Abrir el Arduino IDE y acceder al gestor de librerías desde el menú "Herramientas" > "Gestor de librerías" (Tools > Manage Libraries).
2. En el gestor de librerías, buscar "Arduboy2" y seleccionar la opción correspondiente para instalar la librería oficial de Arduboy.

<figure>
  <img src="/arduboyworkshop/img/bibliotecas.png" alt="Arduboy2 Library" width="400">
  <figcaption>Instalación de la librería Arduboy2</figcaption>
</figure>

!!! warning
    Es importante asegurarse de que la librería _Arduboy2_ esté instalada correctamente, aunque puede usarse la librería Arduboy original, esta se considera obsoleta y no se recomienda su uso en proyectos nuevos.

Una vez hecho esto, ya deberíamos tener el entorno de desarrollo listo para comenzar a programar nuestro Arduboy. En la siguiente sección, aprenderemos a configurar la placa Arduboy y a cargar nuestro primer programa en el dispositivo.


### Configuración de la placa Arduboy

Antes de continuar, si acabas de conseguir la placa Arduboy, es recomendable realizar una actualización del firmware para asegurarnos de que el dispositivo funcione correctamente y tenga las últimas mejoras y correcciones de errores. Para ello, podemos utilizar la herramienta de actualización de firmware proporcionada por Arduboy.

Es por ello que para actualizar el firmware de tu Arduboy, sigue estos pasos:

1. Dirigete a la web oficial de Arduboy en [https://bateske.github.io/ArduboyWebFlasher/](https://bateske.github.io/ArduboyWebFlasher/) y conecta tu Arduboy a tu computadora mediante un cable USB-C (o USB-A con un adaptador).
2. Enciende tu Arduboy con el interruptor de la parte superior y sigue las instrucciones en pantalla para seleccionar el archivo de firmware más reciente y cargarlo en tu Arduboy. Asegúrate de seguir cuidadosamente las indicaciones para evitar problemas durante el proceso de actualización.

<figure>
  <img src="/arduboyworkshop/img/updater.png" alt="Actualización de Firmware" width="400">
  <figcaption>Actualización de Firmware de Arduboy</figcaption>
</figure>

Una vez que hayas actualizado el firmware, tu Arduboy estará listo para ser utilizado con el entorno de desarrollo Arduino IDE y podrás comenzar a programar tus propios juegos y aplicaciones para el dispositivo.