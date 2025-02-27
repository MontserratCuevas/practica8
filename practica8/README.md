# Práctica 8

## Código

```c++
#include <Arduino.h>

void setup() {
  Serial.begin(115200);   // Inicializar Serial (UART0)
  Serial2.begin(115200);  // Inicializar Serial2 (UART2)
}

void loop() {
  // Leer datos de la UART0 y enviarlos a la UART2
  if (Serial.available()) {
    char c = Serial.read();
    Serial2.write(c);
  }
  
  // Leer datos de la UART2 y enviarlos a la UART0
  if (Serial2.available()) {
    char c = Serial2.read();
    Serial.write(c);
  }
}

```
## Descripción

Este es un ejemplo de como usar dos puertos serie (UART) en ESP32 para comunicarse con otros dispositivos.

En la función **setup()** se inicializa los dos puertos serie; UART0 y UART2.

En el bucle,**loop()**, el programa verifica si hay datos disponibles para leer en el puerto UART0, si hay datos disponibles se leen y se guardan en la variable c, estos datos se envían al puerto UART2. También funciona viceversa, lee datos del puerto UART2 y si hay datos los guarda tambén en la variable c y los envía al puerto UART0.

En el puerto serie nos muestra lo que vamos escribiendo por el teclado.

### Diagrama de flujos:

``` mermaid
graph TD
    A[Inicio] --> B[iniciar UART0]
    B --> C[iniciar UART2]
  
    C --> D[bucle principal]

    D --> E{hay datos en UART0?}
    E --> |Sí| F[guardar datos]
    F --> G[enviar datos a UART2]
    G --> D

    E --> |No| H{hay datos en UART2?}
    H --> |Sí| I[guardar datos]
    I --> J[enviar datos a UART0]
    J --> D

    H --> |No| D

  ```


### Foto del montaje:

<img src="montaje8.jpg" width="400" height="200">

## Conclusión

En conclusión, este código establece una comunicación bidireccional entre el puerto UART0 y el puerto UART2.


