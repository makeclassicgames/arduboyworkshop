# Dibujar Figuras

Arduboy proporciona una serie de funciones para dibujar figuras geométricas básicas en la pantalla. Estas funciones permiten crear líneas, rectángulos, círculos y otras formas, lo que facilita la creación de gráficos y elementos visuales en los juegos.
En esta sección, aprenderemos a utilizar estas funciones para dibujar figuras en la pantalla del Arduboy y a combinarlas para crear gráficos más complejos.

Comenzaremos comentando que puedes ver todas las funciones disponibles para dibujar figuras en la documentación oficial de la librería Arduboy2, que se encuentra en [https://mlxxxp.github.io/documents/Arduino/libraries/Arduboy2/Doxygen/html/index.html](hhttps://mlxxxp.github.io/documents/Arduino/libraries/Arduboy2/Doxygen/html/index.html). Allí encontrarás información detalladai sobre cada función, sus parámetros y ejemplos de uso.

Vamos a ver un par de funciones:

* `drawLine(x0, y0, x1, y1, color)`: Dibuja una línea desde el punto `(x0, y0)` hasta el punto `(x1, y1)` con el color especificado. El color puede ser `WHITE` o `BLACK`. Por defecto, el color es `WHITE`, lo que significa que la línea se dibujará en blanco sobre un fondo negro.
* `drawRect(x, y, width, height, color)`: Dibuja un rectángulo en la posición `(x, y)` con el ancho y alto especificados y el color indicado. El color puede ser `WHITE` o `BLACK`. Por defecto, el color es `WHITE`, lo que significa que el rectángulo se dibujará en blanco sobre un fondo negro.
* `drawCircle(x, y, radius, color)`: Dibuja un círculo en la posición `(x, y)` con el radio especificado y el color indicado. El color puede ser `WHITE` o `BLACK`. Por defecto, el color es `WHITE`, lo que significa que el círculo se dibujará en blanco sobre un fondo negro.

!!! info
    Las funciones `drawRect` y `drawCircle` dibujan solo la silueta de la figura; sin embargo, existen las funciones `fillRect` y `fillCircle` permiten dibujar una figura rellena.

Veamos un ejemplo de uso de estas funciones:

```c++
#include <Arduboy2.h>

Arduboy2 arduboy;

void setup() {
    arduboy.begin();
    arduboy.setFrameRate(25);
}

void loop() {
    arduboy.clear();
    arduboy.drawLine(10, 10, 50, 50, WHITE);
    arduboy.drawRect(10, 10, 40, 40, WHITE);
    arduboy.drawCircle(30, 30, 20, WHITE);
    arduboy.display();
}
```

Una vez escrito el código, podemos subir y ejecutarlo en nuestra Arduboy.

<figure>
  <img src="/arduboyworkshop/img/figuresexample.png" alt="Ejemplo de figuras dibujadas en Arduboy" width="300">
  <figcaption>Ejemplo de figuras dibujadas en Arduboy</figcaption>
</figure>