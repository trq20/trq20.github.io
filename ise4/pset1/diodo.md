# Diodo
---
## Contexto

---

Los circuitos con diodos matemáticamente acarrean inconvenientes que hacen que hasta los circuitos mas sencillos sean complejos de resolver. Analicemos lo que ocurre en el circuito de abajo:

![Circuito Diodo](https://web.njit.edu/~pereira/EE291/images/291-9-1.gif) 

Suponiendo que conocemos la tensión de la fuente y el valor de la resistencia, podemos expresar la siguiente ecuación:
$$
I_D = \frac{V_S-V_D}{R}
$$
Pero al mismo tiempo, la corriente en el diodo se expresa de la siguiente forma:
$$
I_D = I_S (e^{\frac{V_D}{V_T}}-1)
$$
Donde `Is` es la corriente de saturación del diodo, `VT` es normalmente `25 mV` y `VD` es la tensión del diodo que aparece en la primer ecuación. Este circuito queda entonces gobernado por dos ecuaciones, las cuales, si quisiéramos resolver por los métodos habituales como igualación o sustitución, resultan imposibles por la naturaleza exponencial de la segunda.

Esto nos deja con dos posibilidades, o resolvemos el problema gráficamente (graficamos ambas ecuaciones y buscamos el cruce) o usamos un método iterativo, esto es, elegir un valor de `VD`, reemplazarlo en una de las ecuaciones y verificarlo en la segunda, continuando el proceso y ajustando la variable hasta que ambas ecuaciones den igual.

Este método es muy tedioso resolverlo a mano porque requiere a veces muchas iteraciones, pero la tarea de ustedes hoy va a ser diseñar un algoritmo que nos facilite esta tarea.



## Donde empezar

---

Dentro de la carpeta `pset1/diodo` clonen el la rama `pset1/diodo` del repositorio `ise4` donde van a encontrarse con parte de los datos para resolver el problema. Escriban en la terminal:

```
git clone -b pset1/diodo https://github.com/trq20/ise4.git
```

Y dentro de la carpeta que se va a clonar, van a ver un `diodo.c` donde van a programar.



## Entendiendo el programa

---

Dentro de `diodo.c` van a ver dos `#include` a las librerías `stdio` y `math`, donde la primera nos dejaba usar funciones como `scanf` y `printf` mientras que la segunda nos va a permitir resolver la exponencial con la función `exp`.

Luego van a ver un par de constantes y variables ya definidas. La palabra `const` define que el valor que tenemos a la derecha no puede cambiar en todo el programa, en este caso, vamos a tener una constante para la corriente de saturación del diodo y otra para la fuente. Luego tenemos una variable que va a representar a la tensión del diodo. Le dimos un valor inicial porque sabemos por experiencia que el valor final va estar cerca de esos valores para darles una ayudita de entrada.

Noten que el valor de la resistencia no esta definida, eso es porque van a tener que pedirla como parámetro de entrada.

Las cosas mencionadas arriba **no las deben cambiar**, abajo van a tener espacio para resolver el problema que tienen por delante.



## Especificaciones

---

El algoritmo que diseñen tiene que ser capaz de:

- Mostrar un mensaje pidiendo por un valor de resistencia (puede ser entero si así lo prefieren) y guardarlo en una variable. Asuman que el valor de resistencia siempre va a ser válido.
- Encontrar la tensión del diodo y la corriente que circula en el circuito.
  - En el caso de la tensión, van a tener que partir de la `VD` dada, resolver las ecuaciones planteadas arriba y comparar las corrientes obtenidas en ambos casos, si son iguales, entonces resolvieron el problema! Sino, tienen que hacer un ajuste en `VD` aumentando o disminuyendo su valor y volver a iterar.
- Una vez encontrado el valor de ambas incógnitas, el programa tiene que imprimir un mensaje indicando cuales son esos valores con una precisión de **dos decimales**. 

Acá tienen un ejemplo de como debería comportarse el programa:

```
$ ./diodo
Ingrese el valor de resistencia del circuito: 330
El valor de VD es 0.32 V
La corriente que circula es de 14.95 mA
```



## Orientación

---

[![](https://img.youtube.com/vi/ID VIDEO/0.jpg)](LINK A VIDEO)

- Van a necesitar usar la función `exp` de la librería `math.h`. Piénsenla así:

```c
double id = is * (exp(e) - 1);
```

- Estamos tratando de encontrar un valor de `VD` para el que dos ecuaciones se hacen iguales, pero es muy complicado que numéricamente encontremos el valor exacto, por eso, sugerimos que puedan evaluar la parte 'entera' del valor. Por ejemplo:

```c
int id1_int = id1 * 1000;	//	id que obtenemos de una de las ecuaciones expresada como entero	
```

La razón por la que multiplicamos por 1000 ese valor es porque normalmente estas corrientes están en el orden de los mili amperes, por lo que son pequeñas para poder expresarlas como enteros. 

- Pueden compilar el programa que hagan con `gcc -o cajero cajero.c` y ejecutarlo con `./cajero`.
- Si al ejecutar el programa notan que nunca devuelve un resultado, probablemente es porque no logre encontrar una solución al problema y va a ser necesario hacer que los ajustes de `VD` sean mas chicos.



## Como probar el código

---

Les ofrecemos algunos ejemplos con los que pueden comparar para saber si su algoritmo esta resolviendo bien este problema:

| R [Ohm] | VD [V] | ID [mA] |
| ------- | ------ | ------- |
| 100     | 0.34   | 46.92   |
| 330     | 0.32   | 14.95   |
| 2200    | 0.28   | 2.99    |



## Como entregar

---

Dentro de la carpeta `pset1/diodo` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

  ```markdown
# Diodo

Alumno: Nombre y apellido
Curso: Curso
Materia: Control de Interfaces
  ```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add diodo.c README.md
git commit -m "Initial commit"
git checkout -b ise4/2021/c/diodo
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

  ```
git push https://github.com/trq20/USERNAME.git ise4/2021/c/diodo
  ```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/ise4/2021/c/diodo`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.

