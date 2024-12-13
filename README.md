# DHT22-CON-ULTRASONIDO-CON-LCD

## PROGRAMACIÓN

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
  lcd.setCursor(2, 0); //coordenadas del LCD 
  lcd.print("DIPLOMADO V");
  lcd.setCursor(2, 1);
  lcd.print("MECATRONICA");
 delay(2000);

lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("iNG. RAUL");
  lcd.setCursor(2, 1);
  lcd.print("ING. ELECTRICO");
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

## LIBRERIA

1. DHT sensor library for ESPx
2. LiquidCrystal I2C

## CONEXIÓN

![](https://github.com/RaulCasS/DHT22-CON-ULTRASONIDO-CON-LCD/blob/main/Captura%20de%20pantalla%202024-12-12%20232515.png?raw=true)

## RESULTADOS

![](https://github.com/RaulCasS/DHT22-CON-ULTRASONIDO-CON-LCD/blob/main/Captura%20de%20pantalla%202024-12-12%20232706.png?raw=true)
![]()
![]()
![]()
