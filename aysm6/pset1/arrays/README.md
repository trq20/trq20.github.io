# Arrays
---

## Contexto
---
Los arrays o arreglos, también a veces llamados vectores, son un conjunto de elementos del mismo tipo (`int`, `float`, `char`, etc) bajo el mismo nombre. Tienen una estructura de este tipo:

| Índices | [0] | [1] | [2] | ... | [n-1] |
| ------  | --- | --- | --- | --- | ----- |
| Elemento | 5 | 123 | 5432 | ... | 99 |

Noten que hay un índice y un elemento. El primero indica la posición del elemento dentro del arreglo. Lo que ven arriba, es un arreglo de `n` elementos, donde el 5 es el elemento 0, el 123 el elemento 1, el 5432 el elemento 2 y el 99 el elemento `n-1`. Vean que aunque hay `n` elementos, el último es el `n-1` ya que arrancamos a contar desde 0. Como decíamos antes, todos los elementos son del mismo tipo, en este caso, `int`.

Los arreglos se pueden declarar de la siguiente forma:

```c
int ints[5];                                // Arreglo de enteros de cinco elementos
char chars[] = "Hi";                        // Arreglo de dos caracteres ya llenado
float floats[3] = { 1.2, 3.14, 75.433 };    // Arreglo de tres float ya llenado
```

Pueden llenarse con valores determinados al momento de declararse o llenarse luego de acuerdo a las circunstancias. El caso del arreglo de caracteres es uno que vamos a analizar en detalle en la próxima actividad. Luego se puede acceder al elemento en particular indicando el índice del mismo:

```c
printf("%f", floats[1]);    // Imprimiria el 3.14 por ser el elemento 1
```

## Donde empezar
---
Dentro de la carpeta `pset1/arrays` clonen la rama `pset1/arrays` del repositorio `aysm6` donde van a encontrarse con algunas lineas de código ya escritas en un `array.c`. Pueden clonarlo abriendo la terminal y escribiendo:

```
git clone -b pset1/arrays https://github.com/trq20/aysm6.git
```

## Entendiendo el programa
---
El programa es sencillo, simplemente al ejecutarse, espera que le indiquen la cantidad de elementos y luego declara un array con esa cantidad. 
Vean que el `main` tiene dos argumentos de entrada que vamos a aprovechar. Ambos argumentos son pasados al main en el momento que ejecutan el programa. 

El `argc` me indica la cantidad de comandos que se ejecutaron al llamar el programa. Por ejemplo, si solo lo ejecutáramos, escribiríamos en la consola:

```
./arrays
```

En este caso, `argc = 1`. Pero para que este programa ande, necesitamos pasarle la cantidad de elementos que queremos, entonces vamos a correrlo así:

```
./arrays 5
```

Donde 5 es la cantidad de elementos que queremos en el array. En este caso, `argc = 2`.

De ahí el if que van a ver al principio del programa, que se asegura de que cuando lo ejecuten, el programa no siga si no se indica la cantidad de elementos.

El `argv` es un array de caracteres, y contiene los comandos que se corrieron. En el caso del ejemplo de arriba, `argv` contiene dos elementos: `./arrays` y `5`.

Finalmente lo que hacemos con ese número es convertirlo a entero (porque es un caracter al haber sido ingresado por consola) y declaramos el array. Lo que sigue es trabajo de ustedes.

## Especificaciones
---
El algoritmo que escriban debe ser capaz de:
- Pedir al usuario que llene el array.
- Preguntar por un elemento del array e imprimirlo.

## Orientación
---
- Pueden usar `scanf` para guardar un valor por consola en una variable. Ejemplos [aquí](https://www.tutorialspoint.com/c_standard_library/c_function_scanf.htm).
- Pueden usar `printf` para imprimir mensajes en la consola para indicarle al usuario que hacer. Ejemplos [aquí](https://www.tutorialspoint.com/c_standard_library/c_function_printf.htm).
- Para llenar el array, pueden pensar en un bucle que recorra elemento por elemento del array y se detenga en cada uno a preguntar al usuario con que lo quiere llenar. Ejemplos [aquí](https://www.tutorialspoint.com/cprogramming/c_arrays.htm).

## Como probar el código
---
Pueden compilar el código escribiendo en la terminal:

```
gcc -o arrays arrays.c
```

Y luego van a ver aparecer un `arrays.exe` que pueden ejecutar desde la consola escribiendo `./arrays`.

Salvando las diferencias en como decidan dar las instrucciones y los mensajes, el programa debería comportarse de esta manera:

```
$ ./arrays 4
Ingrese un valor para el elemento 0: 2
Ingrese un valor para el elemento 1: 3
Ingrese un valor para el elemento 2: 4
Ingrese un valor para el elemento 3: 5
Elija el elemento que quiera (0-3): 2
El elemento 2 es el: 4
```

## Como entregar
---
Dentro de la carpeta `pset1/arrays` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

```markdown
# Arrays

Alumno: Nombre y apellido
Curso: Curso
Materia: Computadoras y Sistemas de Control
```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add arrays.c README.md
git commit -m "Initial commit"
git checkout -b aysm6/2021/uart/arrays
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

```
git push https://github.com/trq20/USERNAME.git aysm6/2021/uart/arrays
```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/aysm6/2021/uart/arrays`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.

