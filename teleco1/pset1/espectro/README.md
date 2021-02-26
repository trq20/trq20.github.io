# Espectro electromagnético
---

## Contexto
---
El espectro electromagnético es una gran clasificación de bandas de frecuencias de acuerdo a sus usos o características que presentan. Hay clasificaciones mas extensas, pero vamos a quedarnos con una bastante sencilla y mas adelante vamos a explorar un poco mas una parte del espectro que es el radioeléctrico. Este último nos va a interesar mas porque es donde se dan la mayor parte de las comunicaciones hoy.

## Donde empezar
---
Dentro de la carpeta `pset1/espectro` clonen del repositorio `teleco1` la rama `pset1/espectro`. Escriban en la terminal:

```
git clone -b pset1/espectro https://github.com/trq20/teleco1.git
```

Van a encontrar un `espectro.csv` y un `espectro.py`. El primero es un archivo separado por comas, pueden abrirlo con Excel o con cualquier editor de texto. Imagínenlo como una tabla con este formato:

| Banda | Longitud de onda | Frecuencia | Uso |
| ----- | ---------------- | ---------- | --- |
| Banda 1 | Un rango de longitud en m | Un rango de frecuencia en Hz | Un ejemplo de uso |

Solo la columna de banda y longitud de onda están completas para darles la información para comenzar. La primer tarea de ustedes es primero completar las dos que faltan.

Una vez que tengan completa la tabla, pueden ver `espectro.py` en donde van a tener algunas cosas ya listas. Este script de Python se va a encargar de tomar cada fila de la tabla y armar una lista de diccionarios. Se va a ver algo parecido a esto:

``` python
{'Banda': 'Rayos gamma', 'Longitud de onda': ' < 10pm', 'Frecuencia': None, 'Uso': None}
{'Banda': 'Rayos X', 'Longitud de onda': ' < 10nm', 'Frecuencia': None, 'Uso': None}
{'Banda': 'Ultravioleta', 'Longitud de onda': ' < 380 nm', 'Frecuencia': None, 'Uso': None}
{'Banda': 'Visible', 'Longitud de onda': ' < 780nm', 'Frecuencia': None, 'Uso': None}
{'Banda': 'Infrarrojo', 'Longitud de onda': ' < 1mm', 'Frecuencia': None, 'Uso': None}
{'Banda': 'Microondas', 'Longitud de onda': ' < 10cm', 'Frecuencia': None, 'Uso': None}
{'Banda': 'Radio', 'Longitud de onda': ' > 10cm', 'Frecuencia': None, 'Uso': None}
```

Noten que primero hay un campo al que llamamos `key` (en este caso son Banda, Longitud de Onda, Frecuencia y Uso) y seguido de `:` viene el valor correspondiente.

La segunda tarea de ustedes es completar el script de Python para que tome como entrada un `string` que debiera ser el nombre de una banda (ejemplo Ultravioleta) y, si la banda esta en la lista, entonces imprimir en la consola toda la información de esa banda. Si no existe, imprimir un mensaje indicándolo.

## Orientación
---
- La función `input` imprime un mensaje en la consola y devuelve el string que el usuario haya ingresado:

```python
entrada = input("Ingrese una banda: ") # En entrada se guarda lo que el usuario ingrese
```
- La función `print` permite mostrar un mensaje o variable en pantalla.

```python
print("Este mensaje va a salir por la consola")
```

- Se puede tomar el valor de una de las entradas de un diccionario accediendo con el key que corresponda. Por ejemplo:

```python
dict = {'Key' : 'Valor', 'OtraKey' : 'Este es un diccionario' }
print(f'{dict["OtraKey"]}, el valor de Key es {dict["Key"]}')
```

El resultado es:

```
Este es un diccionario, el valor de Key es Valor
```

- Pueden encontrar ayuda para formatear strings en esta [página](https://www.w3schools.com/python/ref_string_format.asp).

## Como probar el código
---
- Si como entrada se ingresa algo como "Banda X" deberíamos ver un mensaje como "Esa banda no existe".
- Si como entrada ponemos una banda que si existe, deberíamos ver la información con este formato:

```
Banda : Visible
Longitud de onda :  < 780nm
Frecuencia : None
Uso : None
```

## Como entregar
---
Dentro de la carpeta `pset1/espectro` escriban en la consola `git init`. Luego, creen un archivo llamado `README.md`. El archivo debe tener lo siguiente:

```markdown
# Espectro

Alumno: Nombre y apellido
Curso: Curso
Materia: Telecomunicaciones I

## Tabla
[La tabla completa del csv]
```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add README.md espectro.py
git commit -m "Initial commit"
git checkout -b teleco1/2021/intro/espectro
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

```
git push https://github.com/trq20/USERNAME.git teleco1/2021/intro/espectro
```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/teleco1/2021/intro/espectro`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.