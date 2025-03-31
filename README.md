// C++ code
//
#include <Servo.h>

int pot_base = 0;

int pot_giro = 0;

int pot_altura = 0;

int pot_medio = 0;

int pot_garra = 0;

int angulo_base = 0;

int angulo_altura = 0;

int angulo_garra = 0;

int angulo_medio = 0;

int angulo_giro = 0;

Servo servo_8;

Servo servo_9;

Servo servo_10;

Servo servo_11;

Servo servo_12;

void setup()
{
  pinMode(A4, INPUT);
  pinMode(A3, INPUT);
  pinMode(A2, INPUT);
  pinMode(A1, INPUT);
  pinMode(A0, INPUT);
  servo_8.attach(8, 500, 2500);
  servo_9.attach(9, 500, 2500);
  servo_10.attach(10, 500, 2500);
  servo_11.attach(11, 500, 2500);
  servo_12.attach(12, 500, 2500);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(2, OUTPUT);
}

void loop()
{
  // LEEMOS LOS POTENCIOMETROS
  pot_base = analogRead(A4);
  pot_giro = analogRead(A3);
  pot_altura = analogRead(A2);
  pot_medio = analogRead(A1);
  pot_garra = analogRead(A0);
  // LOS CONVERTIMOS EN ANGULOS
  angulo_base = map(pot_base, 0, 1023, 0, 180);
  angulo_giro = map(pot_giro, 0, 1023, 0, 90);
  angulo_altura = map(pot_altura, 0, 1023, 0, 180);
  angulo_medio = map(pot_medio, 0, 1023, 0, 180);
  angulo_garra = map(pot_garra, 0, 1023, 0, 90);
  // GIRAMOS LOS SERVOS
  servo_8.write(angulo_base);
  servo_9.write(angulo_giro);
  servo_10.write(angulo_altura);
  servo_11.write(angulo_medio);
  servo_12.write(angulo_garra);
  // SI LA GARRA ESTA RECTA; O ESTA ACOSTADA
  // O ESTA EN SU MAXIMA ALTURA, POR LO TANTO
  if (angulo_altura > 75 && angulo_medio > 75) {
    // NO ES DE COLOR AMARILLO
    digitalWrite(3, LOW);
    if (angulo_giro > 75) {
      // ESTA RECOSTADA, POR LO TANTO ES VERDE
      digitalWrite(4, HIGH);
      digitalWrite(2, LOW);
    } else {
      // ESTA DE PIE; POR LO TANTO ES ROJO
      digitalWrite(4, LOW);
      digitalWrite(2, HIGH);
    }
  } else {
    // NO ESTA RECTA; POR LO TANTO ES AMARILLO
    digitalWrite(3, HIGH);
  }
  delay(10); // Delay a little bit to improve simulation performance
}
