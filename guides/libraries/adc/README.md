## Analog to Digital Converter (ADC)
---
Esta sección es sobre `analog.cpp / analog.h` que les va a permitir hacer lecturas analógicas con el microcontrolador sin la necesidad de configurar los registros.

## Funciones
---
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
		analogStart(0);                 // Inicio una conversion    
	}
}

void compare(void) {    
	if (analogRead(0) > 500) {          // Si el valor que se mide es mayor 
										// a este numero arbitrario        
		digitalWrite(0, HIGH);          // Pongo esta pin en HIGH    
	}    
	else {        
		digitalWrite(0, LOW);           // Sino en LOW    
	}
}
```