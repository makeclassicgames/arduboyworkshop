# Dibujar Imágenes

Arduboy proporciona funciones para dibujar imágenes en la pantalla. Estas funciones permiten cargar y mostrar imágenes predefinidas, lo que facilita la creación de gráficos y elementos visuales en los juegos.

Es importante mencionar que la pantalla de Arduboy es monocromática, por lo que las imágenes deben ser en blanco y negro. Además, las imágenes deben tener como mucho una resolución de 128x64 píxeles, para poder mostrarla en pantalla.

Es importante mencionar, que la Arduboy no tiene capacidad de poder leer imágenes en formatos modernos como PNG, JPEG,etc... Por lo que hay que transformarlas a un formato compatible. Arduboy, permite leer y mostrar imágenes en formato binario.

El formato que usa la Arduboy para las imágenes se basa en la utilización de binario para mostrar la información en la pantalla OLED. Estableciendo cada pixel con 1 bit (0= no se muestra, 1= se muestra).

Veamos un poco de cómo se códifican las imagenes con un ejemplo:


<figure>
  <img src="/arduboyworkshop/img/examplebitmap.png" alt="Ejemplo" width="512" height="256" style="border: 1px solid #000;">
  <figcaption>Ejemplo de imagen en formato binario de una imagen de 8x8 píxeles.</figcaption>
</figure>

En el ejemplo anterior, se ha ampliado la imagen para mostrar su formato binario. Vamos a ver como podríamos mostrarla en nuestra pantalla de Arduboy. Para ello, primero debemos definir la imagen en nuestro código. Esto se hace utilizando un array de bytes que representa cada fila de la imagen. Veamos el código para definir la imagen en Arduboy:

```cpp
const uint8_t PROGMEM myImage[]  = {
  0b01111110, // Fila 1
  0b10000001, // Fila 2
  0b10000001, // Fila 3
  0b10100101, // Fila 5
  0b10000001, // Fila 6
  0b10011001, // Fila 7
  0b10000001, // Fila 4
  0b01111110, // Fila 8
};
```

!!! info
    Habrás podido notar que se ha añadido la palabra `PROGMEM` al declarar el array. Esto es necesario para almacenar la imagen en la memoria flash del Arduboy, en lugar de la memoria RAM, que es limitada. Al usar `PROGMEM`, podemos almacenar imágenes más grandes sin agotar la memoria disponible.

Este código lo guardaremos como un fichero `.h` (por ejemplo `myImage.h`) y lo incluiremos en nuestro proyecto para poder usarlo.

!!! note
    Para añadir un fichero a nuestro proyecto en el IDE de Arduino, pulsa en el menu `Sketch` -> `Añadir archivo...` (Sketch->Add File) y selecciona el fichero que quieres añadir. Esto hará que el fichero se copie a la carpeta de tu proyecto y puedas incluirlo en tu código.

Una vez añadido, vamos a dibujar la imagen en la pantalla de Arduboy. Para ello, utilizaremos la función `drawBitmap()`, que nos permite dibujar una imagen en una posición específica de la pantalla. Veamos un ejemplo de cómo hacerlo:

```cpp
#include <Arduboy2.h>
#include "myImage.h" // Incluimos el fichero con la imagen

Arduboy2 arduboy;

void setup() {
  arduboy.begin();
  arduboy.setFrameRate(60);
}

void loop() {
  if (!arduboy.nextFrame()) return;

  arduboy.clear(); // Limpiamos la pantalla
  arduboy.drawSlowXYBitmap(20, 20, myImage, 8, 8, WHITE); // Dibujamos la imagen en la posición (20,20)
  arduboy.display(); // Mostramos la pantalla
}
``` 

En este ejemplo, hemos incluido el fichero `myImage.h` que contiene la definición de nuestra imagen. Luego, en el bucle principal (`loop()`), limpiamos la pantalla, dibujamos la imagen en la posición (20, 20) usando la función `drawSlowXYBitmap()` y finalmente mostramos la pantalla con `arduboy.display()`.

!!! info
    La función `drawSlowXYBitmap()` es una versión más lenta de `drawBitmap()`, pero es más fácil de usar y entender. Si quieres optimizar el rendimiento, puedes usar `drawBitmap()` directamente, pero requerirá un poco más de trabajo para manejar la memoria y los parámetros. Ya que requiere que el formato de la imagen este en formato MSB (Most Significant Bit) y no LSB (Least Significant Bit) como el que hemos usado en el ejemplo. Para más información sobre cómo usar `drawBitmap()`, puedes consultar la documentación oficial de la librería Arduboy2.

Con esto debería de verse la imagen en la pantalla de Arduboy. Puedes cambiar las coordenadas (20, 20) para mover la imagen a diferentes posiciones en la pantalla.

## Sprites y Conversiones

