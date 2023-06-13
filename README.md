# Practica Ultrasonico con LCD
Este repositorio muestra como podemos programar una ESP32 con el sensor ultrasonico y un LCD para medir distancia.

## Introducción

### Descripción

La ```Esp32``` la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (```HC-SR04 Ultrasonic Distance Sensor```) para adquirir distancia; Cabe aclarar que esta practica se usara un simulador llamado [WOKWI](https://https://wokwi.com/).


## Material Necesario

Para realizar esta practica necesitas lo siguiente

- [WOKWI](https://https://wokwi.com/) como simulador.
- Tarjeta ```ESP 32```.
- Sensor ```HC-SR04 Ultrasonic Distance Sensor```.

- ```LDC 16x2 (I2C)```



## Instrucciones

### Requisitos previos

Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://https://wokwi.com/).


### Instrucciones de preparación de entorno 

1. Entramos al simulador [WOKWI](https://https://wokwi.com/) y selecionamos la tarjeta ```ESP 32``` como se muestra en la siguiente imagen.

![](https://github.com/jorgelopezquiroz/Ultrasonico_LCD/blob/main/ESP32.png?raw=true)


2. Posteriormente se abrirá la terminal de programación y se coloca la siguente programación:

```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR   0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 27;   //Pin digital 3 para el Echo del sensor


LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  lcd.init ();
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
  delay(3000); 
   lcd.setCursor(0,0);
  lcd.print("Distancia:"+ String (d)+ "cm");
  lcd.setCursor(0,1);
  lcd.print("   Jorge Lopez  ");
  delay (1000);         //Hacemos una pausa de 100ms
}

```
3. Se necesita instalar la libreria de **DHT sensor library for ESPx** y **LiquidCrystal I2C** en el simulador como se muestra en la siguiente imagen.
![](https://github.com/jorgelopezquiroz/Ultrasonico_LCD/blob/main/LIBRARIES.png?raw=true)
 
4. Hacer la conexion de **HC-SR04 Ultrasonic Distance Sensor** con la **ESP32** y **LCD 16x2 (I2C)**  como se muestra en la siguente imagen.

![](https://github.com/jorgelopezquiroz/Ultrasonico_LCD/blob/main/Conexion.png?raw=true)

### Instrucciónes de operación

1. Iniciar la simulación.
2. Visualizar los datos en el monitor serial.
3. Colocar la distancia se da *doble click* al sensor **HC-SR04 Ultrasonic Distance Sensor** 

## Resultados

Cuando haya compilado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.

![](https://github.com/jorgelopezquiroz/Ultrasonico_LCD/blob/main/Resultados.png?raw=true)




## Evidencias
![](https://github.com/jorgelopezquiroz/Ultrasonico_LCD/blob/main/Evidencia%201.png?raw=true)


![](https://github.com/jorgelopezquiroz/Ultrasonico_LCD/blob/main/Evidencia%202.png?raw=true)


# Créditos

Desarrollado por Jorge Esteban Lopez Quiroz

- [GitHub](https://github.com/jorgelopezquiroz)