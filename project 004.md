# 4-Digit 7-Segment Display with Arduino

## Introduction
A **4-digit 7-segment display** is commonly used for displaying numerical data, such as timers, counters, or temperature readings.
---

## Components Required
- **Arduino Uno** (or any compatible board)
- **4-Digit 7-Segment Display (Common Cathode or Anode)**
- **Resistors (220Ω - 470Ω) for segment current limiting**
- **Jumper wires**
- **Breadboard**

---

## Pin Configuration
A 4-digit 7-segment display typically consists of 7 LED segments (A to G) and a decimal point (DP). It also has 4 digit control pins (D1-D4) for multiplexing.

### Direct Drive:
| Segment | Arduino Pin |
|---------|------------|
| A       | D2         |
| B       | D3         |
| C       | D4         |
| D       | D5         |
| E       | D6         |
| F       | D7         |
| G       | D8         |
| DP      | D9         |
| D1      | D10        |
| D2      | D11        |
| D3      | D12        |
| D4      | D13        |

---

## Wiring Diagram

1. Connect segments A-G and DP through **220Ω resistors** to Arduino digital pins.
2. Connect digit control pins (D1-D4) to Arduino digital pins.
3. Connect display **common cathodes** to **GND**.
 
![image](https://github.com/user-attachments/assets/3dbae77f-4b85-4b64-a2b0-c34d9a8bf56b)

---
## Arduino Code
``cpp
const int segmentPins[] = {2, 3, 4, 5, 6, 7, 8, 9};
const int digitPins[] = {10, 11, 12, 13};
const byte numbers[10] = {
  0b00111111, // 0
  0b00000110, // 1
  0b01011011, // 2
  0b01001111, // 3
  0b01100110, // 4
  0b01101101, // 5
  0b01111101, // 6
  0b00000111, // 7
  0b01111111, // 8
  0b01101111  // 9
};

void displayDigit(int digit, int number) {
  digitalWrite(digitPins[digit], LOW);
  for (int i = 0; i < 8; i++) {
    digitalWrite(segmentPins[i], (numbers[number] >> i) & 1);
  }
  delay(5);
  digitalWrite(digitPins[digit], HIGH);
}

void setup() {
  for (int i = 0; i < 8; i++) {
    pinMode(segmentPins[i], OUTPUT);
  }
  for (int i = 0; i < 4; i++) {
    pinMode(digitPins[i], OUTPUT);
    digitalWrite(digitPins[i], HIGH);
  }
}

void loop() {
  for (int i = 0; i < 4; i++) {
    displayDigit(i, i); // Display numbers 0, 1, 2, 3 on 4 digits
  }
}
```

## Breakdown
(Multiplexing):
- Each digit is turned on one at a time in quick succession.
- Persistence of vision makes all digits appear simultaneously.
- Segments are controlled via binary encoding.

## Applications
- Digital clocks
- Temperature and humidity displays
- Countdown timers
- Scoreboards

---

## Conclusion
Using a **4-digit 7-segment display** with an **Arduino** can enhance many projects requiring numerical output. 
