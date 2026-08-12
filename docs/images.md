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

Una vez visto como se muestran imágenes, en otras ocasiones es necesario trabajar con Sprites. Un Sprite es un objeto gráfico que se puede mover y manipular en la pantalla. Los Sprites son útiles para crear personajes, enemigos y otros elementos interactivos en los juegos.

Arduboy tiene una clase especial para manejar Sprites llamada `Sprites`. Esta clase proporciona funciones para dibujar y animar Sprites en la pantalla. Para usar Sprites, primero debemos definirlos de manera similar a como definimos las imágenes, pero con algunas diferencias.

Para definir un Sprite, podemos usar un array de bytes que representa cada fotograma del Sprite. Cada fotograma es una imagen que se mostrará en la pantalla. Veamos un ejemplo de cómo definir un Sprite con dos fotogramas:

```cpp
const uint8_t PROGMEM mySprite[]  = {
  8,8,
  // Fotograma 1
  0b01111110, // Fila 1
  0b10000001, // Fila 2
  0b10000001, // Fila 3
  0b10100101, // Fila 4
  0b10000001, // Fila 5
  0b10011001, // Fila 6
  0b10000001, // Fila 7
  0b01111110, // Fila 8
  // Fotograma 2
  0b01111110, // Fila 1
  0b10000001, // Fila 2
  0b10000001, // Fila 3
  0b10011001, // Fila 4
  0b10000001, // Fila 5
  0b10100101, // Fila 6
  0b10000001, // Fila 7
  0b01111110, // Fila 8
};
```

Podemos observar que los dos primeros bytes del array indica el ancho y alto del Sprite (8x8 píxeles en este caso). Luego, cada fotograma se define de manera similar a como definimos las imágenes, con cada fila representada por un byte.

Obviamente, para un ejemplo sencillo como el que vemos, se puede calcular a mano los bytes de la imagen... sin embargo, en otras ocasiones es algo más complicado y tedioso. Por ello, existen herramientas que nos permiten convertir imágenes a este formato binario de manera automática. Una de estas herramientas es [Image Converter](https://www.bloggingadeadhorse.com/TeamARGImgConverter/), que nos permite cargar una imagen y generar el código necesario para usarla en Arduboy.

Veamos un ejemplo de como mostrar una imagen. Para ello, hemos creado una imagen de 1 fotograma de 64x64 pixeles para mostrar por pantalla la foto del gran Streamer Caliebre (Al cual dedicamos este taller).

La imagen podemos descargarla desde el siguiente enlace:

<a href="/arduboyworkshop/img/caliebre.jpeg" target="_blank" download>Descargar Imagen</a>

Una vez descargada, podemos usar la herramienta [Image Converter](https://www.bloggingadeadhorse.com/TeamARGImgConverter/) para convertirla a un formato compatible con Arduboy. Solo tenémos que arrastrar la imagen a la herramienta y esta nos devolverá el código necesario para usarla en nuestro proyecto. 

<figure>
  <img src="/arduboyworkshop/img/converter.png" alt="Imagen convertida" width="400">
  <figcaption>Conversor, con la imagen convertida</figcaption>
</figure>

Recuerda que debes copiar el código generado por la herramienta y pegarlo en un fichero `.h` (por ejemplo `caliebre.h`) para poder incluirlo en tu proyecto.

Veamos el código de ejemplo para mostrar la imagen convertida en la pantalla de Arduboy:

```cpp
#include <Arduboy2.h>
#include "caliebre.h" // Incluimos el fichero con la imagen convertida

Arduboy2 arduboy;
Sprites sprites;

void setup() {
  arduboy.begin();
  arduboy.setFrameRate(60);
}

void loop() {
  if (!arduboy.nextFrame()) return;

  arduboy.clear(); // Limpiamos la pantalla
  sprites.drawSelfMasked(32, 0, caliebre, 0); // Dibujamos la imagen en la posición (32,0)
  arduboy.display(); // Mostramos la pantalla
}
```

!!! info
    En este ejemplo se usa la clase `Sprites` para dibujar la imagen convertida. La función `drawSelfMasked()` se utiliza para dibujar la imagen en la pantalla, y el último parámetro indica el fotograma que queremos mostrar (en este caso, el fotograma 0, ya que solo tenemos un fotograma). Existe una clase mejorada llamada `SpritesB` que permite dibujar Sprites de una forma más eficiente. Para más información sobre cómo usar `SpritesB`, puedes consultar la documentación oficial de la librería Arduboy2.

Con la imagen y el código ya podemos mostrar la imagen en la pantalla de Arduboy. Puedes cambiar las coordenadas (32, 0) para mover la imagen a diferentes posiciones en la pantalla.

<figure>
  <img src="/arduboyworkshop/img/arducaliebre.jpg" alt="Imagen en Arduboy" width="400">
  <figcaption>Imagen convertida y mostrada en la pantalla de Arduboy</figcaption>
</figure>