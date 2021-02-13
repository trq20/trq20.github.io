{% include header.md %}

# Intro a Control de Interfaces
---
Bienvenidos a `Control de Interfaces`, parte del módulo de `Instrumental y Sistemas Eléctricos`. El objetivo de esta materia es ayudarles a empezar a programar y entender algunos conceptos básicos de algoritmos y resolución de problemas en distintos lenguajes de programación.

Algunas de las cosas que vamos a estar trabajando son:

- Algoritmos y programación estructurada.
- Estructuras de control, bucles, condicionales, funciones y procedimientos.
- Manejo de constantes, variables y arreglos o vectores.
- Programación de microcontroladores y control de puertos digitales y analógicos.

Vamos a arrancar usando algo de lenguaje `C` para empezar a manejar algunos de estos conceptos para mas adelante usar un lenguaje de mas alto nivel que se llama `Python`.

Para hacer todo esto, vamos a necesitar algunas herramientas:

- Algún editor de código. Hay varios dando vuelta, pero particularmente recomiendo [Visual Studio Code](https://code.visualstudio.com/).
- Instalar [Mingw](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win32/Personal%20Builds/mingw-builds/installer/mingw-w64-install.exe/download) para tener un compilador de `C` en nuestra computadora.
  - Descargar el instalador del link y ejecutarlo.
  - Verificar la instalación abriendo la terminal (en Windows, escribir `cmd` en el inicio), escribir `gcc` seguido de `enter`. Si el comando se reconoce, la instalación se hizo correctamente.

Para hacer las distintas entregas de actividades, vamos a usar `git`. Es una herramienta muy útil para desarrollo de software que permite hacer un control de versiones en repositorios. Para usarla, hacemos lo siguiente:

- Descarguen [Git para Windows](https://git-scm.com/download/win) e instálenlo. Verifiquen en la terminal de Windows la instalación escribiendo el comando `git`. Si fue correcta, tienen que ver un mensaje de ayuda.
- Creen una cuenta en [GitHub](https://github.com/) con su correo. Esta es una página muy útil para tener repositorios y poder trabajar remotamente con otras personas si fuera necesario.  
- Luego únanse al [repositorio](https://school-org-repo.herokuapp.com/) de nuestra materia ingresando su usuario de GitHub, les va a llegar una invitación para unirse al repositorio en el correo.

## Actividades
---
- [Presentación](pset0/presentacion.md).
- [Introducción a C](pset1/README.md).
- [Arrays](pset2/README.md).
- [GPIO](pset3/README.md).