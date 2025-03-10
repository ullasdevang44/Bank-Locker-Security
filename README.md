# Bank Locker Security System using GSM & RFID (ESP32)

## Overview
This project develops a **Bank Locker Security System** using **RFID and GSM technologies** with **ESP32** as the microcontroller. The system ensures only authorized users can access the locker. If an unauthorized person attempts access, an alert is sent to the registered mobile number via the **GSM module**.

## Features
- **RFID Authentication**: Uses RFID tags to verify users.
- **GSM Alert System**: Sends SMS alerts in case of unauthorized access.
- **ESP32-based Control**: Handles authentication and security operations.
- **Automatic Locker Mechanism**: The locker door opens automatically upon successful authentication.
- **WiFi Connectivity**: ESP32 allows future integration with cloud services.

## Components Used
- **Microcontroller**: ESP32
- **RFID Module**: MFRC522 (or similar)
- **RFID Tags**: Passive RFID cards for authentication
- **GSM Module**: SIM800L/SIM900
- **Servo Motor**: To open/close the locker
- **LCD Display (16x2) with I2C**: To show authentication messages
- **Buzzer**: Alarm for unauthorized access
- **Power Supply**: 5V adapter

## How It Works
1. The **RFID reader** scans the tag.
2. The **ESP32** checks if the tag ID is valid.
   - If valid: The **servo motor** opens the locker.
   - If invalid: The **GSM module** sends an alert to the user’s mobile.
3. The system logs all access attempts.
4. The locker remains secure when not in use.

## Installation & Setup
1. **Install Arduino Libraries:**
   - MFRC522 Library (for RFID module)
   - Servo Library (for motor control)
   - TinyGSM Library (for GSM communication)
2. **Upload the Code:**
   - Open the Arduino IDE or VS Code with PlatformIO.
   - Select the **ESP32 board**.
   - Upload the provided code.

## Future Enhancements
- Add **Biometric Authentication** (Fingerprint Scanner)
- Integrate **IoT Monitoring** for real-time tracking
- Implement **Face Recognition** for added security

## Conclusion
This project enhances security for bank lockers by integrating **RFID and GSM** technologies with **ESP32**. The **automated access control** and **real-time alert system** make it a highly secure solution for banks, offices, and homes.
