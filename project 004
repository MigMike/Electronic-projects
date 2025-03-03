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
// Pin definitions
const int segmentPins[] = {2, 3, 4, 5, 6, 7, 8, 9}; // A, B, C, D, E, F, G, DP
const int digitPins[] = {10, 11, 12, 13}; // D1, D2, D3, D4

// Digit patterns for 0-9 (Common Anode: LOW to turn segment ON, HIGH for OFF)
const byte numbers[10] = {
  0b11000000, // 0
  0b11111001, // 1
  0b10100100, // 2
  0b10110000, // 3
  0b10011001, // 4
  0b10010010, // 5
  0b10000010, // 6
  0b11111000, // 7
  0b10000000, // 8
  0b10010000  // 9
};

// Number to display (example: 1234)
int digits[4] = {1, 2, 3, 4};

// Function to display a digit
void displayDigit(int digit, int number) {
  digitalWrite(digitPins[digit], LOW); // Activate digit (LOW for common anode, HIGH for common cathode)

  // Set segments
  for (int i = 0; i < 8; i++) {
    digitalWrite(segmentPins[i], bitRead(numbers[number], i)); // Set segment state
  }

  delay(5); // Small delay for persistence
  digitalWrite(digitPins[digit], HIGH); // Deactivate digit
}

void setup() {
  for (int i = 0; i < 8; i++) pinMode(segmentPins[i], OUTPUT);
  for (int i = 0; i < 4; i++) pinMode(digitPins[i], OUTPUT);
}

void loop() {
  for (int i = 0; i < 4; i++) {
    displayDigit(i, digits[i]);
  }
}

## Breakdown
Direct Drive (Multiplexing):

. Each digit is turned on one at a time in quick succession.
. Persistence of vision makes all digits appear simultaneously.
. Segments are controlled via binary encoding.

## Conclusion
- Using a 4-digit 7-segment display with an Arduino can enhance many projects requiring numerical output. 
