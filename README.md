#include <Wire.h> 
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,16,2);  // set the LCD address to 0x27 for a 16 chars and 2 line display

void setup()
{
  lcd.init();                      // initialize the lcd 
  lcd.backlight();
  Serial.begin(9600);
  pinMode(2,OUTPUT);
   pinMode(3,OUTPUT);
    pinMode(4,OUTPUT);
    digitalWrite(2,HIGH);
    digitalWrite(3,HIGH);
    digitalWrite(4,HIGH);
}
void loop()
{
  lcd.clear();
  
 
  lcd.setCursor(0,0);
  lcd.print("T>09:59:00");
  delay(10000);
  lcd.setCursor(0,0);
  lcd.print("T>10:00:00");
  delay(2000);
 digitalWrite(2,LOW);
  delay(5000);
  digitalWrite(2,HIGH);
  delay(2000);
  int IR1 = analogRead(A0);
  Serial.println("IR1");
  Serial.println(IR1);
  delay(2000);
  if(IR1<500)
  {
   lcd.setCursor(0,1);
   lcd.print("Tab not taken");
    delay(1000);
   SendSMS(" Tab not taken ");
   delay(2000);
    digitalWrite(3,LOW);
    delay(5000);
    digitalWrite(3,HIGH);
  }
  else if(IR1>500)
  {
   lcd.setCursor(0,1);
   lcd.print("Tab taken");
    delay(1000);
   SendSMS(" Tab taken ");
   delay(2000);
    digitalWrite(4,LOW);
    delay(5000);
    digitalWrite(4,HIGH);
  }
  delay(2000);
  lcd.setCursor(0,1);
   lcd.print("--------------");
  delay(10000); 
 // lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("T>12:59:00");
  delay(10000);
  lcd.setCursor(0,0);
  lcd.print("T>13:00:00");
  delay(2000);
  digitalWrite(2,LOW);
  delay(5000);
  digitalWrite(2,HIGH);
  delay(2000);
  int IR2 = analogRead(A1);
  Serial.println("IR2");
  Serial.println(IR2);
   delay(2000);
  if(IR2<500)
  {
   lcd.setCursor(0,1);
   lcd.print("Tab not taken");
    delay(1000);
   SendSMS(" Tab not taken ");
   delay(2000);
    digitalWrite(3,LOW);
  delay(5000);
  digitalWrite(3,HIGH);
  }
  else if(IR2>500)
  {
   lcd.setCursor(0,1);
   lcd.print("Tab taken");
    delay(1000);
   SendSMS(" Tab taken ");
   delay(2000);
    digitalWrite(4,LOW);
  delay(5000);
  digitalWrite(4,HIGH);
  }
  delay(2000);
  lcd.setCursor(0,1);
   lcd.print("------------");
  delay(10000); 
 // lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("T>20:59:00");
  delay(10000);
  lcd.setCursor(0,0);
  lcd.print("T>21:00:00");
  delay(2000);
  digitalWrite(2,LOW);
  delay(5000);
  digitalWrite(2,HIGH);
  //delay(2000);
   int IR3 = analogRead(A2);
  Serial.println("IR3");
  Serial.println(IR3);
   delay(2000);
  if(IR3<500)
  {
   lcd.setCursor(0,1);
   lcd.print("Tab not taken");
    delay(1000);
   SendSMS(" Tab not taken ");
   delay(2000);
    digitalWrite(3,LOW);
  delay(5000);
  digitalWrite(3,HIGH);
  }
  else if(IR3>500)
  {
   lcd.setCursor(0,1);
   lcd.print("Tab taken");
   delay(1000);
   SendSMS(" Tab taken ");
   delay(2000);
    digitalWrite(4,LOW);
  delay(5000);
  digitalWrite(4,HIGH);
  }
 
  delay(2000);
  lcd.setCursor(0,1);
  lcd.print("--------------");
 
}
void SendSMS(char string[100])
{
  Serial.println("AT+CMGF=1");    //To send SMS in Text Mode
  delay(1000);
  Serial.println("AT+CMGS=\"+917411348821.\"\r"); //Change to destination phone number 
  delay(1000);
  Serial.println(string);//the content of the message
  delay(200);
  Serial.println((char)26); //the stopping character Ctrl+Z
  delay(1000);  
}
