## El Makefile
---
1. Creen una carpeta nueva donde van a iniciar un nuevo proyecto y abran esa carpeta con el VS Code.
2. Creen un nuevo archivo en esa carpeta y nómbrenlo `Makefile.mk`, este va a ser el archivo con las reglas para compilar nuestro programa.
3. En ese archivo, copien el siguiente contenido:

```Makefile
MCU=atmega328p
PART=m328p
F_CPU=1000000
CC=avr-gcc
OBJCOPY=avr-objcopy
CFLAGS=-std=c99 -Wall -g -Os -mmcu=${MCU} -DF_CPU=${F_CPU} -I.
TARGET=main
SRCS=main.c
PROGRAMMER=usbasp

all:
    ${CC} ${CFLAGS} -o ${TARGET}.bin ${SRCS}
    ${OBJCOPY} -j .text -j .data -O ihex ${TARGET}.bin ${TARGET}.hex

flash:
    avrdude -p ${PART} -c ${PROGRAMMER} -U flash:w:${TARGET}.hex:i
```

**Nota:** Respeten las tabulaciones al copiar lo de arriba o va a haber problemas al correr el `make`.

4. Guarden este archivo y creen uno adicional con el nombre `main.c` y copien lo siguiente:

```C
#include <avr/io.h>

int main (void) {

    while (1) {

    }
    return 0;
}
```

5. Guarden el archivo y ahora en la terminal del VS Code ejecuten el comando `make -f Makefile.mk`. Si todo salió bien, tiene que haber aparecido un nuevo archivo con el nombre de `main.hex`. 

## Algunas aclaraciones
---
Si llegaron hasta acá, ya están en condiciones de poder compilar programas para micros de Atmel. Las próximas aclaraciones son para ayudarles a entender a grandes rasgos el Makefile y saber que cosas cambiar cuando las circunstancias lo requieran.

Este archivo es básicamente una lista de reglas de compilación, que nos va a ahorrar el trabajo de escribir todos los comandos cada vez que necesitemos compilar. Hay dos secciones, primero hay una serie de definiciones todas en mayúscula y después hay una serie de instrucciones bajo las etiquetas `all` y `flash`. Noten que en lo último, en las instrucciones aparecen entre llaves las mismas definiciones que arriba, por eso, si nuestras condiciones cambian, lo único que hay que cambiar en el archivo es la definición correspondiente.

Las definiciones que podría llegar a ser necesario cambiar son:

- **MCU:** El nombre del microcontrolador que estamos usando.
- **PART:** Es un código asociado al microcontrolador que vamos a usar. Para no hacer extenso el documento, pueden entrar a ver la lista de microcontroladores disponibles con su correspondiente código [aquí](https://www.nongnu.org/avrdude/user-manual/avrdude_4.html#Option-Descriptions).
- **F_CPU:** La frecuencia a la que queremos que corra el microcontrolador.
- **TARGET:** El nombre con el que va a salir el `.hex`.
- **SRCS:** Lista de source files (`.c` o `.cpp`) para compilar, suponiendo que tengamos alguno aparte del `main.c` (como alguna libreria).

Ahora pueden ver un ejemplo de como se vería un Makefile para un ATmega2560, con algunas librerias y otra frecuencia de trabajo:

```makefile
MCU=atmega2560
PART=m2560
F_CPU=8000000
CC=avr-gcc
OBJCOPY=avr-objcopy
CFLAGS=-std=c99 -Wall -g -Os -mmcu=${MCU} -DF_CPU=${F_CPU} -I.
TARGET=project1
SRCS=main.c ADC.c LCD.c PWM.c
PROGRAMMER=usbasp

all:
    ${CC} ${CFLAGS} -o ${TARGET}.bin ${SRCS}
    ${OBJCOPY} -j .text -j .data -O ihex ${TARGET}.bin ${TARGET}.hex

flash:
    avrdude -p ${PART} -c ${PROGRAMMER} -U flash:w:${TARGET}.hex:i
```

