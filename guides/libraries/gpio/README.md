# Puertos Digitales (GPIO)
---
Este apartado es sobre la librería `digital.cpp / digital.h`. Les va a permitir usar los puertos digitales de entrada y salida sin demasiada dificultad.

## Funciones
---
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
