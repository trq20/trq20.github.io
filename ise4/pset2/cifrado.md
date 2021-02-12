# Cifrado
---
## Contexto
---

En el mundo de la informática muchas veces es necesario encriptar claves o información para protegerla. Esto se hace mediante distintos tipos de cifrados o encriptados. Estos son algoritmos que como entrada reciben una cadena de caracteres que se desea encriptar y una clave, dependiendo de como funcione, como salida va a devolver una nueva cadena de caracteres cifrada de acuerdo a lo que diga la clave.

El objetivo de este problema es poder hacer un algoritmo de cifrado sencillo, que como entrada reciba una cadena y una clave de 26 caracteres que todos deben ser letras (no estamos contando la ñ) y va a tomar cada letra de la cadena de entrada y cambiarla por la que indique la clave.



## Donde empezar

---

Dentro de la carpeta `pset2/cifrado` clonen la rama `pset2/cifrado` del repositorio `ise4` donde van a encontrarse con las bases del algoritmo que van a tener que desarrollar. Para clonarlo, escriban en la terminal:

```
git clone -b pset2/cifrado https://github.com/trq20/ise4.git
```

Dentro de la carpeta que se va a clonar, van a ver un `cifrado.c` donde van a programar.



## Entendiendo el programa

---

En `cifrado.c` van a encontrarse primero con tres librerías:

- `stdio` para funciones de entrada y salida.
- `ctype` para usar funciones que traten con caracteres.
- `string` para usar funciones que traten con cadenas de caracteres.

Luego van a ver dos prototipos de funciones que van a tener que desarrollar mas adelante.

- `validar` se va a encargar de verificar de que los datos de entrada sean los correctos.
- `cifrar` se va a encargar de tomar la cadena de entrada y la clave y devolver una nueva cadena encriptada.

Dentro del `main` pueden encontrar un condicional que llama a la función `validate`. Esta parte tiene como objetivo terminar el programa si los datos de entrada fueron incorrectos. Si no lo fueron, entonces van a tener que escribir el código necesario para poder cumplir con las especificaciones que les diremos en un momento.

Luego del `main`, van a ver finalmente el espacio para poder desarrollar las funciones de `validar` y `cifrar`.



## Especificaciones

---

El algoritmo que diseñen tiene que ser capaz de:

- Admitir la clave al momento de ejecutar el programa escribiendo:

```
./cifrado clave
```

- Si la clave es válida, el programa debe mostrar un mensaje pidiendo por una cadena para cifrar.

**validar:** esta función debe encargarse de verificar que la clave ingresada sea válida para el problema. Claves válidas son:

- Las que contengan únicamente letras, independientemente de que sean mayúsculas o minúsculas.
- Las que no tengan letras repetidas.
- Las que no tengan 26 caracteres.

Si la clave no fue proporcionada o se es considerada válida, la función debe devolver 1, sino, un 0. 

**cifrar:** esta función debe tomar la clave y la cadena proporcionada y devolver una cadena encriptada. Para encriptar una cadena, la función debe:

- Evaluar cada caracter de la cadena y, de acuerdo a su orden en el alfabeto (a es 0, b es 1, etc.), reemplazarlo por el caracter que ocupe ese lugar en la clave. Es decir, si la cadena comienza con *ium* entonces la *a* es reemplazada por la *i*, la *b* por la *u* y la *c* por la *m*.
- El cifrado debe respetar las mayúsculas y minúsculas, es decir, si en la cadena hay caracteres en mayúscula, deben conservarse en mayúscula en la cadena encriptada.



## Orientación

---

[![](https://img.youtube.com/vi/ID VIDEO/0.jpg)](LINK A VIDEO)

- Recuerden que `argc` indica la cantidad de parámetros que fueron ingresados, incluyendo el `./cifrado`, mientras que `argv` es un array que tiene cada uno de esos parámetros. Si se ejecuta correctamente, `argc = 2` y `argv[1]` tiene la clave para cifrar.
- En la librería `string.h` tienen estas funciones que pueden servir:
  - `strlen` devuelve la cantidad de caracteres que tiene la cadena (no incluye el fin de cadena o `\0`).
  - `strcpy` copia un `string` a otra variable del mismo tipo siempre y cuando tenga el largo suficiente.
- En la librería `ctype` hay algunas funciones útiles:
  - `tolower` devuelve la mayúscula de la letra que se pase como parámetro.
  - `toupper` devuelve la minúscula de la letra que se pase como parámetro.
  - `islower` devuelve `true` si el caracter que se pasó como parámetro es una letra minúscula.
  - `isupper` devuelve `true` si el caracter que se pasó como parámetro es una letra mayúscula.
  - `isdigit` devuelve `true` si el caracter que se pasó como parámetro es un número.
  - `isalpha` devuelve `true` si el caracter que se pasó como parámetro es una letra.
- El caracter `\0` indica el fin de una cadena y puede ser útil para recorrerla si usamos un bucle como este:

```c
char *cadena;
int i = 0;
...
while(cadena[i] != '\0') {
    ...
    i++;
}
```

- Recuerden que cada caracter tiene un valor numérico que pueden encontrar en la tabla ASCII, busquen que valores tienen asignados las letras y evalúen como pueden usar ese valor como índice para un array.



## Como probar el código

---

Prueben los siguientes escenarios para ver si su código funciona correctamente:

- Si no escriben una clave:

```
$ ./cifrado
Uso: ./cifrado clave
```

- Si pasan una clave que no cumpla con el largo de 26 caracteres:

```
$ ./cifrado asdfghjk
La clave debe contener 26 caracteres
```

- Si pasan una clave con caracteres que no sean letras:

```
$ ./cifrado a123
La clave debe contener solo letras
```

- Si pasan una clave con letras repetidas:

```
$ ./cifrado zxcvbnmasdfghjklqwertyuioo
La clave no puede contener caracteres repetidos
```

- Si pasan una clave apropiada:

```
$ ./cifrado QwerTyuiopAsdfGhjklZxcvBnm
Texto: Este es un texto de prueba.
Cifrado: Tlzt tl xf ztbzg rt hkxtwq.
```



## Como entregar

---

Dentro de la carpeta `pset2/cifrado` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

  ```markdown
# Cifrado

Alumno: Nombre y apellido
Curso: Curso
Materia: Control de Interfaces
  ```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add cifrado.c README.md
git commit -m "Initial commit"
git checkout -b ise4/2021/arrays/cifrado
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

  ```
git push https://github.com/trq20/USERNAME.git ise4/2021/arrays/cifrado
  ```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/ise4/2021/arrays/cifrado`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.