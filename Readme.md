# Practica ESP32 con HC-SR04 Ultrasonic Distance Sensor
Este repositorio muestra como podemos programar una ESP32 con el sensor Ultrasonico de distancia.

## Introducción

### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```HC-SR04```) y una pantalla (```LCD 16x2 I2C```) Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/)
- Tarjeta ESP 32
- Sensor HC-SR04 Ultra Distance 
- Pantalla LCD I2C
- Y muchas ganas de chambear :D


## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Abrir la terminal de programación y colocar la siguente programación:


```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(9600);//iniciailzamos la comunicación
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
   
}

void loop()
{
  

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(5000);          //Hacemos una pausa de 100ms

 lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  lcd.setCursor(0, 1);
  lcd.print("                 " );
  delay (3000);
  lcd.setCursor(0, 0);
  lcd.print("Tenga buen dia   ");
lcd.setCursor(0, 1);
  lcd.print("  Nos vemos      ");
  delay (1500);
  lcd.setCursor(0, 0);
lcd.print("    Made by      ");
lcd.setCursor(0, 1);
  lcd.print("    Uriel M         ");
  delay(1000);


}

```

2. Hacer la conexion de **HC-SR04** con la **ESP32** como se muestra en la siguente imagen.



![](https://github.com/UrielMastache/ESP32-HCSR04/blob/main/Conexion%20sensor.png?raw=true)

3. Hacer la conexion de **LCD I2C** con la **ESP32** como se muestra en la siguiente imagen.

![](https://github.com/UrielMastache/ESP32-HCSR04/blob/main/Conexiones%20LCD.png?raw=true)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial y en la pantalla LCD.

## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial (parte blanca de abajo, así como también en  la pantalla LCD agregada) como se muestra en las siguentes imagenes.

![](https://github.com/UrielMastache/ESP32-HCSR04/blob/main/Simulacion.png?raw=true)

Mensaje 1

![](https://github.com/UrielMastache/ESP32-HCSR04/blob/main/Mensaje%201.png?raw=true)

Mensaje 2

![](https://github.com/UrielMastache/ESP32-HCSR04/blob/main/Mensaje%202.png?raw=true)

## Comentarios

Recuerda que puedes cambiar los mensajes finales en la patanlla LCD desde el codigo, en la parte final. Así como también recuerda que puedes cambiar los valores del sensor dandole clic a este mismo, y cambiara en tiempo real.

![](https://github.com/UrielMastache/ESP32-HCSR04/blob/main/cambiando%20valores.png?raw=true)

Gracias por ver :D 

Ciao.