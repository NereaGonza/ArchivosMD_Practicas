Nerea Gonz谩lez 
# Practica 3: Bluetooth

>Objetivo: Comprender el funcionamiento de BT.
Generaremos un web server utilizando
nuestra ESP32 y tambien una comunicaci贸n serie con una aplicaci贸n de un m贸vil con BT .

 馃搵
## Pr谩ctica B:
---------------------------------
路 C贸digo de la pr谩ctica 

```
//This example code is in the Public Domain (or CC0 licensed, at your option.)
//By Evandro Copercini - 2018
//
//This example creates a bridge between Serial and Classical Bluetooth (SPP)
//and also demonstrate that SerialBT have the same functionalities of a normal Serial
#include "BluetoothSerial.h"
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
BluetoothSerial SerialBT;
void setup() {
Serial.begin(115200);
SerialBT.begin("ESP32test"); //Bluetooth device name
Serial.println("The device started, now you can pair it with bluetooth!");
}
void loop() {
if (Serial.available()) {
SerialBT.write(Serial.read());
}
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
delay(20);
}
```
Incluimos la librer铆a
necesarias para el funcionamiento Bluetooth. 

```
#include "BluetoothSerial.h"
```

La siguiente l铆neas habilitan el bluetooth. 
```
#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif
```
Creamos una instancia de bluetooth.

```
BluetoothSerial SerialBT;
```

Iniciamos la configuraci贸n con el PC (a una velocidad de 115200 baudios). 

Escribimos el nombre del dispositivo de bluetooth, en este caso es 'ESP32Test'.
```
void setup() {
Serial.begin(115200);
SerialBT.begin("ESP32test"); //Bluetooth device name
Serial.println("The device started, now you can pair it with bluetooth!");
}
```
El bucle se encarga de enviar y recibir datos a trav茅s de Bluetooth Serial.
```
void loop() {
if (Serial.available()) {
SerialBT.write(Serial.read());
}
```
Por 煤ltimo, se verificar谩 si hay datos disponibles en el monitor en serie, si es as铆, enviar谩 los datos al dispositivo Bluetooth mediante el Bluetooth de nuestro ESP32.

> SerialBT.write () env铆a datos utilizando el serial bluetooth.

>Serial.read () devuelve los datos recibidos en el puerto serie

```
if (SerialBT.available()) {
Serial.write(SerialBT.read());
}
delay(20);
}
```

>Salida: 

![](blue.jpg)

>Dispositivo enlazado: 

![](movil.jpeg)

