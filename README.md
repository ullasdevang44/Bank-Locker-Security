# Bank Locker Security System using GSM & RFID

## Overview
This project aims to develop a **Bank Locker Security System** using **RFID and GSM technologies**. The system ensures only authorized users can access the locker. If an unauthorized person attempts access, an alert will be sent to the registered mobile number via **GSM module**.

## Features
- **RFID Authentication**: Uses RFID tags to verify users.
- **GSM Alert System**: Sends SMS alerts in case of unauthorized access.
- **Microcontroller-based Control**: Uses an **Arduino/ESP32** to process authentication.
- **Automatic Locker Mechanism**: The locker door opens automatically upon successful authentication.
- **Enhanced Security**: Prevents unauthorized access with real-time alerts.

## Components Used
- **Microcontroller**: Arduino Uno / ESP32
- **RFID Module**: MFRC522 (or similar)
- **RFID Tags**: Passive RFID cards for authentication
- **GSM Module**: SIM800L/SIM900
- **Servo Motor**: To open/close the locker
- **LCD Display (16x2)**: To show authentication messages
- **Buzzer**: Alarm for unauthorized access
- **Power Supply**: 12V/5V adapter

## Working Principle
1. The **RFID reader** scans the tag.
2. The **microcontroller** checks if the tag ID is valid.
   - If valid: The **servo motor** opens the locker.
   - If invalid: The **GSM module** sends an alert to the user’s mobile.
3. The system logs all access attempts.
4. The locker remains secure when not in use.

## Circuit Diagram
(Include a circuit diagram or a link to one)

## Installation & Setup
1. **Clone the Repository:**
   ```sh
   git clone https://github.com/yourusername/bank-locker-system.git
   cd bank-locker-system
   ```
2. **Install Arduino Libraries:**
   - MFRC522 Library (for RFID module)
   - Servo Library (for motor control)
   - SoftwareSerial Library (for GSM communication)
3. **Upload the Code:**
   - Open the Arduino IDE.
   - Select the correct board (Arduino Uno / ESP32).
   - Upload the provided code.

## Code (Main Logic)
```cpp
#include <SPI.h>
#include <MFRC522.h>
#include <Servo.h>
#include <SoftwareSerial.h>

#define SS_PIN 10
#define RST_PIN 9
#define SERVO_PIN 6
#define BUZZER_PIN 7

Servo lockerServo;
SoftwareSerial gsm(2, 3); // RX, TX for GSM module
MFRC522 mfrc522(SS_PIN, RST_PIN);

String authorizedUID = "12345678"; // Change this to match your RFID tag UID

void setup() {
    Serial.begin(9600);
    gsm.begin(9600);
    SPI.begin();
    mfrc522.PCD_Init();
    lockerServo.attach(SERVO_PIN);
    pinMode(BUZZER_PIN, OUTPUT);
    Serial.println("Bank Locker System Initialized");
}

void loop() {
    if (!mfrc522.PICC_IsNewCardPresent() || !mfrc522.PICC_ReadCardSerial())
        return;

    String uid = "";
    for (byte i = 0; i < mfrc522.uid.size; i++)
        uid += String(mfrc522.uid.uidByte[i], HEX);

    Serial.println("Scanned UID: " + uid);
    
    if (uid == authorizedUID) {
        Serial.println("Access Granted");
        lockerServo.write(90);
        delay(5000);
        lockerServo.write(0);
    } else {
        Serial.println("Access Denied - Sending Alert");
        digitalWrite(BUZZER_PIN, HIGH);
        gsm.print("AT+CMGF=1\r");
        delay(1000);
        gsm.print("AT+CMGS=\"+919876543210\"\r");
        delay(1000);
        gsm.print("Unauthorized Access Attempted!");
        gsm.write(26);
        digitalWrite(BUZZER_PIN, LOW);
    }
    delay(2000);
}
```

## Future Enhancements
- Implement **Biometric Authentication** (Fingerprint Scanner)
- Integrate **IoT Monitoring** for real-time tracking
- Use **Face Recognition** for higher security

## GitHub Repository Setup
1. **Create a new GitHub repository:**
   - Go to [GitHub](https://github.com/) and create a new repo: `bank-locker-system`
2. **Push the code to GitHub:**
   ```sh
   git init
   git add .
   git commit -m "Initial Commit - Bank Locker System"
   git branch -M main
   git remote add origin https://github.com/yourusername/bank-locker-system.git
   git push -u origin main
   ```

## Conclusion
This project provides **enhanced security** for bank lockers by integrating **RFID and GSM** technologies. The **automated access control** and **real-time alert system** make it a highly secure solution for banks, offices, and homes.

---
**Author:** Your Name  
**GitHub:** [Your GitHub Profile](https://github.com/yourusername)  
**Date:** March 2025
