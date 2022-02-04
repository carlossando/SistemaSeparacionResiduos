//pantalla
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x20,16,2);
//fin pantalla

//motorPasos
#include <Stepper.h>
const int stepsPerRevolution =20;
Stepper stepperA(stepsPerRevolution, A1, A2,A3, A4);
int stepperCounter =0;
//fin motor pasos
//botones y leds
int botonRojo = 2;//plastico
int ledRojo=3;
int botonAmarillo = 4;//metal
int ledAmarillo = 5;
int botonVerde = 7;//Carton
int ledVerde = 6;
int botonAzul = 8;//Vidrio
int ledAzul = 10;
//fin de botones y leds
//servo
#include <Servo.h>
Servo myservo;
int pos = 0; 
//fin servo

//declaracion de funciones
void motorPasos();
void abrirCompuerta();

void setup() {
  // 
  myservo.attach(9); //el servo
  lcd.init(); // Pantalla
  lcd.backlight();//pantalla
  pinMode(botonRojo,INPUT);
  digitalWrite(botonRojo,HIGH);
  pinMode(botonAmarillo,INPUT);
  digitalWrite(botonAmarillo,HIGH);
  pinMode(botonVerde,INPUT);
  digitalWrite(botonVerde,HIGH);
  pinMode(botonAzul,INPUT);
  digitalWrite(botonAzul,HIGH);
  
  pinMode(ledRojo, OUTPUT);
  pinMode(ledAmarillo, OUTPUT);
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAzul, OUTPUT);
  //motor a pasos
  pinMode(A1, OUTPUT);
  pinMode(A2, OUTPUT);
  pinMode(A3, OUTPUT);
  pinMode(A4, OUTPUT);
  stepperA.setSpeed(60);
  //fin motor a pasos

}

void loop() {
  if(digitalRead(botonRojo)== LOW){
    digitalWrite(ledRojo, HIGH);
    lcd.clear();
    lcd.print("Plastico");
    motorPasos();
}else{
  digitalWrite(ledRojo, LOW);
}
if(digitalRead(botonAmarillo)== LOW){
    digitalWrite(ledAmarillo, HIGH);
    lcd.clear();
    lcd.print("Metal");
    motorPasos();
}else{
  digitalWrite(ledAmarillo, LOW);
}
//
if(digitalRead(botonVerde)== LOW){
    digitalWrite(ledVerde, HIGH);
    lcd.clear();
    lcd.print("Carton");
    motorPasos();
}else{
  digitalWrite(ledVerde, LOW);
}
if(digitalRead(botonAzul)== LOW){
    digitalWrite(ledAzul, HIGH);
    lcd.clear();
    lcd.print("Vidrio");
    motorPasos();
}else{
  digitalWrite(ledAzul, LOW);
}

}
void motorPasos(){
  for(int i=0; i<1;i++){
    stepperA.step(stepsPerRevolution);
  }
  delay(500);
  abrirCompuerta();
  for(int j=0; j<1; j++){
    stepperA.step(-stepsPerRevolution);
  }
  delay(500);
  }// cierra motorPasos
  
  void abrirCompuerta(){
    for (pos = 0; pos <= 180; pos += 1) { // goes from 0 degrees to 180 degrees
    // in steps of 1 degree
    myservo.write(pos);              // tell servo to go to position in variable 'pos'
    delay(15);                       // waits 15ms for the servo to reach the position
  }
  for (pos = 180; pos >= 0; pos -= 1) { // goes from 180 degrees to 0 degrees
    myservo.write(pos);              // tell servo to go to position in variable 'pos'
    delay(15);                       // waits 15ms for the servo to reach the position
  }
  }//cierra abrir compuerta
  
