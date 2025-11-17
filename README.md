Fire is one of the most destructive hazards that can occur in homes, offices, or industries. In many cases, delay in human response leads to severe damage and loss. To overcome this, an automatic fire detection and extinguishing system can help respond immediately.Our project presents a prototype model that can detect fire using a flame sensor and automatically spray water using a servo-controlled sprayer, all managed by an Arduino Nano microcontroller. The system is low-cost, efficient, and can operate independently without human supervision.
```cpp
#include <Servo.h>

Servo servo1;
Servo servo2;

int irPin = 2;      // IR sensor output pin
int servo1Pin = 9;  // Servo 1 signal pin
int servo2Pin = 10; // Servo 2 signal pin

void setup() {
  pinMode(irPin, INPUT);

  servo1.attach(servo1Pin);
  servo2.attach(servo2Pin);

  servo1.write(0);  // Start position
  servo2.write(0);

  Serial.begin(9600);
  Serial.println("System Ready");
}

void loop() {
  int irState = digitalRead(irPin);

  if (irState == LOW) { // IR detects object
    Serial.println("Detected!");

    // Sweep to 90 degrees smoothly
    for(int pos = 0; pos <= 90; pos++){
      servo1.write(pos);
      servo2.write(pos);
      delay(10);
    }

    delay(500); // Hold position for half second

    // Return to 0 degrees
    for(int pos = 90; pos >= 0; pos--){
      servo1.write(pos);
      servo2.write(pos);
      delay(10);
    }

  } else {
    // No detection
    servo1.write(0);
    servo2.write(0);
  }
}
```
