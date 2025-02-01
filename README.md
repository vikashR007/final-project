#include<LiquidCrystal.h>
LiquidCrystal lcd(8,9,10,11,12,13);

#include <OneWire.h>
#include <DallasTemperature.h>

#define ONE_WIRE_BUS 16

OneWire oneWire(ONE_WIRE_BUS);

DallasTemperature sensors(&oneWire);

 float Celcius=0;
 float Fahrenheit=0;


void setup()
{ 
Serial.begin(9600);
  sensors.begin();

 
  
  lcd.begin(16,2);
  lcd.setCursor(0,0);
  lcd.print("WATER QUALITY"); 
  lcd.setCursor(0,1);
  lcd.print("MONITORING SYSTEM");
  delay(2000);
  lcd.clear();

}

void loop()
{
  int sensorValue = analogRead(A0);
  float voltage = sensorValue * (5.0 / 1024.0);
 
  Serial.println ("Sensor Output (V):");
  Serial.println (voltage);
  Serial.println();
  
   sensors.requestTemperatures(); 
  Celcius=sensors.getTempCByIndex(0);
  Fahrenheit=sensors.toFahrenheit(Celcius);
  Serial.print(" C  ");
  Serial.print(Celcius);
  Serial.print(" F  ");
  Serial.println(Fahrenheit);
  delay(1000);
  
  lcd.setCursor(0,0);
lcd.print("temp = ");
  lcd.setCursor(7,0);
lcd.print(Celcius);
  
  lcd.setCursor(0,1);
lcd.print("trb level = ");
  lcd.setCursor(12,1);
lcd.print(voltage);

}
   
