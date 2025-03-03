
# CONTROLLING A STEPPER MOTOR WITH ARDUINO

## Introduction

- A stepper motor is a type of a brushless DC motor that divides a full rotation in equal steps.
- Both the stepper motor and arduino controll the speed and direction .

## coomponents required

- 28BYJ- 48 Stepper motor
- ULN2003 motor Driver
- Arduino board (uno,mega )
- Jumper wires
- Power supply 5v DC
-

## Wiring Diagram

 ULN2003                 Arduino pins
 IN1                     PIN8
 IN2                     PIN9
 IN3                     PIN10
 IN4                     PIN11
 VCC                     5V
 GND                     GND

-![image](https://github.com/user-attachments/assets/b6061d3c-e43b-49cd-90bd-3f74a4e11f87)

- The 28BYJ-48 stepper motor is connected to ULN2003 motor driver via an onboard white 5-pin connector.

## Arduino Code
``` CPP
#include <Stepper.h>

// Define the number of steps per revolution (change this according to your motor)
#define STEPS_PER_REV 200

// Initialize the stepper library with the steps per revolution and pin connections
Stepper stepper(STEPS_PER_REV, 8, 9, 10, 11);

void setup() {
  stepper.setSpeed(60); // Set speed to 60 RPM
  Serial.begin(9600);  // Initialize serial communication
}

void loop() {
  Serial.println("Moving forward");
  stepper.step(STEPS_PER_REV); // Move one full revolution forward
  delay(1000);

  Serial.println("Moving backward");
  stepper.step(-STEPS_PER_REV); // Move one full revolution backward
  delay(1000);
}


## Breakdown

- The Stepper library is included to handle stepper motor movement.
- The Stepper object is initialized with the number of steps per revolution and the control pins.
- The setSpeed() function sets the rotation speed in RPM.
- The step() function is used to move the motor forward and backward in steps.

## Root Cause Analysis

- If the motor vibrates but does not rotate, check the wiring.
- Ensure the correct sequence of motor driver inputs.
- Adjust the speed settings if the motor does not move smoothly.
- Make sure the motor is receiving sufficient power.

## Conclusion

- Using an Arduino with a ULN2003 driver makes it simple to control a stepper motor for precise movements. 
