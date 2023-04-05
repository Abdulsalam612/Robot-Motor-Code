# Robot-Motor-Code
PS4 controller code into ESP32 for 4-wheeled motored car
#include <PS4Controller.h>
#include <ESP32_Servo.h>

Servo motor1;
Servo motor2;
Servo motor3;
Servo motor4;

const int in1 = 12;
const int in2 = 14;
const int in3 = 27;
const int in4 = 26;

// Define the speed variables
const int forward = 125;
const int backward = 55;
const int stop = 90;

// Define the delay between each movement
const unsigned long movementDelay = 100;

void setup() {
  Serial.begin(115200);
  PS4.begin("E8:61:7E:6B:93:30");

  attachMotors();
  initializeMotors();
}

void loop() {
  controlMotors();
}

void attachMotors() {
  motor1.attach(in1);
  motor2.attach(in2);
  motor3.attach(in3);
  motor4.attach(in4);
}

void initializeMotors() {
  motor1.write(stop);
  motor2.write(stop);
  motor3.write(stop);
  motor4.write(stop);
  delay(5000);
}

void controlMotors() {
  int lx = PS4.LStickX();
  int ly = PS4.LStickY();
  int ry = PS4.RStickY();
  int rx = PS4.RStickX();


  // Move Forwards and Backwards
  if (ly > 70) {
    // Forward movement
    if (rx > 70) {
      // Forward and right rotation
      motor1.write(backward);
      motor2.write(forward);
      motor3.write(forward);
      //motor4.write(forward);
    } else if (rx < -70) {
      // Forward and left rotation
      motor1.write(forward);
      motor2.write(forward);
      motor3.write(backward);
      //motor4.write(forward);
    } else {
      // Pure forward movement
      motor1.write(forward);
      motor2.write(forward);
      motor3.write(forward);
      //motor4.write(forward);
    }
    delay(movementDelay);
  } else if (ly < -70) {
    // Backward movement
    if (rx > 70) {
      // Backward and right rotation
      motor1.write(backward);
      motor2.write(backward);
      motor3.write(backward);
      //motor4.write(forward);
    } else if (rx < -70) {
      // Backward and left rotation
      motor1.write(backward);
      motor2.write(backward);
      motor3.write(forward);
      //motor4.write(backward);
    } else {
      // Pure backward movement
      motor1.write(backward);
      motor2.write(backward);
      motor3.write(backward);
      //motor4.write(backward);
    }
    delay(movementDelay);
  } else if (lx > 70) {
    // Steer right
    motor1.write(backward);
    motor2.write(backward);
    motor3.write(forward);
    //motor4.write(forward);
    delay(movementDelay);
  } else if (lx < -70) {
    // Steer left
    motor1.write(forward);
    motor2.write(forward);
    motor3.write(backward);
    //motor4.write(backward);
    delay(movementDelay);
  } else if (rx > 70) {
    // Right rotation
    motor1.write(backward);
    motor2.write(forward);
    motor3.write(stop);
    //motor4.write(stop);
    delay(movementDelay);
  } else if (rx < -70) {
    // Left rotation
    motor1.write(stop);
    motor2.write(stop);
    motor3.write(backward);
    //motor4.write(forward);
    delay(movementDelay);
   } else if (lx > 70 && ly > 70) {
    // Forward-Right Diagonal Movement
    motor1.write(stop);
    motor2.write(stop);
    motor3.write(forward);
    //motor4.write(forward);
    delay(movementDelay);
  } else if (lx < -70 && ly > 70) {
    // Forward-Left Diagonal Movement
    motor1.write(forward);
    motor2.write(forward);
    motor3.write(stop);
    //motor4.write(stop);
    delay(movementDelay);
    } else if (lx > 70 && ly < -70) {
    // Backward-right Diagonal Movement
    motor1.write(backward);
    motor2.write(backward);
    motor3.write(stop);
    //motor4.write(stop);
    delay(movementDelay);
  } else if (lx < -70 && ly < -70) {
    // Backward-Left Diagonal Movement
    motor1.write(stop);
    motor2.write(stop);
    motor3.write(backward);
    //motor4.write(backward);
    delay(movementDelay);
    }else if(PS4.Cross()){    
    dance();
  } else {
    // Center the wheels
    motor1.write(stop);
    motor2.write(stop);
    motor3.write(stop);
    //motor4.write(stop);
  }
}



void dance() {  
  // Dance moves for the car
  // Add the dance moves logic here...
  motor1.write(50);
     delay(20);
     motor2.write(130);
     delay(20);
     motor3.write(130);
     delay(20);
     motor4.write(50);     
     delay(1000);

     motor1.write(130);
     delay(20);
     motor2.write(50);
     delay(20);
     motor3.write(50);
     delay(20);
     motor4.write(130);     
     delay(1000);

     motor1.write(130);
     delay(20);
     motor2.write(130);
     delay(1000);

     motor1.write(50);
     delay(20);
     motor2.write(50);
     delay(1000);
     
     motor1.write(130);
     delay(20);
     motor2.write(130);
     delay(20);
     motor3.write(50);
     delay(20);
     motor4.write(50);     
     delay(1000);

     motor3.write(130);
     delay(20);
     motor4.write(130);     
     delay(1000); 

     motor3.write(50);
     delay(20);
     motor4.write(50);     
     delay(1000); 

     motor1.write(50);
     delay(20);
     motor2.write(130);
     delay(20);
     motor3.write(130);
     delay(20);
     motor4.write(50);     
     delay(3000);
     motor1.write(90);
     motor2.write(90);
     motor3.write(90);
     motor4.write(90);
     delay(300);
     
}
