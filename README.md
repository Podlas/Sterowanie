# Sterowanie obrotami silnika i kierunkiem obrotów.
# Opis projektu.

Sterowanie obrotami będzie odbywać się za pomocą potencjometru a zmiana kierunku obrotów silnika za pomocą przycisku. 
Sterowanie obrotami jaki i kierunkiem będzię dobywać się przy użyciu sterownika L293D - dwukanałowego sterownika silników.

# Materiały użyte w projekcie:

-L293D - dwukanałowy sterownik silników,

-Arduino UNO R3 ATMega328,

-Potencjometr obrotowy 10kΩ,

-Mini silnik MT78 3-6 V,

-Płytka stykowa,

-Przewody połączeniowe męsko-męskie,

-Tact Switch 6x6mm .
# Zdjęcia wykonanego układu:
![nazwa](./1/jpg)




# KOD PROGRAMU:


```c
int enablePin = 11; //pin włączający/wyłączający silnik w zależności od stanów wejść IN1 i IN2

int in1Pin = 10; //deklaracja pinu IN1 w mostku

int in2Pin = 9; //deklaracja pinu IN2 w mostku


int switchPin = 7; // deklaracja pinu przycisku

int potPin = 0; // deklaracja pinu potencjometru


void setup()

{

  pinMode(in1Pin, OUTPUT); //ustawienie pinu na wyjście 
  
  pinMode(in2Pin, OUTPUT);
  
  pinMode(enablePin, OUTPUT);
  
  pinMode(switchPin, INPUT_PULLUP); //gdy wciśniety to silnika obraca się  zgodnie ze wskazówkami zegara gdy nie to w przeciwnym kierunku, 
  
}

void loop()

{

  int speed = analogRead(potPin) / 4; //odczytanie wartości obrotowej silnika z wejścia anlogowego, dzielona przez 4 ponieważ odczyt będzie z przedziału pomiędzy 0 a 1023, a na                                        wyjściu analogowym potrzebujemy zakresu od 0 do 255.
  
  boolean reverse = digitalRead(switchPin); //odczytanie wartości z przycisku 
  
  setMotor(speed, reverse); //funkca załączenia silnika
  
}


void setMotor(int speed, boolean reverse)

{

  analogWrite(enablePin, speed); //prędkość obrotową ustawiamy używając “analogWrite” na pinie “enable”
  
  digitalWrite(in1Pin, ! reverse); //funkcja kierunku obrotów w przeciwnym kierunku
  
  digitalWrite(in2Pin, reverse); //funkcja kierunku obrotów
  
}
```
