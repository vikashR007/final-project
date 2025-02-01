#include<LiquidCrystal.h>
LiquidCrystal lcd(12,11,10,6,8,7);
int gas = A0;
int buzzer = 5;
// Include the Servo library 
#include <Servo.h> 
// Declare the Servo pin 
int servoPin = 9; 
// Create a servo object 
Servo Servo1;
void setup()
{ 
   Serial.begin(9600); 
   pinMode(buzzer, OUTPUT);
      pinMode(gas,INPUT);
Servo1.attach(servoPin); 
  lcd.begin(16,2);
  lcd.setCursor(0,0);
  lcd.print("LPG GAS LEAKAGE "); 
  lcd.setCursor(0,1);
  lcd.print("DETECTION SYSTEM");
  delay(2000);
  lcd.clear();

}

void loop()
{

digitalWrite(buzzer,LOW);
int   gas1=analogRead(gas);
// Make servo go to 0 degrees 
   Servo1.write(0); 
   delay(1000); 
lcd.setCursor(0,0);
  lcd.print("GAS = ");
  lcd.setCursor(6,0);
  lcd.print(gas1);
 delay(600);
  lcd.clear();

  if(gas1>900)
{
   digitalWrite(buzzer,HIGH);
    // Make servo go to 180 degrees 
   Servo1.write(90); 
   delay(1000); 
   while(1)
   {
   digitalWrite(buzzer,HIGH);
  lcd.setCursor(0,0);
  lcd.print("LEAKAGE DETECTED");
  lcd.setCursor(0,1);
   lcd.print("REGULATOR OFF");
 delay(5000);
  lcd.clear();
   }
}
}
