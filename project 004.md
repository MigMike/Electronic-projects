# 4-Digit 7-Segment Display with Arduino

## Introduction
A 4-digit 7-segment display is commonly used for displaying numerical data, such as timers, counters, or temperature readings. It provides a simple yet effective way to show numerical information in embedded systems.

## Components Required
1. **Arduino Uno (or any compatible board)**
   - The microcontroller processes data and controls the display through digital pins.
   - Provides power and logic control for the display.

2. **4-Digit 7-Segment Display (Common Cathode or Anode)**
   - Consists of four 7-segment displays that share common segment pins.
   - Uses multiplexing to display numbers efficiently.

3. **Resistors (220Ω - 470Ω) for segment current limiting**
   - Limits the current flowing through each LED segment to prevent damage.
   - Ensures appropriate brightness of the display.

4. **Jumper Wires**
   - Used to make connections between the Arduino, display, and breadboard.
   - Ensures reliable signal transmission.

5. **Breadboard**
   - Provides a convenient way to connect components without soldering.
   - Helps organize the wiring and connections efficiently.

## Pin Configuration
A 4-digit 7-segment display typically consists of 7 LED segments (A to G) and a decimal point (DP). It also has 4 digit control pins (D1-D4) for multiplexing.

### Direct Drive Pin Mapping
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

## Wiring Diagram
- Connect segments A-G and DP through 220Ω resistors to Arduino digital pins.
- Connect digit control pins (D1-D4) to Arduino digital pins.
- Connect display common cathodes to GND.
---
![image](https://github.com/user-attachments/assets/e5d35ac6-6f35-481c-b085-e15693d95e7f)

---
## Arduino Code
```cpp
#define A 2
#define B 3
#define C 4
#define D 5
#define E 6
#define F 7
#define G 8
#define DP 9

#define DIGIT1 10
#define DIGIT2 11
#define DIGIT3 12
#define DIGIT4 13

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

const int segmentPins[8] = {A, B, C, D, E, F, G, DP};
const int digitPins[4] = {DIGIT1, DIGIT2, DIGIT3, DIGIT4};

int displayNumber = 1234;

void setup() {
    for (int i = 0; i < 8; i++) {
        pinMode(segmentPins[i], OUTPUT);
    }
    for (int i = 0; i < 4; i++) {
        pinMode(digitPins[i], OUTPUT);
    }
}

void displayDigit(int digit, int pos) {
    digitalWrite(DIGIT1, HIGH);
    digitalWrite(DIGIT2, HIGH);
    digitalWrite(DIGIT3, HIGH);
    digitalWrite(DIGIT4, HIGH);
    
    for (int i = 0; i < 8; i++) {
        digitalWrite(segmentPins[i], (numbers[digit] >> i) & 1);
    }
    
    digitalWrite(digitPins[pos], LOW);
    delay(5);
    digitalWrite(digitPins[pos], HIGH);
}

void loop() {
    int num = displayNumber;
    for (int i = 3; i >= 0; i--) {
        displayDigit(num % 10, i);
        num /= 10;
    }
}
```

## Breakdown
### Direct Drive (Multiplexing)
- Each digit is turned on one at a time in quick succession.
- Persistence of vision makes all digits appear simultaneously.
- Segments are controlled via binary encoding.

## Conclusion
Using a 4-digit 7-segment display with an Arduino can enhance many projects requiring numerical output. Understanding how to wire, code, and control the display is essential for integrating it into timers, clocks, and data readouts.

