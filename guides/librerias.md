# Librerías
---

[Puertos Digitales](#-puertos-digitales)
- [pinMode(pin, mode)](#-pinmodepin-mode)
- [digitalWrite(pin, output)](#-digitalwritepin-output)
- [digitalRead(pin)](#-digitalreadpin)
- [pinToggle(pin)](#-pintogglepin)
- [attachExternalInt(pin, *f, mode)](#-attachexternalintpin-f-mode)
- [attachPinChangeInt(pin, *f)](#-attachpinchangeintpin-f)
  
[Analog to Digital Converter (ADC)](#-analog-to-digital-converter-adc)
- [analogRead(pin)](#-analogreadpin)
- [analogStart(pin)](#-analogstartpin)
- [analogRef(ref)](#-analogrefref)
- [analogInterrupt(*f, trigger)](#-analoginterruptf-trigger)

[LCD Display](#-lcd-display)
- [LCD(rs, en, d4, d5, d6, d7)](#-lcdrs-en-d4-d5-d6-d7)
- [clear()](#-clear)
- [setXY(x, y)](#-setxyx-y)
- [putC(ch)](#-putcch)
- [print(str)](#-printstr)
- [print(int32_)](#-printint32_)
- [print(uint32_)](#-printuint32_)
- [print(float_)](#-printfloat_)


## Puertos Digitales
---
Este apartado es sobre la librería `digital.cpp / digital.h`. Les va a permitir usar los puertos digitales de entrada y salida sin demasiada dificultad. Dentro de esta librería tienen:

### pinMode(pin, mode)
---
Configura el pin como entrada o salida. La forma de usar esta función es indicar primero el numero de pin que queremos configurar, que responde a como están clasificados en el [Arduino UNO](https://images.prismic.io/circuito/8e3a980f0f964cc539b4cbbba2654bb660db6f52_arduino-uno-pinout-diagram.png?auto=compress,format), luego, como segundo argumento de la función, pasan el modo, sea `INPUT` o `OUTPUT`.

```c
pinMode(0, OUTPUT); // PD0 es salida
pinMode(16, INPUT); // PC2 es entrada
```

### digitalWrite(pin, output)
---
El funcionamiento es similar a la función anterior, pero ahora, suponiendo que el pin ya fue configurado como salida, podemos determinar el valor de ese pin, es decir, si esta en `HIGH` o `LOW`.

```c
digitalWrite(5, HIGH);  // PD5 va a ser uno
digitalWrite(6, LOW);   // PD6 va a ser cero
```

### digitalRead(pin)
---
Esta función devuelve el valor del pin, independientemente si es una entrada o salida, es decir, que si el pin estaba en uno, devuelve `HIGH`, si estaba en cero, devuelve `LOW`.

```c
int pin = digitalRead(6);   // Guarda en la variable pin el valor de PD6
```

### pinToggle(pin)
---
Si el pin determinado es una salida, entonces esta función hace que cambie su valor, es decir, si estaba en `HIGH` pasa a `LOW` y viceversa.

```c
pinToggle(6);   // El valor de PD6 cambia de cero a uno o viceversa
```

### attachExternalInt(pin, *f, mode)
---
Esta función nos permite agregar una interrupción externa a un pin determinado y asociarle una función que va a ejecutarse cada vez que el evento que configuramos se de. Noten que tiene tres parámetros:

- `pin` es el numero de pin que queremos que tenga la interrupción externa. **Solo los pines 2 y 3 tienen esta característica**.
- `f`es la función que queremos que se ejecute cada vez que la interrupción se da. La función tiene que ser del tipo `void f(void)`.
- `mode` es el tipo de evento que va a generar esta interrupción. Las opciones son `LOW` para un nivel bajo de tensión, `CHANGE` para cualquier cambio en el pin, `FALL` para un flanco descendente y `RISE` para un flanco ascendente.

```c
void blink(void);   // Prototipo de la funcion que voy a usar

int main(void) {    
	pinMode(4, OUTPUT);                // PD4 es salida    
	attachExternalInt(2, blink, RISE); // PD2 tiene una interrupcion por flanco 
																		 // ascendente que ejecuta la funcion blink    
	while(1);                          // Bucle infinito para que el programa no termine
}

void blink(void) {    
	pinToggle(4);       // PD4 hace un toggle cada vez que se dispara la interrupcion
}
```

### attachPinChangeInt(pin, *f)
---
Funciona casi igual que la función anterior, pero ahora la interrupción que estamos asociando al pin es la interrupción por pin change, que se activa cuando cualquier cambio de valor en el pin ocurre. Noten que no hay posibilidad ahora de configurar si la interrupción se da por flanco o nivel, porque esta no tiene esa posibilidad. Todos los pines tienen la posibilidad de tener una interrupción asociada, excepto los pines PB6 y PB7 que van conectados al cristal y PC6 que es el pin de reset.

```c
void blink(void);   // Prototipo de la funcion que voy a usar

int main(void) {    
	pinMode(4, OUTPUT);                 // PD4 es salida    
	attachPinChangeInt(2, blink, RISE); // PD2 tiene una interrupcion por pin change 
																			// que ejecuta la funcion blink    
	while(1);                           // Bucle infinito para que el programa no termine
}

void blink(void) {    
	if (digitalRead(2)) {   // Reviso si el pin esta en uno o cero        
			pinToggle(4);       // Si esta en uno PD4 hace un toggle    
	}
}
```

## Analog to Digital Converter (ADC)
---
Esta sección es sobre `analog.cpp / analog.h` que les va a permitir hacer lecturas analógicas con el microcontrolador sin la necesidad de configurar los registros.

### analogRead(pin)
---
Devuelve un `uint16_t` con el valor que el pin que se pasa como argumento esta leyendo. El numero que va a estar entre 0 y 1023 dependiendo de que tan próximo este el valor de tensión en el pin a la tensión de referencia del ADC. El numero que pasen como parámetro no es el numero de pin, sino canal. Los canales que admiten entrada analógica son los que están asociados a los pines 14-19.

```c
uint16_t adc = analogRead(2);   // Guardo en adc el valor de lo que 
																// este midiendo PC2 (ADC2) 
```

### analogStart(pin)
---
Inicia una conversión en el pin indicado pero no devuelve ningún valor.

```c
analogStart(0); // Inicia una conversion en el pin PC0
```

### analogRef(ref)
---
Cambia el valor de la tensión de referencia del ADC a una de las tres opciones disponibles:

- `AREF`: tensión de referencia conectada al pin que lleva ese nombre. Puede ser cualquier valor entre 0 y 5V.
- `AVCC`: 5V o 3,3V dependiendo de con que tensión se este alimentando el microcontrolador.
- `INTERNAL`: es la tensión interna de 1,1V del microcontrolador.

Cambiar la tensión de referencia es util para poder mejorar la precisión si estamos midiendo algo que no entrega mucha tensión.

```c
analogRef(INTERNAL);    // Tension de 1,1V
analogRef(AVCC);        // Tension de alimentacion (3,3V o 5V)
analogRef(AREF);        // Tension de referencia
```

### analogInterrupt(*f, trigger)
---
Asocia una función que se ejecute cada vez que el ADC termina una conversión y permite elegir el evento que dispara la cada conversión entre las siguientes opciones:

- `FREE`: el ADC inicia una conversión cada vez que se le indique con `analogStart()`.
- `ANALOG_CMP`: se dispara una conversión cuando se dispara la interrupción del comparador analógico.
- `EXT_INT0`: se dispara una conversión con cada interrupción externa, particularmente la `INT0` (pin 2).
- `TMR0_MATCH_A`: se dispara con cada match entre `TCNT0` y `OCR0A`.
- `TMR0_OVF`: se dispara con cada overflow del `TCNT0`.
- `TMR1_MATCH_A`: se dispara con cada match entre `TCNT1` y `OCR1A`.
- `TMR1_OVF`: se dispara con cada overflow del `TCNT1`.
- `TMR1_CAPTURE`: se dispara con un input capture event del Timer 1.

```c
void compare(void); // Prototipo de la funcion que voy a usar como interrupcion

int main(void) {    
	analogInterrupt(compare, FREE);     // Asocio la funcion a la interrupcion 
																			// y la activo por INT0    
	pinMode(0, OUTPUT);                 // PD0 es salida    
	while(1) {                          // Bucle infinito para que el programa no termine        
		analogStart(0);                   // Inicio una conversion    
	}
}

void compare(void) {    
	if (analogRead(0) > 500) {          // Si el valor que se mide es mayor 
																			// a este numero arbitrario        
		digitalWrite(0, HIGH);            // Pongo esta pin en HIGH    
	}    
	else {        
		digitalWrite(0, LOW);             // Sino en LOW    
	}
}
```

## LCD Display
---
Esta librería es para poder trabajar con Displays LCD de 16x2. De momento, solamente funciona para ese tipo de display y con cuatro bits de datos, no ocho. En `LCD.cpp / LCD.h` se define la clase `LCD` y vamos a hablar de los métodos que tiene. Los atributos son privados así que no pueden modificarse.

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