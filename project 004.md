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
 
- ![image](https://github.com/user-attachments/assets/a28170df-3e96-43ee-8c10-2ed61f35c264)

---
## Arduino Code 
// Define segment pins (A to G and DP)
const int segmentPins[] = {2, 3, 4, 5, 6, 7, 8, 9};

// Define digit select pins
const int digitPins[] = {10, 11, 12, 13};

// Digit patterns for numbers 0-9 (Common Cathode)
const byte digitPatterns[10] = {
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

void setup() {
    // Set segment pins as output
    for (int i = 0; i < 8; i++) {
        pinMode(segmentPins[i], OUTPUT);
    }
    // Set digit control pins as output
    for (int i = 0; i < 4; i++) {
        pinMode(digitPins[i], OUTPUT);
    }
}

void displayNumber(int number) {
    int digits[4] = {
        number / 1000,          // Extract thousands
        (number / 100) % 10,    // Extract hundreds
        (number / 10) % 10,     // Extract tens
        number % 10             // Extract ones
    };

    for (int i = 0; i < 4; i++) {
        digitalWrite(digitPins[i], LOW);  // Activate digit
        setSegments(digitPatterns[digits[i]]);
        delay(5);  // Multiplexing delay
        digitalWrite(digitPins[i], HIGH); // Deactivate digit
    }
}

void setSegments(byte pattern) {
    for (int i = 0; i < 8; i++) {
        digitalWrite(segmentPins[i], (pattern >> i) & 0x01);
    }
}

void loop() {
    for (int num = 0; num <= 9999; num++) {
        unsigned long start = millis();
        while (millis() - start < 1000) {
            displayNumber(num);
        }
    }
}


## Breakdown
Direct Drive (Multiplexing):

. Each digit is turned on one at a time in quick succession.
. Persistence of vision makes all digits appear simultaneously.
. Segments are controlled via binary encoding.

## Conclusion
- Using a 4-digit 7-segment display with an Arduino can enhance many projects requiring numerical output. 
