# RGB

Arduboy cuenta con un led RGB que nos permite mostrar diferentes colores en la parte frontal de la consola. Este led se encuentra en la parte superior izquierda de la consola, justo al lado del altavoz.

Podemos controlar el color del led RGB mediante varias funciones que nos permiten encenderlo, apagarlo y cambiar su color. Dependiendo si queremos usar entradas/salidas analógicas o digitales, podemos usar diferentes funciones para controlar el led RGB.

## Usando entradas/salidas digitales

Comenzaremos utilizando las entradas/salidas digitales para controlar el led RGB. Para ello, utilizaremos la función `digitalWriteRGB()`, que nos permite establecer el color del led RGB mediante valores de intensidad para cada uno de los colores (rojo, verde y azul).

!!! info
    Una entrada/salida digital es un pin que puede estar en uno de dos estados: alto (HIGH) o bajo (LOW). En el caso del led RGB, podemos encender o apagar cada uno de los colores utilizando estos estados.

Esta función tiene 2 definiciones:

* `digitalWriteRGB(uint8_t color, uint8_t val)`: Esta definición nos permite establecer el color del led RGB mediante valores de intensidad para cada uno de los colores (rojo, verde y azul). El valor para el color se pasa en el primer parámetro con los valores recibidos son `RED_LED`, `GREEN_LED` o `BLUE_LED`. El segundo parámetro recibe los valores `RGB_ON` y `RGB_OFF`, que representan los estados alto y bajo respectivamente. Por ejemplo, para encender el color rojo, podemos usar `digitalWriteRGB(RED_LED, RGB_ON)`.
* `digitalWriteRGB(uint8_t red, uint8_t green, uint8_t blue)`: Esta definición nos permite establecer el color del led RGB mediante valores de intensidad para cada uno de los colores (rojo, verde y azul). Los valores para cada color se pasan en los parámetros `red`, `green` y `blue`, con valores como `RGB_ON` y `RGB_OFF`, que representan los estados alto y bajo respectivamente. Por ejemplo, para encender el color rojo, podemos usar `digitalWriteRGB(RGB_ON, RGB_OFF, RGB_OFF)`.

Podemos ver la siguiente tabla con los valores que podemos usar para encender o apagar cada uno de los colores del led RGB:

|RED_LED|GREEN_LED|BLUE_LED|Color|
|-------|---------|--------|-----|
|RGB_ON |RGB_OFF  |RGB_OFF |Rojo |
|RGB_OFF|RGB_ON   |RGB_OFF |Verde|
|RGB_OFF|RGB_OFF  |RGB_ON  |Azul |
|RGB_ON |RGB_ON   |RGB_OFF |Amarillo|
|RGB_ON |RGB_OFF  |RGB_ON  |Magenta|
|RGB_OFF|RGB_ON   |RGB_ON  |Cian |
|RGB_ON |RGB_ON   |RGB_ON  |Blanco|


## Usando entradas/salidas analógicas

Una vez hemos visto como trabajar con entradas/salidas digitales, podemos usar entradas/salidas analógicas para controlar el led RGB. Para ello, utilizaremos la función `setRGBled()`, que nos permite establecer el color del led RGB mediante valores de intensidad para cada uno de los colores (rojo, verde y azul).

Es importante mencionar que una salida analógica es un pin que puede tener un valor de voltaje variable, lo que nos permite controlar la intensidad de cada uno de los colores del led RGB. En el caso del led RGB, podemos establecer la intensidad de cada color mediante valores de 0 a 255, donde 0 representa apagado y 255 representa encendido al máximo.

!!! info
    En Arduino las salidas analógicas se manejan utilizando dispositivos especiales llamados PWM (Pulse Width Modulation), que nos permiten simular una salida analógica mediante la modulación de ancho de pulso. Esto permite establecer diferentes niveles de voltaje en el pin de salida. Para realizar esto, se utilizan los dispositivos DAC (Digital to Analog Converter), que convierten una señal digital en una señal analógica. En el caso del led RGB, podemos usar estos dispositivos para controlar la intensidad de cada color mediante valores de 0 a 255 (8 bits).

Para el caso del led RGB, podemos establecer la intensidad de cada color mediante valores de 0 a 255, donde 0 representa apagado y 255 representa encendido al máximo. Por ejemplo, para encender el color rojo al máximo, podemos usar `setRGBled(255, 0, 0)`. Para encender el color verde al 50% de intensidad, podemos usar `setRGBled(0, 128, 0)`.

Puedes ver un ejemplo completo en los ejemplos de la librería Arduboy2, donde se muestra como encender el led RGB con diferentes colores y niveles de intensidad. En el ejemplo `RGBLED`, podemos ver como se enciende el led RGB con diferentes colores y niveles de intensidad mediante la función `setRGBled()` o utilizando la función `digitalWriteRGB()`. En este ejemplo, se enciende el led RGB con diferentes colores y niveles de intensidad mediante un bucle que recorre los valores de intensidad para cada color.