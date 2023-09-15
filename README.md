# RFIDmotorControl
Control motor with RFID UID system
#include <SoftwareSerial.h>
#include <Servo.h>

SoftwareSerial mySerial(A1, A0);
Servo servo; 
Servo servo1;

int i;
int pos = 0; 
int pos1 = 30; 
int pos2 = 60; 
bool motorActivated = false; 

void setup() {
  mySerial.begin(9600);
  Serial.begin(9600);

  servo.attach(9); 
  servo1.attach(10);

  servo.write(0);
  servo1.write(180);

  pinMode(8,OUTPUT); //Enable
  pinMode(2,OUTPUT); //Step
  pinMode(5,OUTPUT); //Direction
}

char str[256] = {0,};
int idx = 0;

void loop() {
  if (mySerial.available()) { 
    char data = mySerial.read();
    St동
        if (!motorActivated) { 
        activateMotor();
      }
    }
      idx = 0;
    }
  }  
}
String transformUID(String uid) {
  if (uid.indexOf("B5") != -1) {       //uid.indexOf사용시 해당 UID에 ""안 문장 포함시 A값으로 변환
    return "A";
  } else if (uid.indexOf("45") != -1) {
    return "B";
  } else if (uid.indexOf ("93") != -1) {
    return "C";
  } else if (uid.indexOf  ("A6") != -1) {
    return "D";
  } else {
    return "Unknown";
  }
}


void activateMotor() {
 digitalWrite(8, LOW);
  digitalWrite(5, LOW);
  digitalWrite(2, LOW);

  delay(1000);

  for(i = 0 ; i < 920 ; i++)
  {
    digitalWrite(2, LOW);
    delay(5);
    digitalWrite(2, HIGH);
    }
    delay(1000);
      digitalWrite(5, HIGH);

   for (pos = 0; pos <= 30; pos += 1) { 
    servo.write(pos);             
    servo1.write(180 - pos);  
    delay(100);                    
  }
  for (pos1 = 30; pos1 <= 60; pos1 += 1) { 
    servo.write(pos1);             
    servo1.write(180 - pos1);                     
    delay(100);
  }
    for (pos2 = 60; pos2 <= 90; pos2 += 1) { 
    servo.write(pos2);             
    servo1.write(180 - pos2);
    delay(100);
  }
  delay(6000);
   for (pos = 90; pos >= 0; pos -= 1) { 
    servo.write(pos);
    servo1.write(180 - pos);
    delay(100);                     
  }
  delay(2000);

for(i = 0 ; i < 920 ; i++)
  {
    digitalWrite(2, LOW);
    delay(5);
    digitalWrite(2, HIGH);
    }
  motorActivated = false; 
}

