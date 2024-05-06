# Los-bombas
Cierre semestre

# 3.2 Practica 0, Checar IDE Arduino y correr el BLINK

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























