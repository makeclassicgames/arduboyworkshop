# Sonido

Arduboy tiene un altavoz incorporado que permite reproducir sonidos y música. El sonido se genera mediante la modulación de ancho de pulso (PWM) a través de 2 pines de salida, lo que permite generar diferentes frecuencias y tonos.

Veamos los Pines de salida que se utilizan para generar el sonido en Arduboy:

* Pin 1: Permite generar sonido mediante onda cuadrada. Este pin permite generar frecuencias entre 15.26Hz a 1000000Hz.
* Pin 2: Permite generar sonido mediante onda cuadrada. Este pin permite generar frecuencias entre61.04Hz a 15625Hz.

Existen varias funciones y librerías que nos permiten generar sonidos y música en Arduboy. La librería `Arduboy2` proporciona funciones para reproducir tonos y música, así como para controlar el volumen y la duración del sonido.

Sin embargo, es recomendable usar la librería `ArduboyPlayTune`, que nos permite reproducir tonos y música de manera más sencilla y con menos consumo de memoria. Esta librería proporciona funciones para reproducir tonos y música, así como para controlar el volumen y la duración del sonido.

Puedes instalar la librería `ArduboyPlayTune` desde el Administrador de Bibliotecas de Arduino, buscando "ArduboyPlayTune" e instalándola. Una vez instalada, podemos incluirla en nuestro proyecto y utilizar sus funciones para reproducir sonidos y música.

<figure>
  <img src="/arduboyworkshop/img/arduboyplaytune.png" alt="ArduboyPlayTune" width="300"/>
  <figcaption>Figura 1: Librería ArduboyPlayTune</figcaption>
</figure>

Con la libreria `ArduboyPlayTune` instalada, podemos ver el ejemplo incluido en la libreria Arduboy2 que nos permite reproducir diferentes tonos y música. Este ejemplo se encuentra en el menú de ejemplos de Arduino, en la sección "Arduboy2" y se llama "PlayTune". Al abrir este ejemplo, podemos ver el código que nos permite reproducir diferentes tonos y música.

Veamos algunas partes de este ejemplo:

```cpp
#include <Arduboy2.h>
#include <ArduboyPlaytune.h>

Arduboy2 arduboy;
ArduboyPlaytune tunes;
```

En esta primera parte, incluimos las librerías `Arduboy2` y `ArduboyPlaytune`, y creamos los objetos `arduboy` y `tunes` que nos permitirán controlar la consola y reproducir sonidos y música.

!!! warning
    Es importante mencionar que la librería `ArduboyPlayTune` utiliza la librería `Arduboy2` para controlar la consola, por lo que es necesario incluir ambas librerías en nuestro proyecto.

Si nos centramos en la función `setup()`, podemos ver que se inicializa la consola y se establece el volumen del sonido:

```cpp
void setup() {
  arduboy.begin();
  arduboy.setFrameRate(60);
  tunes.initChannel(PIN_SPEAKER_1);
#ifndef AB_DEVKIT
  // if not a DevKit
  tunes.initChannel(PIN_SPEAKER_2);
#else
  // if it's a DevKit
  tunes.initChannel(PIN_SPEAKER_1); // use the same pin for both channels
  tunes.toneMutesScore(true);       // mute the score when a tone is sounding
#endif
```
En este apartado podemos ver que se inicializa la consola y se inicial los canales correspondientes a los pines de salida del altavoz. En el caso de que estemos usando un DevKit, se inicializa el mismo pin para ambos canales y se silencia la música cuando se está reproduciendo un tono.

Veamos ahora la función `loop()`, donde se reproduce la música y los tonos:

```cpp
if (arduboy.pressed(UP_BUTTON)) {
    y-=1;
    tunes.tone(1175,300);
}
```

En este apartado podemos ver que se comprueba si se ha pulsado el botón de dirección "UP" y, en caso afirmativo, se reproduce un tono con una frecuencia de 1175Hz durante 300ms. Podemos ver que la función `tone()` nos permite reproducir un tono con una frecuencia y duración determinada.

En cada una de las direcciones de los botones, se reproduce un tono diferente, lo que nos permite generar diferentes sonidos al pulsar los botones de dirección.

En el caso de pulsar A o B, se silencia el sonido o se vuelve a activar la música, lo que nos permite controlar el sonido de la consola. Para ello, se utiliza `arduboy.audio.off()` y `arduboy.audio.on()`, que nos permiten silenciar o activar el sonido de la consola.

Por último, podemos ver que se reproduce la música de fondo mediante la función `tunes.playScore()`, que nos permite reproducir una partitura de música en formato de texto. En este ejemplo, se repeproduce la partitura `tunes_score`, que se encuentra definida en el ejemplo y contiene la música que se reproduce de fondo.

Para más información sobre la librería `ArduboyPlayTune`, puedes consultar la documentación oficial de la librería en el siguiente enlace: [ArduboyPlayTune](https://github.com/Ar-zz-duboy/ArduboyPlaytune).