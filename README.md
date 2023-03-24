#include <IRremote.h>     
#define Tecla_1 0xFF00BF00    
#define Tecla_2 0xFE01BF00  

// RIEGO GOTEO
int bomba = 0;
int sensor1 = A0;
int sensor2 = A1;
int sensor3 = A2;
int sensor4 = A3;
int s1 = 0;
int s2 = 0;
int s3 = 0;
int s4 = 0;
int VN = 900;
// RIEGO GOTEO
// fertilizante
int sensorNivel = 10;
int valvulaN = 4;
int valvulaA = 5;
int tamañoTinaco = #; 
int nivelAgua = 0;
// fertilizante

// luz azul & luz roja

// luz azul & luz roja

// otro
int control = 13;
int humedad = 10;
int sensorGotas = 9;
int agua = 0;
int valH = 0;
int val = 0;
// otro



void setup() {
pinMode(humedad,OUTPUT);
pinMode(valvulaN,OUTPUT);
pinMode(ledR,OUTPUT);
pinMode(bomba,OUTPUT);
pinMode(sensor1,INPUT);
pinMode(sensor2,INPUT);
pinMode(sensor3,INPUT);
pinMode(sensor4,INPUT);
pinMode(sensorGotas,INPUT);
pinMode(sensorNivel,INPUT);
IrReceiver.begin(control, DISABLE_LED_FEEDBACK); 
}

void loop() {
// riego goteo
s1 =analogRead(sensor1);
s2 =digitalRead(sensor2);
s3 =digitalRead(sensor3);
s4 =digitalRead(sensor4);
if (s1 >= VN && s2 >= VN){  
digitalWrite(bomba,HIGH);

}
else{
digitalWrite(bomba,LOW);
}
// riego goteo

// CONTROL
if (IrReceiver.decode()) {        
Serial.println(IrReceiver.decodedIRData.decodedRawData, HEX); 
if (IrReceiver.decodedIRData.decodedRawData == Tecla_1){
valH = 300;
}   
if (IrReceiver.decodedIRData.decodedRawData == Tecla_2){
valH = 100;
} 
IrReceiver.resume();       
}
delay (100);            
// CONTROL

// humedad relativa
val = analogRead(sensorGotas);
if (val <= valH && nivelAgua == 1){
digitalWrite(humedad,HIGH);
}
else {
digitalWrite(humedad,LOW);
}
// humedad relativa

// fertilizante
nivelAgua = digitalRead(sensorNivel);
if (nivelAgua == 1){
digitalWrite(valvulaN,HIGH);
digitalWrite(valvulaA,HIGH);
delay(100 * tamañoTinaco);
digitalWrite(valvulaN,LOW);
delay(4900 * tamañoTinaco);
digitalWrite(valvulaA,LOW)
}
}
}
