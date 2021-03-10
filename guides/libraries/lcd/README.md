## LCD Display
---
Esta librería es para poder trabajar con Displays LCD de 16x2. De momento, solamente funciona para ese tipo de display y con cuatro bits de datos, no ocho. En `LCD.cpp / LCD.h` se define la clase `LCD` y vamos a hablar de los métodos que tiene. Los atributos son privados así que no pueden modificarse.

## Funciones
---
### LCD(rs, en, d4, d5, d6, d7)
---
Este es el constructor de clase y toma seis parámetros que son todos números de pin a los que conectaremos los pines del LCD.

```cpp
LCD lcd(2, 3, 4, 5, 6, 7); // RS -> pin 2 | EN -> pin 3 | D4 -> pin 4  
		                       // D5 -> pin 5 | D6 -> pin 6 | D7 -> pin 7
```

### clear()
---
Este método hace que el LCD se limpie de los caracteres que haya y vuelva el cursor al comienzo del display.

```cpp
LCD lcd(2, 3, 4, 5, 6, 7);
lcd.clear();
```

### setXY(x, y)
---
Ubica el cursor en la posición determinada, donde `x` indica la columna e `y` la fila. Recuerden que es un display de 16x2 así que contando desde cero, podemos ir de 1 a 16 columnas y 1 a 2 filas.

```cpp
LCD lcd(2, 3, 4, 5, 6, 7);
lcd.setXY(2, 6);    // El cursor se desplaza a la segunda fila, sexta columna
```

### putC(ch)
---
Imprime un único caracter en la pantalla en la posición actual del cursor.

```cpp
LCD lcd(2, 3, 4, 5, 6, 7);
lcd.putC('H');  
```

### print(str)
---
Imprime una cadena de caracteres en el LCD.

```cpp
LCD lcd(2, 3, 4, 5, 6, 7);
lcd.print("Hola mundo!")    
```

### print(int32_)
---
Imprime un número entero con signo en el LCD.

```cpp
LCD lcd(2, 3, 4, 5, 6, 7);
lcd.print(-2356);
```

### print(uint32_)
---
Imprime un numero entero sin signo en el LCD.

```cpp
LCD lcd(2, 3, 4, 5, 6, 7);
lcd.print(234567);
```

### print(float_)
---
Imprime un número flotante en el LCD.

```cpp
LCD lcd(2, 3, 4, 5, 6, 7);
lcd.print(234.65);
```