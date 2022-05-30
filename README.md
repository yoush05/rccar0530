# rccar0530

#include <SoftwareSerial.h>
SoftwareSerial BTSerial(12, 13);   //(RX,TX)이다. 

int motor1PinA  = 2  ;
int motor1PinB  = 3  ;
int enablelPin  =11 ;   
int motor2PinA  = 4  ;
int motor2PinB  = 5  ;
int enableRpin  = 10 ;  

변수선언..

char in;
   void setup() {
        BTSerial.begin(9600);//블루투스 통신
        Serial.begin(9600);//시리얼통신
    
        pinMode(motor1PinA, OUTPUT);
        pinMode(motor1PinB, OUTPUT);
        pinMode(motor2PinA, OUTPUT);
        pinMode(motor2PinB, OUTPUT);
        pinMode(enableRpin, OUTPUT);
        pinMode(enablelPin, OUTPUT);

        // set enablePin high so that motor can turn on:
       analogWrite(enableRpin, 250);
       analogWrite(enablelPin, 250);
       }
       보이드 셋업은 여기까지이다. 
       
         void loop() {
       if (BTSerial.available())
          { in =BTSerial.read();S
            Serial.write(in);
         }
         if (Serial.available()) 
          {  BTSerial.write(Serial.read());
             Serial.print("data =");
           Serial.println(in);
          }
          
          
             switch(in){
               case 'F':Forward(); break;
               case 'R': Right(); break; 
               case 'S': Stop(); break;
               case 'L': Left(); break;
               case 'B': Back(); break;
               case 'G': FowardLeft(); break;
             } 
      }  
      함수를 선언해버린다. 앱의 setting에 있는 값 그대로 선언하였다.
  
  여기서부터 각각의 함수에 대한 내용을 설정해준다. 
      void Back(){  
    digitalWrite(motor1PinA, HIGH);
 digitalWrite(motor1PinB, LOW);
 digitalWrite(motor2PinA, HIGH);
 digitalWrite(motor2PinB, LOW);
}
일단 여기서는 뒤로가는 코드를 했다. 

void Right(){  
     digitalWrite(motor1PinA, HIGH);
 digitalWrite(motor1PinB, HIGH);
 digitalWrite(motor2PinA, LOW);
 digitalWrite(motor2PinB, HIGH);
}
왼쪽바퀴만 돌린다. 오른쪽 바퀴는 돌리지 않는다. 

void Stop(){  
    digitalWrite(motor1PinA, HIGH);
       digitalWrite(motor1PinB,HIGH);
       digitalWrite(motor2PinA,HIGH);
       digitalWrite(motor2PinB,HIGH);
}
멈춘다. 그냥 다 하이로 두니까 모든 바퀴가 멈춰버린다. 

void Left(){  
     digitalWrite(motor1PinA, LOW);
 digitalWrite(motor1PinB, HIGH);
 digitalWrite(motor2PinA, LOW);
 digitalWrite(motor2PinB, LOW);
}
오른쪽 바퀴만 돌린다. 왼쪽 바퀴만 돌리게 된다. 

void Forward(){  
     digitalWrite(motor1PinA, LOW);
 digitalWrite(motor1PinB, HIGH);
 digitalWrite(motor2PinA, LOW);
 digitalWrite(motor2PinB, HIGH);
}
앞으로 가는 코드를 짰다. 원래는 앞으로만 가는 코드를 쓰려 했으나 .. 앞으로 가는 코드가 순서가 꼬여버렸다. 

void FowardLeft(){  
  analogWrite(enablelPin,100);
 analogWrite(enableRpin, 200);
 digitalWrite(motor1PinA, LOW);
 digitalWrite(motor1PinB, HIGH);
 digitalWrite(motor2PinA, LOW);
 digitalWrite(motor2PinB, HIGH);
}
앞으로 가면서 왼쪽으로 가는 코드이다. 먼저 속도를 바꿔준다. 오른쪽 바퀴 속도를 상대적으로 더 빠르게 해줬다. 

코드는 똑바로 한거같은데,, 근데 오른쪽 뒤 바퀴가 안돌아간다. 그래서 속도가 너무 느리다.
아마도 선 연결이 문제인거같다. 선이 계속 빠지는게 문제일수도 있고, 합선이 된거일수도 있는거같다. 
문제를 찾아내는 과정이 중요한거같은데 이번시간 안에는 하지 못하겠다. 
