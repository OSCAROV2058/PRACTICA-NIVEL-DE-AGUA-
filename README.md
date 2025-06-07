# PRACTICA-NIVEL-DE-AGUA
EN ESTA PRACTICA SE BUSCA IMPLEMENTAR UN NIVEL DE AGUA CON UN SENSOR ULTRASONICO REFLEJANDO EL DATO EN UNA PANTALLA LCD.

### Descripcion

Este repositorio muestra como podemos programar un nivel de agua con el sensor ultrasonico (HC-SR04) y una pantalla LCD, marcando nivel en 4 leds cumpliendo las siguientes condiciones:

tanque vacio - 0 leds encendidos

tanque 25% - 1 led encendido

tanque 50% - 2 led encendido

tanque 75% - 3 led encendido

tanque 100% - 4 led encendido

## Material necesario

-WOKWI

-Tarjeta ESP32

-Sensor ultrasonico (HC-SR04)

-Pantalla LCD (16x2)

-4 leds

-4 resistencias 220 homs

## Instrucciones de preparación de entorno

1. Abrir la terminal de programación y colocar la siguente programación:

```

// defines pins numbers
const int trigPin = 4;
const int echoPin = 18;
const int led1 = 16;
const int led2 = 0;
const int led3 = 2;
const int led4 = 15;

#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

// defines variables
long duration;
int distance;
int safetyDistance;


void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
Serial.begin(9600); // Starts the serial communication

 lcd.init();
  lcd.backlight();

}

void loop() {

// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

safetyDistance = distance;

if (safetyDistance>=1 && safetyDistance<=2)
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.setCursor(0, 0);
  lcd.print(" TANQUE VACIO ");
  delay(2000);
  lcd.clear();
}

if (safetyDistance>=3 && safetyDistance<=99)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.setCursor(0, 0);
  lcd.print(" TANQUE AL 25% ");
  delay(2000);
  lcd.clear();
}

if (safetyDistance>=100 && safetyDistance<=199)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.setCursor(0, 0);
  lcd.print(" TANQUE AL 50% ");
  delay(2000);
  lcd.clear();
}

if (safetyDistance>=200 && safetyDistance<=299)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
    lcd.setCursor(0, 0);
  lcd.print(" TANQUE AL 75% ");
  delay(2000);
  lcd.clear();
}

if(safetyDistance>=300 && safetyDistance<=399) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
    lcd.setCursor(0, 0);
  lcd.print(" TANQUE AL 100% ");
  delay(2000);
  lcd.clear();
}

// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
delay(50);
lcd.clear();

lcd.setCursor(0, 0);
  lcd.print(" DIPLOMADO 5 ");
  lcd.setCursor(0, 1);
  lcd.print(" AUTOMATIZACION ");
delay(2000);
lcd.clear();
 
 lcd.setCursor(0, 0);
  lcd.print(" OSCAR OCAMPO ");
  lcd.setCursor(0, 1);
  lcd.print(" ING. MECANICO ");
delay(2000);
lcd.clear();

lcd.setCursor(0, 0);
  lcd.print(" 07 JUNIO 2025 ");
delay(2000);
lcd.clear();

}

```

2. Instalar la libreria de LiquidCrystal I2C como se muestra en la siguente imagen.

![]()

3. Hacer la conexion del sensor ultrasonico, leds, resistencias y LCD con la ESP32 como se muestra en la siguente imagen.

![]()

## Instrucciónes de operación

1. Iniciar simulador.

2. Visualizar los datos en el monitor serial. (CURSO, NOMBRE Y CARRERA, FECHA).
   
3. Colocar la distancia dando doble click al sensor ultrasonico.

## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en las siguentes imagenes.

![]()

![]()

![]()

![]()

![]()

## Creditos

Desarrollado por Ing. Oscar Jair Ocampo Villarreal
- ([github](https://github.com/OSCAROV2058))
