# PUSH-BUTTON-COUNTER-TASK-01

This project is a simple embedded system application that counts the number of times a push button is pressed and displays the count in real-time.  
It’s ideal for learning basic **microcontroller I/O**, **debouncing techniques**, and **digital input handling**.

---

## 📜 Project Overview
- **Microcontroller:** Arduino Uno R3  
- **Display:** I2C 16x2 LCD  
- **Input:** 4-pin Push Button  
- **Output:** Real-time count on LCD  
- **Simulation:** [View on Wokwi](https://wokwi.com/projects/437828967903221761)  

---

## 🛠 Components Used

| Component         | Quantity | Description                        |
|-------------------|----------|------------------------------------|
| Arduino Uno R3    | 1        | Main microcontroller board         |
| I2C LCD 16x2      | 1        | Displays the counter value         |
| Push Button (4-pin)| 1       | Input device to increment the count|
| Jumper Wires      | ~6       | For wiring                         |

---

## ⚡ Circuit Connections

### **I2C LCD:**
- **VCC** → 5V  
- **GND** → GND  
- **SDA** → A4  
- **SCL** → A5  

### **Push Button:**
- **One leg** → Digital Pin D2  
- **Opposite leg** → GND  

---

## 💻 Code Overview
The Arduino reads the digital input from the push button.  
When pressed, it increments a counter and updates the LCD display with the new count.

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

#define BUTTON_PIN 2
LiquidCrystal_I2C lcd(0x27, 16, 2);

int counter = 0;
int lastButtonState = LOW;

void setup() {
  pinMode(BUTTON_PIN, INPUT);
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("Push Counter:");
  lcd.setCursor(0, 1);
  lcd.print("Count: 0");
}

void loop() {
  int currentState = digitalRead(BUTTON_PIN);
  if (currentState == HIGH && lastButtonState == LOW) {
    counter++;
    lcd.setCursor(0, 1);
    lcd.print("Count: ");
    lcd.print(counter);
    lcd.print("    ");
    delay(200);
  }
  lastButtonState = currentState;
}
