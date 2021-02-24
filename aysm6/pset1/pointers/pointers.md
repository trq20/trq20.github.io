## Contexto
---
Ya hablamos en un momento de arrays. Un concepto que va de la mano, es un pointer o puntero. Este es un tipo de variable especial que almacena no un valor, sino una dirección de memoria que contiene un valor.

Veámoslo de esta manera:

```c
int num = 5443;     // Declaro una variable arbitraria
int *p;             // Declaro un puntero del tipo al que quiero apuntar
p = &num;           // Guardo en el puntero, la dirección de memoria de la variable
```

En este caso, tenemos un puntero que guarda una dirección de memoria de una variable. Los punteros se declaran con el operador `*` antes del nombre. Para almacenar la dirección, noten que usamos el operador `&` que quizás recuerden del `scanf`. Este operador equivale a decir 'la dirección de'.

La otra parte de esto, es que el puntero no solo nos sirve para almacenar una dirección de memoria, sino que también podemos ver el contenido al que apunta usando nuevamente el operador `*`. Con este ejemplo tenemos:

```c
#include <stdio.h>

int main(void) {

    int num = 5443;
    int *p;
    p = &num;

    printf("La direccion de num es %d\n", p);
    printf("El valor al que apunta *p es %d\n", *p);
    return 0;
}
```

Y el resultado es:

```
La direccion de num es 6422216
El valor al que apunta *p es 5443
```

Estas particularidades de los punteros van a ser útiles para trabajar con pasajes de variables por referencia y armar listas, pero también van a permitirnos trabajar con arrays. En el fondo, un array es un puntero a una serie de elementos. De hecho, podemos imprimir los elementos de un array de esta forma:

```c
#include <stdio.h>

int main(void) {

        int nums[] = { 1, 2, 3, 5, 6 }; // Declaro el array
        int *p;                         // Declaro el puntero
        p = nums;                       // Apunto al array
        for(int i=0 ; i < 5 ; i++) {    
            printf("%d\n", *p);         // Imprimo el contenido al que apunta *p
            p++;                        // Incremento la direccion para apuntar al  
                                        // siguiente elemento
        }
        return 0;
}
```

Noten que puedo apuntar a un elemento distinto incrementando la dirección a la que apunto, debido a que los elementos de un array están asignados de manera contigua en la memoria.

Con las cadenas de caracteres (un array de chars) pasa algo bastante particular. Recordando que una cadena de caracteres, también denominada `string`, siempre tiene un caracter adicional al final de la cadena que llamamos el caracter nulo (`\0` o `NULL`), podemos aprovechar esta particularidad para imprimir todos los caracteres de la cadena de esta forma:

```c
#include <stdio.h> 

int main(void) {

    char *str = "Hola mundo!";

    while(*str != '\0') {   // Verifico que el caracter no sea el fin de cadena
        printf("%c", *str); // Imprimo el caracter al que apunta
        str++;              // Incremento la direccion para ir al siguiente
    }
    return 0;
}
```

Esto nos permite recorrer arrays de caracteres con un bucle sin la necesidad de saber la cantidad de elementos, porque simplemente tenemos que encontrar el caracter nulo que indica el fin de cadena.

## Donde empezar
---
Dentro de la carpeta `pset1/pointers` clonen la rama `pset1/pointers` del repositorio `aysm6` donde van a encontrarse con algunas lineas de código ya escritas en un `pointers.c`. Pueden clonarlo abriendo la terminal y escribiendo:

```
git clone -b pset1/pointers https://github.com/trq20/aysm6.git
```

## Entendiendo el programa
---
El programa es sencillo, simplemente al ejecutarse, espera que le pasen una cadena de caracteres. La tarea de ustedes, es imprimir esa cadena usando punteros. Ejemplo, si el programa se ejecuta como:

```
./pointers Hola mundo!
```

El resultado debe ser:

```
Hola mundo!
```

## Especificaciones
---
Usando punteros, el algoritmo que escriban debe ser capaz de imprimir la cadena que se ejecute junto con el programa.

## Orientación
---
- Recuerden que `argc` les indica la cantidad de comandos (cadenas separadas por espacios) que fueron ejecutadas.
- La variable `argv` es un array donde cada elemento es una cadena que se ingresó.
- Tienen que pensar en algún bucle que recorra todos los elementos de `argv` y otro bucle dentro que pueda recorrer la cadena usando punteros.

## Como compilar el código
---
Compilen el código escribiendo en la terminal:

```
gcc -o pointers pointers.c
```

## Como entregar
---
Dentro de la carpeta `pset1/pointers` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

```markdown
# Pointers

Alumno: Nombre y apellido
Curso: Curso
Materia: Computadoras y Sistemas de Control
```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add arrays.c README.md
git commit -m "Initial commit"
git checkout -b aysm6/2021/uart/pointers
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

```
git push https://github.com/trq20/USERNAME.git ise4/2021/uart/pointers
```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/aysm6/2021/uart/pointers`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.

