# Hola mundo!
---

## Problema
---
A modo de actividad introductoria, vamos a empezar por el programa mas sencillo que es el de poder ingresar un nombre por la consola e imprimir un saludo.

## Especificaciones
---
Implementar en un archivo `hello.c` dentro de una carpeta `pset1/hello` un programa que resuelva lo planteado arriba.

El programa debe:

- Imprimir un mensaje pidiendo el nombre de la persona que ejecuta el programa.
- Imprimir un mensaje saludando a la persona que ingresó el nombre.

El programa debe comportarse de esta manera:

```
$ ./hello
Como es tu nombre? Fabrizio
Hola Fabrizio!
```

## Orientación
---

[![](https://img.youtube.com/vi/ID)](LINK A VIDEO)

- Van a necesitar trabajar con un tipo de dato especial que en otros lenguajes se denomina `string`. Ese tipo de dato no existe en el lenguaje C, pero podemos solucionarlo temporalmente así:

```c
typedef char * string;	// Creamos el tipo de dato
...
string name;		   // Declaramos la variable 
```

- Para tratar con un `string`, sugerimos la función `gets` para poder hacerlo de forma mas sencilla:

```c
gets(name);	// Entre parentesis pasamos la variable donde queremos guardar el texto
```

## Como probar el código
---
Asegúrense de que el programa se comporte de la manera apropiada, especialmente para casos donde el que ejecute el programa tenga mas de un nombre o decida poner su nombre y apellido.

## Como entregar
---
Dentro de la carpeta `pset1/hello` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

```markdown
# Hello

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
git push https://github.com/trq20/USERNAME.git ise4/2021/c/hello
```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/tree/ise4/2021/c/hello`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.