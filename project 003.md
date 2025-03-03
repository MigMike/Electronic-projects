# ULN2003 Motor Driver 

## Overview
The **ULN2003** is a high-voltage, high-current Darlington transistor array commonly used for driving stepper motors, relays, and other inductive loads. It consists of **seven NPN Darlington pairs**, each capable of driving **500mA** and withstanding peak currents up to **600mA**.

## Features
- 7-channel Darlington transistor array
- Each channel can handle **50V** and **500mA** continuous current
- Built-in **freewheeling diodes** for inductive load protection
- **TTL/CMOS compatible inputs**
- Commonly used to drive **28BYJ-48 stepper motors**

## Pin Configuration
| Pin No | Name  | Description |
|--------|-------|-------------|
| 1-7    | IN1-IN7 | Input control pins |
| 8      | GND   | Ground |
| 9      | COM   | Common cathode for freewheeling diodes |
| 10-16  | OUT7-OUT1 | Output pins |

## Circuit Diagram
```
        +12V
         |
         |  Motor Coil
         |
 INx ----|------ OUTx
         |
         |  ULN2003
        GND
```
- ![image](https://github.com/user-attachments/assets/84976fbf-58c1-43d6-9652-cf2f43704098)


## Application Circuit: Driving a 28BYJ-48 Stepper Motor
### Connection Table
| ULN2003 Pin | Stepper Motor Coil |
|------------|------------------|
| OUT1       | Coil A |
| OUT2       | Coil B |
| OUT3       | Coil C |
| OUT4       | Coil D |


## Interfacing with Arduino
### Wiring
| ULN2003 | Arduino |
|---------|---------|
| IN1     | D8      |
| IN2     | D9      |
| IN3     | D10     |
| IN4     | D11     |
| GND     | GND     |
| COM     | +5V     |

### Arduino Code 

```cpp
#include <Stepper.h>
#define STEPS 2048
Stepper stepper(STEPS, 8, 10, 9, 11);

void setup() {
    stepper.setSpeed(10);
}

void loop() {
    stepper.step(2048);  // Full rotation
    delay(1000);
}
```

## Applications
- Stepper motor control
- Relay driving
- LED matrix and display driving
- Solenoid control

## Alternatives
- ULN2803 (8 channels)
- L293D (H-bridge for bidirectional motor control)

## Conclusion
The **ULN2003** is a simple yet powerful solution for controlling inductive loads like stepper motors and relays. It is widely used in embedded systems and automation projects due to its ease of use and reliability.

