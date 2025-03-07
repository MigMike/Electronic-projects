# Controlling a Stepper Motor Using Arduino 

## Introduction
Stepper motors are widely used in precision control applications like CNC machines, 3D printers, and robotics. The ULN2003 stepper driver allows easy interfacing between the stepper motor and an Arduino.

---

## Components Required

### 1. **Arduino (e.g., Arduino Uno)**
   - Acts as the brain of the system.
   - Sends control signals to the ULN2003 driver board.
   - Executes the step sequence to rotate the motor accurately.

### 2. **Stepper Motor (28BYJ-48)**
   - A unipolar stepper motor commonly used with the ULN2003 driver.
   - Has four phases and operates using a step sequence.
   - Provides precise angular movement control.

### 3. **ULN2003 Stepper Motor Driver Board**
   - Amplifies the low-power control signals from the Arduino to drive the stepper motor.
   - Uses Darlington transistor arrays to handle high current requirements.
   - Provides LED indicators for each phase to visualize operation.

### 4. **Power Supply (5V DC)**
   - Required to power the stepper motor.
   - The motor typically operates on 5V and draws significant current.
   - An external power supply is recommended rather than powering it from the Arduino.

### 5. **Jumper Wires**
   - Used to connect the components.
   - Ensures proper data and power transmission between the Arduino, ULN2003 driver, and stepper motor.

---

## Circuit Diagram

```
Arduino       ULN2003 Driver       Stepper Motor (28BYJ-48)
----------------------------------------------------------
  5V   --->   VCC                   (Power)
  GND  --->   GND                   (Ground)
  D8   --->   IN1
  D9   --->   IN2
  D10  --->   IN3
  D11  --->   IN4

ULN2003 Output pins connect to the motor's coils.
External 5V DC supply should used for motor power.
`![image](https://github.com/user-attachments/assets/f9baa52c-35d8-4e64-95e9-dc95a94bbb88)
``
---
## Arduino Code

```cpp
#include <Stepper.h>

#define STEPS 2048 // Steps per revolution for 28BYJ-48 motor

Stepper stepper(STEPS, 8, 10, 9, 11); // Define stepper motor control pins

void setup() {
    stepper.setSpeed(10); // Set speed in RPM
    Serial.begin(9600);
}

void loop() {
    Serial.println("Rotating Forward");
    stepper.step(STEPS); // Rotate one full revolution forward
    delay(1000);
    
    Serial.println("Rotating Backward");
    stepper.step(-STEPS); // Rotate one full revolution backward
    delay(1000);
}
```

---

## Code Breakdown

1. **Include the Stepper Library:** The `<Stepper.h>` library is included to simplify stepper motor control.
2. **Define Steps per Revolution:** The 28BYJ-48 motor has 2048 steps per revolution in full-step mode.
3. **Specify Control Pins:** The stepper motor is controlled using four pins (8, 9, 10, and 11).
4. **Set Speed:** The `setSpeed(10)` function sets the rotation speed to 10 RPM.
5. **Loop Execution:**
   - The motor rotates one full revolution forward.
   - Waits for a second.
   - Rotates one full revolution in reverse.
   - Repeats the cycle.

---

## Conclusion
Using an Arduino with a ULN2003 driver makes stepper motor control simple and efficient. This setup allows precise control of the motor's position and speed, making it ideal for automation projects. By modifying the code, you can achieve various movement patterns based on your application needs.

