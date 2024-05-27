# Los-bombas

## Portada
### Instituto Tecnologico de Tijuana

### Materia: 
Lenguajes de interfaz

### Profesor: 
René Solis

### Alumnos: 
Valeria Rosales Gomez C21212361

Ulises Andres Vara Espinoza 21212656

Oscar Bernardino Vera Cortez 20211855

Melanie Estefania GonzaleZ Vazquez 2121956

# Cierre semestre
## Practica 3.1
### CODIGO EN VISUAL

```c#
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.IO.Ports;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;


namespace practica1

{
    public partial class Form1 : Form

    {

        SerialPort serialPort = new SerialPort();

        bool IsClose = false;
        
        public Form1()

        {

            InitializeComponent();

            serialPort = new SerialPort();

            serialPort.BaudRate = 9000;

            string[] ports = SerialPort.GetPortNames();

            foreach (string port in ports)

            {

                cbPort.Items.Add(port);

            }

        }
        
        private void buttonconect_Click(object sender, EventArgs e)

        {

            if (cbPort.SelectedItem == null)

            {

                MessageBox.Show("Por favor, selecciona un puerto COM.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);

                return;

            }
            try

            {

                serialPort.PortName = cbPort.SelectedItem.ToString();

                serialPort.BaudRate = 9600; // Velocidad de comunicación

                serialPort.DataReceived += new SerialDataReceivedEventHandler(serialPort_DataReceived);

                serialPort.Open();

                MessageBox.Show("Conexión establecida correctamente.", "Conectado", MessageBoxButtons.OK, MessageBoxIcon.Information);

            }

            catch (Exception ex)

            {

                MessageBox.Show("Error al conectar al puerto COM: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);

            }

        }
        
        private void buttonenv_Click(object sender, EventArgs e)

        {

            if (!serialPort.IsOpen)

            {

                string mensaje = textBoxmensj.Text;

                serialPort.WriteLine(mensaje);

                serialPort.ReadLine();

            }

            try

            {

                MessageBox.Show("Primero, debes conectar al puerto COM.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);

                return;

            }

            catch (Exception ex)

            {

                MessageBox.Show("Error al enviar el mensaje: " + ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);

            }

        }

        private void buttonrest_Click(object sender, EventArgs e)

        {

            if (serialPort.IsOpen)

            {

                serialPort.Close();

                MessageBox.Show("Conexión cerrada correctamente.", "Desconectado", MessageBoxButtons.OK, MessageBoxIcon.Information);

            }

        }

        private void serialPort_DataReceived(object sender, SerialDataReceivedEventArgs e)

        {

            string receivedData = serialPort.ReadLine();

            DisplayReceivedData(receivedData);

        }

        private void DisplayReceivedData(string data)

        {

            if (InvokeRequired)

            {

                BeginInvoke((MethodInvoker)delegate { DisplayReceivedData(data); });

            }

            else

            {

                textBoxmensj.AppendText(data + Environment.NewLine);

            }

        }

        private void Form1_Load(object sender, EventArgs e)

        {

        }

    }

}
```

## CODIGO EN ARDUINO
```c
void setup() {

  // put your setup code here, to run once:

  Serial.begin(9600);

  

  // Espera a que el Monitor Serie esté listo

  while (!Serial) {

    ;

  }

}

void loop() {

  // put your main code here, to run repeatedly:

  // Muestra el mensaje en el Monitor Serie

  Serial.println("Hola, mundo!");

  

  // Espera un segundo antes de enviar el mensaje nuevamente

  delay(1000);

}


```
## EVIDENCIA
![7e8acf1a-1e88-432c-8aa7-a6b1943dd68e](https://github.com/KingVara2/Los-bombas/assets/158336615/707b08f8-593c-48d1-a5d8-f9d6885539c0)

![85a06821-fe33-4433-86b1-78a9eee42c18](https://github.com/KingVara2/Los-bombas/assets/158336615/5ffeff09-09ab-48b5-b836-37e34ef58ffb)

![15bc6522-cf0d-49be-97cd-94b1e27bb423](https://github.com/KingVara2/Los-bombas/assets/158336615/17dc33e1-faf5-4579-81af-184712f735b8)


# 3.2 
## Practica 0, Checar IDE Arduino y correr el BLINK

Practica en arduino con codigo de c# 

## CÓDIGO

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


## Practica 3.5

## CODIGO

```c#
#include <WiFi.h>

#include <Wire.h>

#include <Adafruit_GFX.h>

#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128

#define SCREEN_HEIGHT 64

#define OLED_RESET    -1

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);


void setup() {

  Serial.begin(115200);

  if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {

    Serial.println(F("SSD1306 allocation failed"));

    for (;;);

  }
  display.clearDisplay();
}

const char *encToString(uint8_t enc) {

  switch (enc) {

    case ENC_TYPE_NONE: return "NONE";

    case ENC_TYPE_TKIP: return "WPA";

    case ENC_TYPE_CCMP: return "WPA2";

    case ENC_TYPE_AUTO: return "AUTO";

  }

  return "UNKN";

}





void loop() {

  delay(5000);

  Serial.printf("Beginning scan at %lu\n", millis());

  auto cnt = WiFi.scanNetworks();

  display.clearDisplay();

  if (!cnt) {

    Serial.printf("No networks found\n");

    display.setTextSize(0.5);

    display.setTextColor(SSD1306_WHITE);

    display.setCursor(0, 0);

    display.println("No networks found");

  } else {

    Serial.printf("Found %d networks\n\n", cnt);

    display.setTextSize(0.5);

    display.setTextColor(SSD1306_WHITE);

    display.setCursor(0, 0);

    display.println("Networks:");

    for (auto i = 0; i < cnt; i++) {

      Serial.printf("%s \n", WiFi.SSID(i));

      display.setCursor(0, (i + 1) * 8);

      display.printf("%s ", WiFi.SSID(i));

    }

  }

  Serial.printf("\n--- Sleeping ---\n\n\n");

  display.display();

  delay(5000);

}
```

## EVIDENCIA 
![7ddda51f-1a9d-423d-ab27-792d35ff908a](https://github.com/KingVara2/Los-bombas/assets/158336615/6f4d7c78-7261-4378-b167-30c838fbe2b4)























