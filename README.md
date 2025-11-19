# RFID Access Control System

## Quick Start Guide

### Prerequisites
- **Proteus 8 Professional** (for simulation)
- **CodeVisionAVR** (for code compilation)
- **AVR Programmer** (for hardware deployment)

### Files Included
- `ATmega8Codevision` - Main C source code
- `project_name.hex` - Compiled firmware
- `circuit.DSN` - Proteus schematic

## Running the Project

### Option 1: Proteus Simulation
1. **Open Proteus**
   - Launch Proteus ISIS
   - Open `circuit.DSN` file

2. **Load HEX File**
   - Double-click ATmega8 microcontroller
   - In properties, browse and select `.hex` file
   - Set clock frequency to 8MHz
   - Click OK

3. **Run Simulation**
   - Click Play button (bottom left)
   - System shows "Pass Your Card" message
   - Use virtual terminal to simulate card data

### Option 2: Hardware Implementation
1. **Program ATmega8**
   - Connect AVR programmer (USBasp/ArduinoISP)
   - Use AVRDUDE or CodeVisionAVR to flash `.hex` file
   - Command: `avrdude -c usbasp -p m8 -U flash:w:project_name.hex:i`

2. **Build Circuit**
   - Follow schematic in `circuit.DSN`
   - Connect RFID reader to USART pins
   - Connect LCD, LEDs, buzzer, relay as per pinout
   - Provide 12V power supply

3. **Test System**
   - Power on circuit
   - System displays startup animation
   - Swipe RFID cards for testing

## Card Programming Procedure

### Register New Card
1. Press **INT0 Button** repeatedly to select slot (1-10)
2. Press **INT1 Button** to enter programming mode
3. Swipe RFID card near antenna
4. System confirms "Saved in slot X"

### Delete Existing Card
1. Press **INT0 Button** to select slot 11-20 (delete mode)
2. Press **INT1 Button** to enter delete mode
3. Swipe card to remove from system
4. System confirms "Cleared slot X"

## System Architecture
- **Microcontroller**: ATmega8 @ 8MHz
- **RFID**: 125KHz, USART @ 9600 baud
- **Storage**: EEPROM for 10 cards (14 bytes each)
- **Display**: 16x2 LCD
- **Control**: Relay door mechanism
- **Indicators**: Green/Red LED + Buzzer

## Normal Operation
1. System displays "Pass Your Card" with animations
2. User swipes RFID card
3. If authorized: Green LED, relay activates, door opens
4. If unauthorized: Red LED, buzzer, "Do Not Match" message

## Troubleshooting
- **No response**: Check power supply and clock settings
- **Card not reading**: Verify antenna connections and resonance capacitor
- **Programming fails**: Check programmer connections and fuses
- **LCD not working**: Contrast potentiometer and data bus connections

## Pin Configuration Summary
- **LCD**: PORT C
- **LEDs/Buzzer**: PORTC.4, PORTC.5
- **Relay**: PORTC.2
- **Buttons**: PORTD (INT0, INT1)
- **RFID**: USART (RX/TX)

## Technical Specifications
- **Voltage**: 12V DC input
- **RFID Frequency**: 125 KHz
- **Communication**: USART 9600 baud
- **Card Data**: 14-byte identification
- **Storage Capacity**: 10 cards
