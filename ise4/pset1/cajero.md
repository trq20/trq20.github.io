# Cajero
---

## Problema
---
Piensen en el cajero de un banco, al tener una cantidad limitada de billetes y querer reponerlos constantemente, van a diseñar algún algoritmo que pueda determinar cuantos billetes de cada valor puede entregarle a la persona para que la cantidad de billetes sea la mínima posible.

Supongan que este cajero dispone únicamente de billetes de 50, 20, 10, 5 y 1. Se acerca una persona a retirar dinero e ingresa que necesita $27, el algoritmo tiene que poder determinar que billetes darle a esta persona. El proceso lógico seria algo como esto: de 50 no podemos entregarle (es mucho mas que lo que necesita), uno de 20 es posible entregarle y ahora todavía tenemos que darle $7 (27 - 20 = 7). Uno de 10 no es posible pero si uno de 5 y nos quedan $2 (7 - 5 = 2). Finalmente, los $2 que faltan los completamos con dos billetes de 1. 

## Especificaciones
---
Implementar en un archivo `cajero.c` dentro de una carpeta `pset1/cajero` un programa que resuelva el problema planteado arriba.

El algoritmo que desarrollen debe cumplir con lo siguiente:

- El programa debe presentar un mensaje al iniciarse que pida por un monto a retirar.
- La persona debe poder ingresar un monto entero (`int`) a retirar. Pueden asumir por esta ocasión que nunca se va ingresar algo que no sea un número entero. Consideren usar algo como lo siguiente:

```c
#include <stdio.h>	// Libreria necesaria para usar scanf

...
int monto;
scanf("%d", &monto);
...
```

- El programa debe usar al menos un bucle para resolver el problema.
- Al terminar, el programa debe indicar la cantidad de cada billete que se va a entregar de la siguiente manera:

```
Cantidad de billetes de 50: 4
Cantidad de billetes de 20: 1
Cantidad de billetes de 10: 1
Cantidad de billetes de 5: 0
Cantidad de billetes de 1: 3
```

Pueden usar la función `printf` para imprimir mensajes en la consola:

```c
#include <stdio.h>	// Libreria necesaria para usar printf

...
int billetes50 = 0;
...
printf("Cantidad de billetes de 50: %d\n", billetes50);
...
```

- Resumiendo, el programa debería comportarse como en este ejemplo:

```
$ ./cajero
Ingrese el monto a retirar: 696
Billetes de 50: 13
Billetes de 20: 2
Billetes de 10: 0
Billetes de 5: 1
Billetes de 1: 1
```

## Orientación
---

  [![](https://img.youtube.com/vi/ID VIDEO/0.jpg)](LINK A VIDEO)

- Probablemente necesiten variables que cumplan el rol de contadores. Recuerden de inicializarlas en cero!
- Pueden compilar el programa que hagan con `gcc -o cajero cajero.c` y ejecutarlo con `./cajero`.

## Como entregar
---
Dentro de la carpeta `pset1/cajero` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

```markdown
# Cajero

Alumno: Nombre y apellido
Curso: Curso
Materia: Control de Interfaces
```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add cajero.c README.md
git commit -m "Initial commit"
git checkout -b ise4/2021/c/cajero
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

```
git push https://github.com/trq20/USERNAME.git ise4/2021/c/cajero
```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/ise4/2021/c/cajero`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.

