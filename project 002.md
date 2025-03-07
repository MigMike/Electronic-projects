# ULN2003 Motor Driver

## Introduction
The **ULN2003** is a popular Darlington transistor array used to drive **stepper motors, relays, solenoids, and high-power LEDs**. It is commonly used with **28BYJ-48 stepper motors** in automation and robotics applications. The ULN2003 is designed to interface with **TTL/CMOS logic devices**, allowing low-power microcontrollers to control high-power loads.

## Features
- 7 Darlington transistor pairs
- High voltage (up to **50V**) and high current (up to **500mA** per channel)
- Built-in **flyback diodes** for protection against voltage spikes
- TTL and CMOS logic compatible inputs
- **Common-cathode clamping diodes** for inductive load protection
- Available in **DIP16, SO16, and TSSOP16** packages

## Pinout
The **ULN2003** has 16 pins:

| Pin Number | Name        | Function |
|------------|------------|----------|
| 1-7        | **IN1 - IN7** | Input control pins from microcontroller (TTL/CMOS) |
| 8          | **GND**       | Ground connection |
| 9          | **COM**       | Common cathode for flyback diodes (connect to motor supply voltage) |
| 10-16     | **OUT7 - OUT1** | Output pins to drive loads |
---
![image](https://github.com/user-attachments/assets/23320022-0c57-4870-b044-12df05a76cd0)

---
## Components Required:

### 1. **Darlington Transistor Pairs**
Each channel in the ULN2003 consists of a **Darlington transistor pair**, which provides high current gain. This configuration allows a small input current to control a large output current, making it ideal for driving motors and relays.
- Boosts the control signal from the microcontroller.
- Allows low-power devices to control high-power loads efficiently.

### 2. **Input Resistors (2.7kΩ)**
Each input pin has a built-in **2.7kΩ pull-down resistor**, which helps stabilize the input voltage when the driving source is disconnected or in a floating state.
- Ensures the input does not remain in an undefined state.
- Reduces unintended switching due to noise.

### 3. **Base Resistors (≈ 2.7kΩ - 10kΩ)**
Each Darlington transistor pair has a **base resistor** to limit the base current, preventing excessive current flow that could damage the transistors.
- Controls current to the transistor base.
- Enhances the reliability of the driver circuit.

### 4. **Flyback Diodes (Clamp Diodes)**
The **internal flyback diodes** (also called freewheeling or snubber diodes) protect the circuit against **back EMF** (Electromotive Force) generated when switching inductive loads like motors and relays.
- Prevents voltage spikes that could damage transistors and other components.
- Improves the longevity of the motor driver.

### 5. **Common Cathode Diode Network (Pin 9 - COM)**
The **COM** pin is connected to the power supply voltage of the load (e.g., +5V or +12V). It acts as a common node for the flyback diodes.
- Ensures proper operation of the internal protection diodes.
- Must be connected to the same voltage as the motor supply.

## Applications
- Driving **28BYJ-48 stepper motors**
- Controlling **relays and solenoids**
- Operating **high-power LEDs** and **lamps**
- Signal amplification for **microcontroller outputs**
- Industrial and **automotive applications**

## Example Usage: ULN2003 with 28BYJ-48 Stepper Motor
The **ULN2003** is commonly used to drive a **28BYJ-48 stepper motor**. 

### Connections:
| **ULN2003 Pin** | **Microcontroller (e.g., Arduino) / Motor** |
|-----------------|--------------------------------|
| IN1 - IN4      | Digital Pins (e.g., D8 - D11) |
| OUT1 - OUT4    | 28BYJ-48 Motor Coils |
| COM            | Motor Supply (5V/12V) |
| GND            | Common Ground |

### Arduino Code 
```cpp
#define IN1 8
#define IN2 9
#define IN3 10
#define IN4 11

void setup() {
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);
}

void loop() {
    digitalWrite(IN1, HIGH);
    delay(10);
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, HIGH);
    delay(10);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, HIGH);
    delay(10);
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, HIGH);
    delay(10);
    digitalWrite(IN4, LOW);
}
```

## Conclusion
The **ULN2003 motor driver** is a simple, efficient, and widely used component in motor control applications. Its built-in protection diodes, Darlington transistor pairs, and TTL compatibility make it an ideal choice for interfacing microcontrollers with high-power loads.

