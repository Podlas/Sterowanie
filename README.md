# Sterowanie obrotami silnika i kierunkiem obrotów.
Sterowanie obrotami będzie odbywać się za pomocą potencjometru a zmiana kierunku obrotów silnika za pomocą przycisku. 
Sterowanie obrotami jaki i kierunkiem będzię dobywać się przy użyciu sterownika L293D - dwukanałowego sterownika silników.

Materiały użyte w projekcie:

-L293D - dwukanałowy sterownik silników,

-Arduino UNO R3 ATMega328,

-Potencjometr obrotowy 10kΩ,

-Mini silnik MT78 3-6 V,

-Płytka stykowa,

-Przewody połączeniowe męsko-męskie,

-Tact Switch 6x6mm .

KOD PROGRAMU:

int enablePin = 11;
int in1Pin = 10;
int in2Pin = 9;
int switchPin = 7;
int potPin = 0;

void setup()
{
  pinMode(in1Pin, OUTPUT);
  pinMode(in2Pin, OUTPUT);
  pinMode(enablePin, OUTPUT);
  pinMode(switchPin, INPUT_PULLUP);
}

void loop()
{
  int speed = analogRead(potPin) / 4;
  boolean reverse = digitalRead(switchPin);
  setMotor(speed, reverse);
}

void setMotor(int speed, boolean reverse)
{
  analogWrite(enablePin, speed);
  digitalWrite(in1Pin, ! reverse);
  digitalWrite(in2Pin, reverse);
}
