# Como preparar el VS Code para compilar y programar micros de Atmel
El Visual Studio Code es un editor de código gratuito muy flexible que nos va a permitir escribir en lenguajes como `C/C++`, `C#`, `Javascript`, `Python`, `HTML`, `CSS` entre otros. Nos da la posibilidad de debuggear lo que programemos y una variedad de herramientas mas siempre que tengamos los complementos necesarios.
La idea de este documento es brindar una serie de pasos para preparar el VS Code para que podamos escribir código en `C/C++` para programar microcontroladores de Atmel.



## Visual Studio Code

---

El instalador pueden conseguirlo en https://code.visualstudio.com/.



## Previo

---

Antes que nada, verifiquen que puedan ejecutar el comando `make`. Para eso:
1. Escriban en el inicio `cmd`, eso debería buscarles la terminal de Windows.
2. Abran la terminal y escriban `make` y enter.
3. Si la terminal les devuelve que no reconoce el comando, sigan con la siguiente sección. Si el comando lo reconoce pero da error al ejecutarlo, salteen la siguiente parte.



## Intalar MINGW

---

1. Descarguen el ejecutable para el [MINGW](https://osdn.net/projects/mingw/downloads/68260/mingw-get-setup.exe/). Ese link debería iniciar la descarga inmediatamente.
2. Ejecuten la aplicación y permitan que se instale en el directorio por defecto (C:/MINGW).
3. Tiene que aparecer una ventana de instalación en la que va a aparecer una lista con paquetes. Eligan todos los disponibles en el *Basic Setup* y vayan a *Instalation->Aply Changes*.
4. Cuando la instalación termine, vayan al directorio donde se instaló y busquen la carpeta `bin`. Dentro, tiene que haber un archivo llamado `mingw32-make` y hagan una copia en el mismo directorio del archivo pero renombrándolo a `make`.
5. Repitan los pasos de la sección anterior.



## Instalar WinAVR

---

1. Consigan las herramientas de desarrollo para [Atmel] en (https://sourceforge.net/projects/winavr/files/latest/download).
2. Ejecuten el instalador.



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

