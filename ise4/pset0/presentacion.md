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

Usen los comandos de arriba para navegar en la consola hasta encontrar la carpeta `presentacion`.



## El README

---

En la terminal, escriban `touch README.md`, esto va a cread un archivo con la extensión `md` que viene de `markdown`, este es un lenguaje especial para escribir con una sintaxis bastante cómoda que GitHub reconoce y renderiza en el repositorio. Por que el nombre `README`? Porque GitHub lo usa inmediatamente en el repositorio como una muestra y cualquier persona que entre al repositorio ve eso primero.

La tarea de ustedes es presentarse en ese archivo. Mínimamente el archivo tiene que:

- Contener:
  - Nombre y apellido.
  - Edad.
  - Curso.
  - Un texto breve en donde ustedes se presenten con cualquier información que consideren relevante.
- Usar:
  - Al menos un tipo `header` y un tipo de `emphasis`.

Fuera de eso, siéntanse libres de escribir lo que quieran y usar todo lo que gusten de la sintaxis de `markdown` para que el archivo se vea bien. Pueden ver todas las herramientas [acá](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf). 

Pueden ver mi presentación en [mi repositorio](https://github.com/trq20/carlassaraf) si quieren para sacar ideas :smile: (Si van al `README` y hacen click en `raw` pueden ver el código fuente).

Pueden usar el bloc de notas, Visual Studio Code o cualquier otro editor de texto para escribir y modificar el archivo. Si tienen Git Bash, pueden modificarlo desde la misma terminal escribiendo `nano README.md`. Si prefieren, también pueden descargar [Typora](https://typora.io/#windows) que es un editor dedicado para `markdown` y tiene bastantes herramientas. Sino, pueden descargar una extensión de markdown para Visual Studio Code.



## El repositorio

---

Cuando tengan terminada la presentación, vamos a crear un repositorio y publicarlo en GitHub. Primero hay que crear el repositorio en GitHub. Para eso, visiten la cuenta a [la que se unieron](https://github.com/trq20) y busquen la opción de `New` para crear un nuevo repositorio. Algunas observaciones para lo que viene a continuación:

-  El nombre del repositorio debe ser su nombre de usuario de GitHub.
- En la opción de publico o privado, pueden elegir el que prefieran. Si lo hacen público, cualquiera que visite el url puede ver el contenido del repositorio. Si eso no les molesta, pueden hacerlo público, sino, lo ponen como privado y solo ustedes y los usuarios con permiso pueden ver el contenido.

Luego pueden crear el repositorio y van a ver una nueva pantalla. Lo importante de acá es el link que les muestra en una caja a la derecha que tiene un formato como `https://github.com/trq20/USERNAME.git` donde `USERNAME` va a ser el nombre de usuario que eligieron. Copien eso que vamos a necesitarlo en un momento.

Volviendo a la carpeta donde creamos nuestra presentación, vamos a escribir:

- `git init` para crear un repositorio local en esa ubicación.
- `git add .` para agregar el `README.md` a nuestro repositorio.
- `git commit -m "Initial commit"` como para poder guardar el estado de nuestro repositorio. 
- `git push url master` donde `url` es el que copiaron de GitHub y `master` es el nombre de la rama que vamos a publicar. Ya vamos a hablar mas en detalle de lo que son las ramas.

Si no hay errores, visiten `https://github.com/trq20/USERNAME` y deberían poder ver el repositorio publicado.