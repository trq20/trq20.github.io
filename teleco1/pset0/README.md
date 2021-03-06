# Presentación
---
El objetivo de esta actividad es poder usar `git` y crear su primer repositorio en GitHub. Elijan un lugar donde crear una carpeta nueva con el nombre `presentacion`.  Lo siguiente pueden hacerlo de dos formas:

## Git Bash
---
Al instalar `git`, debería haberse instalado una consola especial que pueden usar. Dentro de la carpeta `presentacion`, hagan click derecho y tendrían que poder ver una opción que diga `Git Bash Here`.

## Command Promt
---
Abran la terminal de Windows.

- Al abrir la terminal, van a ver un `C:\Usuarios\nombre>`, esto nos dice a donde la terminal apunta en este momento.
- El comando `ls` nos lista todos los archivos y carpetas en el directorio actual.
- El comando `cd` nos permite cambiar de directorio. Si escribimos un nombre seguido del comando, la consola va a intentar entrar a ese directorio (si existe). Si el comando es seguido de `.` entonces la consola va a ir un directorio hacia atrás.

Usen los comandos de arriba para navegar en la consola hasta encontrar la carpeta `presentacion`. Si tienen dudas de como usar la consola de Windows, pueden ver [este video](https://youtu.be/VPBe7yTWPD4).

## El README
---
En la terminal, escriban `touch README.md`, esto va a crear un archivo con la extensión `md` que viene de `markdown`, este es un lenguaje especial para escribir con una sintaxis bastante cómoda que GitHub reconoce y renderiza en el repositorio. Por que el nombre `README`? Porque GitHub lo usa inmediatamente en el repositorio como una muestra y cualquier persona que entre al repositorio ve eso primero.

La tarea de ustedes es presentarse en ese archivo. Mínimamente el archivo tiene que:

- Contener:
  - Nombre y apellido.
  - Edad.
  - Curso.
  - Un texto breve en donde ustedes se presenten con cualquier información que consideren relevante.
- Usar:
  - Al menos un tipo `header` y un tipo de `emphasis`.

Fuera de eso, siéntanse libres de escribir lo que quieran y usar todo lo que gusten de la sintaxis de `markdown` para que el archivo se vea bien. Pueden ver todas las herramientas [acá](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf). 

Pueden ver mi presentación en [mi repositorio](https://github.com/trq20/carlassaraf) si quieren para sacar ideas (Si van al `README` y hacen click en `raw` pueden ver el código fuente).

Pueden usar el bloc de notas, Visual Studio Code o cualquier otro editor de texto para escribir y modificar el archivo. Si tienen Git Bash, pueden modificarlo desde la misma terminal escribiendo `nano README.md`. Si prefieren, también pueden descargar [Typora](https://typora.io/#windows) que es un editor dedicado para `markdown` y tiene bastantes herramientas. Sino, pueden descargar una extensión de markdown para Visual Studio Code.

## El repositorio
---
Para continuar, asegúrense de que tienen el repositorio creado en la cuenta de GitHub. Pueden verificarlo visitando `http://github.com/trq20/USERNAME` con `USERNAME` como su nombre de usuario de GitHub o entrando al enlace que se les envió por correo. Si la pagina no existe y ya habían completado este [formulario](https://docs.google.com/forms/d/e/1FAIpQLSe2m_H-AmedQ_1u3ikfkPpQdamA2jGEHe3EnPI63YXIZo1Jvw/viewform), entonces den aviso para que se pueda solucionar.

Volviendo a la carpeta donde creamos nuestra presentación, vamos a escribir:

- `git init` para crear un repositorio local en esa ubicación.
- `git add .` para agregar el `README.md` a nuestro repositorio.
- `git commit -m "Initial commit"` como para poder guardar el estado de nuestro repositorio. 
- `git push https://github.com/trq20/USERNAME.git master` donde `USERNAME` es su nombre de usuario y `master` es el nombre de la rama que vamos a publicar. Ya vamos a hablar mas en detalle de lo que son las ramas.

Si no hay errores, visiten `https://github.com/trq20/USERNAME` y deberían poder ver el repositorio publicado.

Cuando terminen, completen este [formulario](https://docs.google.com/forms/d/e/1FAIpQLScs8MRhBWhsKbzUdhfP5C_rvg_01PuGeXc3i3AJLqv78FQ02w/viewform).