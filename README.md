# Los-bombas
Cierre semestre

# 3.2 
## Practica 0, Checar IDE Arduino y correr el BLINK

Practica en arduino con codigo de c# 

## CODIGO

``` C#
 /*
  Programa: Control de Raspberry Pi Pico W
  Autor: Los bombas
  Fecha: 06/05/2024
*/

//
  Descripción:
  Este programa inicializa la comunicación serial en una Raspberry Pi Pico W y envía un mensaje de bienvenida.
  Posteriormente, entra en un bucle infinito.

  
// Variable booleana para controlar si el mensaje ya ha sido impreso
bool mensajeImpreso = false;

void setup() {
  // Inicializa la comunicación serial a 115200 baudios.
  Serial.begin(115200);
  
  // Envía un mensaje de bienvenida solo si el mensaje no ha sido impreso todavía.
  if (!mensajeImpreso) {
    Serial.println("Hola, Raspberry Pi Pico W!");
    mensajeImpreso = true; // Marcamos el mensaje como impreso
  }

}

void loop() {

  // Retraso mínimo para evitar saturar el bucle.
  delay(1);

}
```
## EVIDENCIA
![image](https://github.com/KingVara2/Los-bombas/assets/158336615/a924141f-c446-4a04-a1fb-afdc453e2254)

## Practica 3

## CODIGO

```c#
#include <Adafruit_SSD1306.h>
#include <Adafruit_GFX.h>
Adafruit_SSD1306 display(128, 64);

void setup() {
  // Initialize the display
  display.begin(SSD1306_SWITCHCAPVCC, 0x3C);  // Address 0x3C for 128x32
  // Clear the display
  display.clearDisplay();
  display.setTextColor(WHITE);
  display.setTextSize(2);
  display.setCursor(0, 0);
  display.println("Raspberry Pi Pico W");
  display.println("with OLED display");
  display.display();
}

void loop() {
  // Nothing to do here, just display the static text
}
```
## EVIDENCIA 
![image](https://github.com/KingVara2/Los-bombas/assets/158336615/0cfd8cfd-f922-466c-a711-11b751a42a55)




























