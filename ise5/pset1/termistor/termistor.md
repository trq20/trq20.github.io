

# Termistor

## Problema

---

Los termistores son resistores variables por temperatura. Hay dos tipos:

- `PTC`: Positive Temperature Coefficient, donde el valor de resistencia aumenta con la temperatura. Son particularmente útiles para aplicaciones que requieran protección por sobre corriente o auto regulación térmica.
- `NTC`: Negative Temperature Coefficient, donde el valor de resistencia disminuye con la temperatura. Son mas usados en sistemas de control de temperatura.

En esta aplicación, vamos a usar un NTC para hacer una medición de temperatura. La curva de transferencia del termistor se ve así:

![](https://images.squarespace-cdn.com/content/v1/5ab541ef70e802ff969fb817/1560975278671-VH9T4JNPSWVM7KKMQN7R/ke17ZwdGBToddI8pDm48kIqK6i8kpAv-mU8h-BPM-B9Zw-zPPgdn4jUwVcJE1ZvWQUxwkmyExglNqGp0IvTJZUJFbgE-7XRK3dMEBRBhUpwnVk7ZqrCag1uAnU7ZS_rtaprZxICTRXZ27_h5u6Sr-yiD--DDRTvrufcM8m58Xi8/ResistancevsTemperature.png)

La tarea de ustedes es obtener la temperatura que indique el NTC a partir de la resistencia que presenta. Como el microcontrolador no puede medir resistencia directamente, vamos a armar un divisor de tensión, medir la caída de tensión que presenta el termistor y obtener el valor de temperatura, mostrándolo en un LCD.

Recuerden que un divisor de tensión se calcula como:
$$
V_{NTC} = V_{CC} \frac{R_{NTC}}{R_{NTC} + R}
$$
Donde: 

- `VNTC` es la tensión que miden en el microcontrolador. 
- `VCC` es la fuente. 
- `R` es un valor de resistencia conocido que elijan. 

Despejando de esa formula, pueden obtener el valor de resistencia del NTC. 

Con ese valor de resistencia, queda encontrar el valor de temperatura que corresponde según el gráfico. Hay varias formas de matemáticamente obtener esa curva, pero la mas sencilla de manejar es:
$$
R_{(T)}=R_{(T_0)}e^{\beta(\frac{1}{T}-\frac{1}{T_0})}
$$
Donde: 

- `R(T)` es el valor de resistencia que acaban de medir.
- `R(T0)` es un valor de resistencia para un valor de temperatura específico que da el fabricante.
- `β` es una constante en grados Kelvin que da el fabricante.
- `T0` es el valor de temperatura para `R(T0)` (usualmente 25 °C).
- `T` es el valor de temperatura que estamos buscando.

Pero la fórmula de arriba no nos sirve para descubrir el valor de temperatura, entonces, despejando obtenemos la fórmula que vamos a usar:
$$
T= \frac{T_0 \beta}{T_0 \log(\frac{R_{(T)}}{R_{(T_0)}}) + \beta}
$$


## Donde empezar

---

Dentro de la carpeta `pset1/termistor` clonen la rama `pset1/termistor` del repositorio `ise5` donde van a encontrarse con las bases del algoritmo que van a tener que desarrollar. Para clonarlo, escriban en la terminal:

```
git clone -b pset1/termistor https://github.com/trq20/ise5.git
```

Dentro de `main.cpp` es donde van a empezar a trabajar, van a tener también una carpeta con las librerías habituales y el makefile para compilar.



## Entendiendo el programa

---

Además de las librerías habituales, se incluye `math.h` para que puedan usar la función `log()` para calcular la temperatura.

Luego van a ver tres constantes que son propias del NTC que vamos a usar:

```c
const uint16_t B = 3.9E3;	// El beta de la formula, en grados Kelvin
const uint16_t T0 = 298;	// T0 que es 25 °C pero lo ponemos en Kelvin
const uint16_t R = 10E3;	// R(T0)
```

El trabajo de ustedes va a ser tomar la medición de tensión del termistor y poder hacer los cálculos necesarios para mostrar el valor de resistencia que presenta y la temperatura en el LCD.



## Circuito y simulación

---

El circuito van a tener que diseñarlo y simularlo en Proteus. Los componentes que van a necesitar mínimamente son:

- ATmega328P.
- NTC (busquen el código NCP21XV103).
- LCD 16x2 (aparece en la librería de Proteus con el nombre LM016L).
- Una resistencia de un valor arbitrario para que puedan armar el divisor de tensión.

Son libres de decidir que pines del microcontrolador usar. Algunas aclaraciones:

- Sobre el LCD:
  - `VDD` y `VEE` van a `5V`.
  - `VSS` y `RW` van a `GND`.
  - `D0-D3` no se conectan.
  - `RS`, `E`, `D4-D7` van al microcontrolador en el orden que prefieran.
- Recuerden que los pines analógicos son `PC0-PC6`.
- Los pines `AVCC` y `RESET` del microcontrolador deben ir a `5V`.

Una vez que tengan el circuito armado y el programa compilado, tienen que hacer doble click en el microcontrolador o click derecho y propiedades y en *Program file* cargar el `.hex` que obtuvieron al compilar. Una vez que esto lo tengan, simulan el circuito dando inicio con el botón que está en la esquina inferior izquierda.



## Especificaciones

---

Al simularlo, el programa debe mostrar: 

- En la primer fila del LCD el valor de resistencia del NTC.
- En la segunda fila el valor de temperatura en grados centígrados.

Pueden modificar la temperatura en las propiedades del NTC.



## Orientación

---

[![](https://img.youtube.com/vi/ID VIDEO/0.jpg)](LINK A VIDEO)

- Pueden mirar esta [página](https://www.notion.so/Librer-as-153c030dc4874e12a9fbd75a49dd08a0) para entender mejor como funcionan las librerías y que funciones pueden usar.  

- Recuerden que el valor que reciban de la función `analogRead` es un número entero que es proporcional a la temperatura, pero necesita que le hagan una conversión. Pueden pensarlo así:

```c
uint16_t val = analogRead(0);			   // Devuelve un numero entre 0 y 1023
float tension = (float)val * REF / 1023;	// Valor de tension que en el pin
```

Esto puede hacerse de forma mas compacta, pero la idea es que tenemos que hacer la lectura, luego convertirla a tensión con la relación de la segunda linea (donde `REF` es el valor de tensión de referencia que elegimos). 

- Recuerden que pueden fijar una tensión de referencia mas apropiada para mejorar la precisión de la medición si arman un divisor de tensión y conectan esa tensión al pin `AREF` del microcontrolador.

- La formula para calcular la temperatura la devuelve en grados Kelvin, necesitan hacer la conversión a grados centígrados.

$$
T[C] = T[K]-273
$$



## Como probar el código

---

Una vez que terminen el programa, vayan a la terminal, asegúrense de que esta apunte a la carpeta donde están trabajando y escriban `make -f makefile.mk`. Si todo está en orden, tienen que ver este mensaje:

```
$ make -f makefile.mk
avr-gcc -Wall -g -Os -mmcu=atmega328p -DF_CPU=1000000 -I. -o ntc.bin main.cpp libs/analog.cpp libs/LCD.cpp libs/digital.cpp -lm
avr-objcopy -j .text -j .data -O ihex ntc.bin ntc.hex
```

Y luego, van a ver que algunos archivos nuevos van a aparecer, uno de ellos es el `ntc.hex`, este contiene la traducción de nuestro código a instrucciones en hexadecimal que vamos a grabar en la flash del microcontrolador.

En el Proteus, vayan a las propiedades del microcontrolador y en *Program file* carguen el `ntc.hex`. Luego den inicio a la simulación con el botón en la esquina inferior izquierda.



## Como entregar

---

Dentro de la carpeta `pset1/termistor` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

  ```markdown
# Termistor

Alumno: Nombre y apellido
Curso: Curso
Materia: Adquisicion de Datos

[Imagen del circuito]
  ```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add .
git commit -m "Initial commit"
git checkout -b ise5/2021/temperatura/termistor
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

  ```
git push https://github.com/trq20/USERNAME.git ise5/2021/temperatura/termistor
  ```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/ise5/2021/temperatura/termistor`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.

