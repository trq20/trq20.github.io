# Como preparar el VS Code para compilar y programar micros de Atmel
----
El Visual Studio Code es un editor de código gratuito muy flexible que nos va a permitir escribir en lenguajes como `C/C++`, `C#`, `Javascript`, `Python`, `HTML`, `CSS` entre otros. Nos da la posibilidad de debuggear lo que programemos y una variedad de herramientas mas siempre que tengamos los complementos necesarios.
La idea de este documento es brindar una serie de pasos para preparar el VS Code para que podamos escribir código en `C/C++` para programar microcontroladores de Atmel.

## Visual Studio Code
---
El instalador pueden conseguirlo [acá](https://code.visualstudio.com/).

## Previo
---
Antes que nada, verifiquen que puedan ejecutar el comando `make`. Para eso:

1. Escriban en el inicio `cmd`, eso debería buscarles la terminal de Windows.
2. Abran la terminal y escriban `make` y enter.
3. Si la terminal les devuelve que no reconoce el comando, sigan con la siguiente sección. Si el comando lo reconoce pero da error al ejecutarlo, salteen la siguiente parte.

## Intalar MINGW
---
1. Sigan las intrucciones de este [video](https://youtu.be/wC-aHZ87sic). El link de descarga esta en la descripción.
   
## Instalar WinAVR
---
1. Consigan las herramientas de desarrollo para [Atmel](https://sourceforge.net/projects/winavr/files/latest/download).
2. Ejecuten el instalador.
