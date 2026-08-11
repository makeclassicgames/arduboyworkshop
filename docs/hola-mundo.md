# Hola Mundo

Vamos a ponernos manos a la obra y crear nuestro primer programa para Arduboy. En esta sección, aprenderemos a escribir un programa simple que muestre un mensaje en la pantalla del dispositivo.

Recuerda seguir los pasos anteriores para instalar y configurar el entorno de desarrollo Arduino IDE y la librería _Arduboy2_ antes de continuar con este tutorial.

La librería _Arduboy2_ proporciona una serie de ejemplos que podemos utilizar como punto de partida para nuestros propios programas. Uno de estos ejemplos es el programa "Hola Mundo", que muestra un mensaje en la pantalla del Arduboy.

Para acceder a este ejemplo, sigue estos pasos:

1. Abre el Arduino IDE.
2. Ve al menú "Archivo" > "Ejemplos" > "Arduboy2" > "Hola Mundo" (Hello World).

Esto te llevará al código del ejemplo "Hola Mundo" que puedes modificar y cargar en tu Arduboy.

Veamos el código del ejemplo "Hola Mundo" y cómo funciona:

```c++
#include <Arduboy2.h>

Arduboy2 arduboy;

void setup() {
  arduboy.begin();
  arduboy.setFrameRate(15);
}

void loop() {
  if (!arduboy.nextFrame()) return;

  arduboy.clear();
  arduboy.setCursor(4, 9);
  arduboy.print(F("Hola, Mundo!"));
  arduboy.display();
}
```

Veamos qué hace cada parte del código:

- `#include <Arduboy2.h>`: Esta línea incluye la librería _Arduboy2_, que proporciona funciones y métodos para interactuar con el hardware del Arduboy.
- `Arduboy2 arduboy;`: Crea un objeto llamado `arduboy` que nos permitirá acceder a las funciones de la librería.

!!! info
    El objeto `arduboy` es esencial para controlar la pantalla, los botones y otras funciones del dispositivo. A través de este objeto, podemos dibujar en la pantalla, leer la entrada de los botones y manejar el sonido. Existen otras clases base como `Arduboy2Base` y `Arduboy2Core`, que proporcionan funcionalidades más básicas y permiten un mayor control sobre el hardware, pero para la mayoría de los proyectos, el objeto `arduboy` es suficiente.

Podemos observar 2 funciones principales en el código: `setup` y `loop`. Estas funciones son fundamentales en la programación de Arduino y, por extensión, en la programación de Arduboy.

- `void setup()`: Esta función se ejecuta una vez al inicio del programa. Aquí inicializamos el Arduboy y configuramos la velocidad de fotogramas.
- `void loop()`: Esta función se ejecuta en un bucle continuo. Aquí es donde escribimos el código que queremos que se ejecute repetidamente.

Vamos a centrarnos en la función `setup`:

- `arduboy.begin();`: Inicializa el Arduboy y prepara el dispositivo para su uso. Fuerza que aparezca el logo de Arduboy en la pantalla al iniciar el programa.
- `arduboy.setFrameRate(15);`: Configura la velocidad de fotogramas a 15 cuadros por segundo. 

!!! warning
    Es importante tener en cuenta que la velocidad de fotogramas puede afectar el rendimiento del juego y la experiencia del usuario. Ajustar la velocidad de fotogramas según las necesidades del juego es fundamental para garantizar un rendimiento óptimo.

Ahora vamos a ver la función `loop`:

- `if (!arduboy.nextFrame()) return;`: Esta línea asegura que el código dentro del bucle se ejecute solo una vez por fotograma, evitando que el programa se ejecute demasiado rápido y afecte la experiencia del usuario.
- `arduboy.clear();`: Limpia la pantalla antes de dibujar el siguiente fotograma.
- `arduboy.setCursor(4, 9);`: Establece la posición del cursor en la pantalla para que el texto se dibuje en esa ubicación.
- `arduboy.print(F("Hola, Mundo!"));`: Muestra el mensaje "Hola, Mundo!" en la pantalla del Arduboy.
- `arduboy.display();`: Actualiza la pantalla para mostrar el contenido dibujado en el fotograma actual.

!!! note
    Es importante recordar que el Arduboy tiene una pantalla monocromática de 128x64 píxeles, por lo que debemos tener en cuenta las limitaciones de espacio al mostrar texto o gráficos en la pantalla. Además de que todo lo que pintemos en la pantalla debe ser dibujado en cada fotograma, ya que el contenido de la pantalla no se mantiene entre fotogramas.

!!! info
    Habrás podido observar que el mensaje "Hola, Mundo!" se encuentra dentro de la función `F`. Esta función indica al compilador que el texto debe almacenarse en la memoria flash del Arduboy en lugar de la memoria RAM, lo que ayuda a optimizar el uso de recursos en el dispositivo.

## Cargando el programa en Arduboy

Una vez hemos revisado el código del ejemplo "Hola Mundo", podemos cargarlo en nuestro Arduboy siguiendo estos pasos:

1. Conecta tu Arduboy a tu computadora mediante un cable USB.
2. Enciende tu Arduboy con el interruptor de la parte superior.
3. En el Arduino IDE, selecciona la placa correcta y el puerto correspondiente a tu Arduboy desde el menú "Herramientas" > "Placa" y "Puerto" (Tools > Board y Port).
4. Haz clic en el botón "Cargar" (Upload) para compilar y cargar el programa en tu Arduboy.

!!! info
    Recuerda que arduboy se basa en la placa Arduino Leonardo, por lo que es importante seleccionar la placa correcta en el Arduino IDE para evitar problemas al cargar el programa. En caso de error, revisa tanto la placa como el puerto (en Windows COMX, en Linux /dev/ttyACMX) seleccionados en el IDE y asegúrate de que coincidan con tu Arduboy.

!!! warning
    Si experiementas algún problema al cargar el programa, asegúrate de que tienes permisos de escritura en el puerto serie y que no hay otro programa utilizando el puerto. Además, verifica que la librería _Arduboy2_ esté instalada correctamente y que estás utilizando la versión más reciente del Arduino IDE.

Si todo ha ido bien, deberías ver el mensaje "Hola, Mundo!" en la pantalla de tu Arduboy. ¡Felicidades! Has creado y cargado tu primer programa en el dispositivo.

<figure>
  <img src="/arduboyworkshop/img/helloworld.jpeg" alt="Hola Mundo" width="300">
  <figcaption>Mensaje "Hola, Mundo!" en la pantalla del Arduboy.</figcaption>
</figure>

