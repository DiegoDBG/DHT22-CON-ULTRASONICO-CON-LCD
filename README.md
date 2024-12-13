# DHT22 CON ULTRASONICO CON LCD
## Practica con un sensor ultrasonico, sensor de temperatura y humedad THD22 en una placa de desarrollo ESP32 y un LCD de 12C 
Este repositorio muestra como podemos programar una **ESP32** con el sensor **HC-SR04** y sensor **DHT22** mostrarando los datos optenidos en un **LCD 12c**.

### Introducción
**Descripción:** 
La **ESP32** la utilizamos en un entorno de adquision de datos, en esta practica ocuparemos un **sensor ultrasonico** para medir la distancia del entorno, sensor de temperatura y humedad, como tambien un **LCD de 12c** para visualizar los datos opotenidos, todo siendo simulado en una pagina llamda **WOKWI**

### Material Necesario
Para realizar esta practica necesitas lo siguiente:
- WOKWI
- Tarjeta ESP32
- Sensor ultrasonico HC-SR04
- Sensor de temperatura y humedad DHT22
- LCD (16x2) 12c

### Requisitos previos:
Para poder usar este repositorio necesitas entrar a la plataforma WOKWI.

### Instrucciones de preparación de entorno:
1.-Abrir la terminal de programación y colocar la siguente programación:
```
const int Trigger = 4;   //Pin digital 4 para el Trigger del sensor
const int Echo = 2;   //Pin digital 2 para el Echo del sensor

#include <LiquidCrystal_I2C.h> //Libreria de LCD
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
#include "DHTesp.h" //Libreria de DHT

const int DHT_PIN = 15; //pin del sensor de temperatura
DHTesp dhtSensor;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0

}

void loop() {

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
 
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  //delay(2000); 
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  Serial.println("---");
  delay(2000);          //Hacemos una pausa de 200ms

  lcd.clear(); 
  lcd.setCursor(4, 0); //coordenadas del LCD 
  lcd.print("MODULO V");
  lcd.setCursor(6, 1);
  lcd.print("AIyM");
 delay(2000);

lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("diego bahena");
  lcd.setCursor(6, 1);
  lcd.print("I.E.E");
  delay(2000);

 lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  delay(2000);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  delay(2000);

}
```
2.- Instalar las librerias de **LiquidCrystal I2C** y de **DHT sensor library for ESPx** como se muestra en la siguente imagen.

![image](https://github.com/user-attachments/assets/bdc9e5bf-37b3-4845-bd5b-71c4c5f39de3)

3.- Hacer la conexion de **HC-SR04** como de **DHT22** con la **ESP32** y el **LCD 12C** como se muestra en la siguente imagen.

![image](https://github.com/user-attachments/assets/eecee0fa-06a1-49c8-a187-8d2bf10903d7)

### Instrucciónes de operación
- Iniciar simulador.
- Visualizar los datos en el LCD.
- Colocar la distancia dando click al sensor ultrasonico HC-SR04
- Colocar la temperatura y humedad dando click al sensor DHT22
  
### Resultados
Cuando haya funcionado, verás los valores dentro del LCD como se muestra en la siguente imagen.

![image](https://github.com/user-attachments/assets/3949858c-4496-405e-9a99-29e93075f1b8)

![image](https://github.com/user-attachments/assets/77f9db88-3c3d-4647-af80-d8f02d20741b)

![image](https://github.com/user-attachments/assets/a7ba93fa-3a4a-47bf-825a-685128526953)

![image](https://github.com/user-attachments/assets/bab60b62-9fea-43b8-97bd-fb2799994432)

### Desarrollado por 
Diego David Bahena Galan

[GitHub](https://github.com/DiegoDBG)
