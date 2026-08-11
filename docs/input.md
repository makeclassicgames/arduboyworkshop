# Entrada (Input)

Una vez hemos creado y subido nuestro primer programa "Hola Mundo" en el Arduboy, es hora de aprender a manejar la entrada de usuario a través de los botones del dispositivo. El Arduboy cuenta con varios botones que permiten a los jugadores interactuar con los juegos y aplicaciones.

<figure>
  <img src="/arduboyworkshop/img/Arduboy.png" alt="Botones de Arduboy" width="150">
  <figcaption>Botones de control del Arduboy.</figcaption>
</figure>

Vemos que tenemos disponibles los siguientes botones:

- **Cruceta direccional (D-Pad):** Permite mover el cursor o personaje en cuatro direcciones: arriba, abajo, izquierda y derecha.
- **Botones A y B:** Son botones de acción que pueden ser utilizados para confirmar selecciones, saltar pantallas o realizar otras acciones dentro del juego.

Arduboy permite detectar el estado de los botones en cada fotograma del juego, lo que permite a los desarrolladores crear interacciones dinámicas y responsivas. En la siguiente sección, aprenderemos a leer la entrada de los botones y a utilizarla para controlar el comportamiento de nuestro juego o aplicación.

Veamos un ejemplo de utlización con el ejemplo anterior "Hola Mundo" para detectar la entrada de los botones y realizar una acción en consecuencia.

```c++

#include <Arduboy2.h>

Arduboy2 arduboy;

byte x,y;


void setup() {
  // initiate arduboy instance
  arduboy.begin();

  arduboy.setFrameRate(15);
  x=4;
  y=9;
}


void loop() {
  if (!(arduboy.nextFrame()))
    return;

  if(arduboy.pressed(UP_BUTTON)){
    y--;
  }

  if(arduboy.pressed(DOWN_BUTTON)){
    y++;
  }

  if(arduboy.pressed(LEFT_BUTTON)){
    x--;
  }

  if(arduboy.pressed(RIGHT_BUTTON)){
    x++;
  }

  // first we clear our screen to black
  arduboy.clear();

  arduboy.setCursor(x, y);

  arduboy.print(F("Hello, world!"));

  arduboy.display();
}
```

Vamos a ver este código centrándonos en las diferencias con el ejemplo anterior "Hola Mundo". En este caso, hemos agregado la detección de los botones de entrada para mover el mensaje "Hello, world!" en la pantalla del Arduboy.

Comenzamos viendo que hemos creado dos variables `x` y `y` de tipo `byte` para almacenar las coordenadas del cursor en la pantalla. Inicializamos estas variables en la función `setup()` con valores iniciales de 4 y 9, respectivamente.

En la función `loop()`, hemos agregado varias condiciones para detectar si se han presionado los botones de dirección. Utilizamos el método `arduboy.pressed()` para verificar si un botón específico está siendo presionado en ese momento.

Vemos que se comprueban los botones de dirección (arriba, abajo, izquierda y derecha) y se ajustan las coordenadas `x` e `y` en consecuencia. Por ejemplo, si se presiona el botón "UP_BUTTON", la coordenada `y` se decrementa en 1, moviendo el mensaje hacia arriba en la pantalla.

Una vez que se han actualizado las coordenadas, se limpia la pantalla y se establece el cursor en la nueva posición utilizando `arduboy.setCursor(x, y)`. Luego, se imprime el mensaje "Hello, world!" en la pantalla y se actualiza la pantalla con `arduboy.display()`.

Tras ver este ejemplo, podemos observar cómo la entrada de los botones permite interactuar con el contenido en la pantalla del Arduboy, brindando una experiencia más dinámica y divertida para los usuarios. En la siguiente sección, exploraremos cómo dibujar figuras y gráficos en la pantalla del Arduboy para mejorar aún más la experiencia de juego.