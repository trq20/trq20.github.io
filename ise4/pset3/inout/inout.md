# Inout
---
## Problema

---

Para comenzar a familiarizarnos con programación de microcontroladores, vamos a plantear un problema sencillo. Queremos armar un circuito que tenga un microcontrolador, dos pulsadores y dos LEDs. Cada pulsador va a controlar el comportamiento de un LED. 

El primer pulsador, cuando se oprime, debe prender el LED y al soltarlo, debe apagarlo.

El segundo pulsador, debe hacer un `toggle` del LED cada vez que se oprime, es decir, si el LED estaba apagado, al oprimirlo se debe encender y si estaba prendido, se apaga. Al soltar el pulsador, el LED debe quedar en el último estado.



## Donde empezar

---

Para poder probar el programa que hagamos, vamos a necesitar un simulador, en este caso, vamos a usar el [tinkercad](https://www.tinkercad.com/) que nos va a permitir hacer el circuito y escribir el código para el microcontrolador.

Entren al simulador, creen una cuenta y comiencen un nuevo circuito que responda al problema planteado arriba. Van a necesitar:

- Un Arduino.
- Dos pulsadores.
- Dos resistencias de 10K (de `pull-down`) y dos de 330.
- Dos LEDs.

Pueden elegir los pines que quieran para conectar todo, pero al final, debería quedarles algo como esto:

![image-20210101152033185](C:\Users\fabri\AppData\Roaming\Typora\typora-user-images\image-20210101152033185.png)

Van a notar un botón que dice *</ Código*, cuando vayan ahí, se va a abrir una pestana con bloques, vayan a la opción de *Texto* y ahí van a notar unas líneas de código ya preparadas. Borren todo excepto las funciones `setup` y `loop`.

Los que estén familiarizados con Arduino van a estar familiarizados con estos términos:

- `setup` es una función que se ejecuta una sola vez, normalmente escribimos cosas como inicialización de puertos digitales, analógicos o de comunicaciones.
- `loop` es una función que se ejecuta después del `setup` y queda permanentemente corriendo. Pueden imaginarse que es como si la función fuera un gran bucle infinito.



## Especificaciones

---

El algoritmo que diseñen tiene que ser capaz de:

- Encender y apagar un LED cada vez que se oprima y suelte un pulsador respectivamente.
- Cambiar el estado de un segundo LED cada vez que se oprima un segundo pulsador. Al soltarlo, el LED debe quedar como estaba.



## Orientación

---

[![](https://img.youtube.com/vi/ID VIDEO/0.jpg)](LINK A VIDEO)

- La función `pinMode` elige si un pin es `INPUT` o `OUTPUT`, toma como parámetros el número de pin y luego el modo.
- La función `digitalWrite` escribe un valor en un pin que este configurado como salida. Toma como parámetros el número de pin y luego el valor de la salida que puede ser `HIGH` o `LOW`.
- La función `digitalRead` toma como valor de entrada un pin que deseen leer y les devuelve `HIGH` o `LOW` dependiendo de si el pin tiene tensión o no.
- La función `delay` les permite generar un retardo en el programa. Como parámetro escriben el valor en `milisegundos` que quieren que demore.



## Como probar el código

---

Tienen la opción de correr el programa en este simulador. El microcontrolador debería responder distinto para cada pulsador:

- Para uno, al oprimirse un LED tiene que encenderse y quedarse así hasta que se suelte.
- Para el otro, el segundo LED debe cambiar de estado cada vez que se oprima el pulsador, dejándolo igual cuando se suelte.



## Como entregar

---

Una vez que su programa este andando, pueden descargar el programa desde el `tinkercad` y guárdenlo con el nombre de `inout.ino` dentro de la carpeta `pset3/inout`.

Dentro de la carpeta `pset3/inout` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

  ```markdown
# Inout

Alumno: Nombre y apellido
Curso: Curso
Materia: Control de Interfaces

[Imagen del circuito]
  ```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add inout.ino README.md
git commit -m "Initial commit"
git checkout -b ise4/2021/gpio/inout
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

  ```
git push https://github.com/trq20/USERNAME.git ise4/2021/gpio/inout
  ```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/ise4/2021/gpio/inout`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.

