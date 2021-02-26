<script type="text/javascript" charset="utf-8" 
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML,
https://vincenttam.github.io/javascripts/MathJaxLocal.js"></script>


# UART
---
## Contexto
---
El nombre UART viene de Universal Asynchronous Receiver Transmitter. Es un periférico que permite la comunicación entre dos dispositivos de manera serial, es decir, un bit seguido de otro.

La mayoría de los microcontroladores vienen con este periférico preparado y, salvando algunas diferencias de acuerdo a la potencia que tenga el micro, el principio de funcionamiento es el mismo y requerirá que configuremos la velocidad de transmisión que se mide en `bauds` o bits por segundo, elegir la cantidad de stop, parity y data bits, habilitar el transmisor y/o receptor dependiendo de la necesidad y elegir las interrupciones apropiadas.

Una comunicación serial se ve como esto:

![](./uart.png)

Donde pueden ver que hay un bit de `start` en nivel bajo, luego se transmite el paquete de datos que puede variar entre 5 y 9 bits empezando por el bit menos significativo y finalmente vienen los bits de `paridad` (que no figuran en esta comunicación) y el bit de `stop` que indica el fin del paquete.

## Donde empezar
---
Van a clonar un programa y un circuito ya armados con las cosas mínimas para que puedan enfocarse en el UART únicamente. En la carpeta `pset1/uart` escriban en la terminal:

```
git clone -b pset1/uart https://github.com/trq20/aysm6.git
```

Van a encontrar dos carpetas, una llamada `sch` con el esquemático en Proteus 8 y una llamada `src` donde van a ver un `main`, un `makefile` y una carpeta de librerías. 

## Entendiendo el programa
---
A grandes rasgos, lo que hace el programa es configurar algunos periféricos del micro para generar un control proporcional de temperatura. El micro va a leer cada 100 ms indicado por un timer dos lecturas analógicas, la de un LM35 y la de un potenciómetro, va a compararlas y luego va a generar un PWM en una de las dos salidas habilitadas para regular la velocidad del motor correspondiente a través de un MOSFET.

Pueden detenerse a leer los comentarios de cada una de las librerías si quieren para entender mas en detalle como funciona, pero lo que les va a interesar a ustedes es lo que se encuentra en `UART.h`, `UART.c` y `GPIO.c`.

En `UART.h` van a encontrarse simplemente con algunos prototipos y espacio para escribir las macros que vean necesario.

En `UART.c` van a ver cuatro funciones, una de las cuales ya se hizo. El trabajo de ustedes es armar las funciones que faltan según las especificaciones que se den.

Finalmente, en `GPIO.c` van a encontrarse con una interrupción lista, pero que no tiene nada. Esta es una interrupción externa que tiene la intención de que cada vez que se detecte un flanco ascendente en el pin, el micro mande por UART la información del LM35 y el potenciómetro.

## Especificaciones
---
Escribir el código necesario para que las funciones de `UART.c` cumplan con lo siguiente:
- `UART_Init` debe inicializar el UART para trabajar a la velocidad que se le pase como parámetro. Debe tener:
  - Un `stop` bit.
  - Sin `parity` bits.
  - Ocho bits de datos.
  - Tx habilitado pero Rx deshabilitado.
  - Polaridad normal.
  - Sin interrupciones.
  - Velocidad normal.
- `UART_Putc` debe ser capaz de enviar un **único** byte por UART, verificando los flags apropiados. 
- `UART_Prints` debe poder enviar una cadena de caracteres por UART.

Además, en la interrupción de `GPIO.c` el micro debe:
- Enviar por USART la temperatura seguido del setpoint indicado por el potenciómetro con este formato:

```
temperatura & setpoint |
```

## Orientación
---
- Para poder enviar un byte por UART, no pierdan de vista los flags `UDRE0` y `TXC0`.
- Para poder enviar una cadena, piensen en la actividad de punteros, pueden aprovecharlos.
- En cuanto a como calcular el valor que va en el registro `UBRR0` para elegir la velocidad, tienen esta ecuación que pueden usar:

$$
BAUD=\frac{f_{osc}}{16(UBRR0+1)}
$$

- En `GPIO.c` tienen las variables `temp` y `sp` que tienen guardadas la temperatura y el valor del setpoint respectivamente.
- Las dudas que tengan sobre los registros pueden aclararlas en la hoja de datos en el capítulo 17. 

## Como probar el código
---
Una vez que lo tengan resuelto, ejecuten en la terminal:

```
make -f makefile.mk
```

Si no ven errores, van a tener el `.hex` para cargar en el micro en el Proteus. La simulación debería comportarse según las especificaciones de arriba.

## Como entregar
---
Dentro de la carpeta `pset1/uart` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

```markdown
# UART

Alumno: Nombre y apellido
Curso: Curso
Materia: Computadoras y Sistemas de Control
```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add .
git commit -m "Initial commit"
git checkout -b aysm6/2021/uart/uart
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

```
git push https://github.com/trq20/USERNAME.git aysm6/2021/uart/uart
```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/aysm6/2021/uart/uart`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.
