# Word
---

## Contexto
---
Muchos editores de texto como el Word tienen un algoritmo que les permite contar la cantidad de palabras y oraciones que se escribieron. El objetivo de esta actividad es desarrollar un algoritmo que nos permita contar la cantidad de oraciones y palabras que hay en un archivo de texto que les vamos a proporcionar.

## Donde empezar
---
Dentro de la carpeta `pset2/word` clonen la rama `pset2/word` del repositorio `ise4` donde van a encontrarse con las bases del algoritmo que van a tener que desarrollar además de una carpeta con algunas frases de personajes de ficción para trabajar. Para clonarlo, escriban en la terminal:

```
git clone -b pset2/word https://github.com/trq20/ise4.git
```

Dentro de la carpeta que se va a clonar, van a ver un `word.c` donde van a programar.

## Entendiendo el programa
---
En `word.c` van a encontrarse primero con tres librerías:

- `stdio` para funciones de entrada y salida.
- `ctype` para usar funciones que traten con caracteres.

Luego van a ver lo que denominamos un prototipo de función que ya está desarrollada, por lo que no tienen que preocuparse. Esta función es `read_file` y se encarga de tomar un archivo de texto y guardar el texto en un `string` que es este caso, es la variable `text`. Noten que el tamaño de esta cadena viene determinado por una etiqueta que llamamos `MAX`, este simplemente es un valor arbitrario que decidimos y que definimos con un `define` para poder encontrarlo y cambiarlo más fácil si fuese necesario.

Dentro del `main` van a ver un condicional que se encarga de verificar que el programa se ejecute correctamente con dos parámetros, siendo el primero el nombre del programa y el segundo, el nombre del archivo para leer.

Luego aparece otro condicional que llama la función `read_file`, si el archivo existe y se pudo abrir sin inconvenientes, entonces se arroja un error y se termina el programa.

Luego de esto, tienen espacio para poder escribir el algoritmo que permita resolver el problema planteado arriba.

## Especificaciones
---
El algoritmo que diseñen tiene que ser capaz de:

- Contar la cantidad de palabras en el archivo e imprimir un mensaje indicándolo. Consideren que terminó una palabra cada vez que encuentren un espacio.
- Contar la cantidad de oraciones en el archivo e imprimir un mensaje. Consideren los `.`, `!` y `?` como caracteres que indican que una oración terminó.

## Orientación
---

[![](https://img.youtube.com/vi/ID VIDEO/0.jpg)](LINK A VIDEO)

- En la librería `ctype` esta la función `isspace` que devuelve `true` si el caracter que se pasa como parámetro es un espacio.
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

- Recuerden que la última palabra de la cadena esta seguida por un `.` no un espacio.

## Como probar el código
---
Estos son algunos ejemplos de lo que deberían obtener en estos casos:

```
$ ./word frases/gandalf.txt
Cantidad de palabras: 17
Cantidad de oraciones: 1
```

```
$ ./word frases/geralt.txt
Cantidad de palabras: 46
Cantidad de oraciones: 4
```

```
$ ./word frases/roland.txt
Cantidad de palabras: 66
Cantidad de oraciones: 6
```

## Como entregar
---
Dentro de la carpeta `pset2/word` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

```markdown
# Word

Alumno: Nombre y apellido
Curso: Curso
Materia: Control de Interfaces
```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add word.c README.md
git commit -m "Initial commit"
git checkout -b ise4/2021/arrays/word
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

```
git push https://github.com/trq20/USERNAME.git ise4/2021/arrays/word
```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/ise4/2021/arrays/word`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.

