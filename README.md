# Práctica 1: Blink con ESP32

## Objetivo
El objetivo de esta práctica es generar el parpadeo periódico de un LED utilizando el microcontrolador ESP32. Además, se utilizará la salida serie para depurar el programa.

## Materiales Necesarios
- Microcontrolador ESP32
- LED integrado (o LED externo con resistencia de 220Ω)
- Cable USB para programación
- Entorno de desarrollo (Arduino IDE o PlatformIO)

## Descripción de la Funcionalidad
1. Configurar el pin del LED como salida.
2. Crear un bucle infinito con las siguientes acciones:
   - Encender el LED.
   - Esperar 500 ms.
   - Apagar el LED.
   - Esperar 500 ms.

## Código Básico
```cpp
#define LED_BUILTIN 2
#define DELAY 500

void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  delay(DELAY);
  digitalWrite(LED_BUILTIN, LOW);
  delay(DELAY);
}
```

## Modificaciones y Ejercicios

### 1. Envío de Datos por el Puerto Serie
Modificar el programa para incluir el envío de mensajes "ON" y "OFF" al puerto serie:

```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
  Serial.begin(115200);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  Serial.println("ON");
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  Serial.println("OFF");
  delay(1000);
}
```

### 2. Manipulación Directa de Registros
Acceder directamente a los registros del microcontrolador para controlar el LED:

```cpp
uint32_t *gpio_out = (uint32_t *)GPIO_OUT_REG;

void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  *gpio_out |= (1 << 2);  // Encender LED
  delay(500);
  *gpio_out ^= (1 << 2);  // Apagar LED
  delay(500);
}
```

### 3. Medición de Frecuencia con Osciloscopio
Eliminar los `delay()` y modificar el programa para medir la frecuencia máxima del parpadeo en cuatro escenarios:
1. Con envío al puerto serie y usando funciones de Arduino.
2. Con envío al puerto serie y acceso directo a registros.
3. Sin envío al puerto serie y usando funciones de Arduino.
4. Sin envío al puerto serie y acceso directo a registros.

### 4. Informe Final
Generar un archivo `informe.MD` con:
- Código fuente del programa.
- Diagrama de flujo del programa.
- Diagrama de tiempos de ejecución.

### 5. Tiempo Libre del Procesador
Responder la pregunta: ¿Cuál es el tiempo libre que tiene el procesador en la implementación realizada?

## Ejercicios Opcionales
1. Leer el valor de un convertidor A/D y mostrarlo en el puerto serie y por un pin D/A.
2. Leer el sensor de temperatura interno y mostrar el valor por el puerto serie.

## Referencias
- [Repositorio Blink](https://github.com/schacon/blink)
- [Introducción a PlatformIO con ESP32](https://electropeak.com/learn/getting-started-with-platformio-ide-to-program-esp32)
- [Lectura de ADC en ESP32](https://randomnerdtutorials.com/esp32-adc-analog-read-arduino-ide/)
- [Lectura del sensor de temperatura interno](https://gist.github.com/xxlukas42/7e7e18604f61529b8398f7fcc5785251)

---
Sube los resultados a tu repositorio personal en GitHub y adjunta el informe en formato Markdown.

