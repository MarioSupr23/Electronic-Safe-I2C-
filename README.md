# Arduino Electronic Safe

An electronic safe system built with Arduino that uses a 4-digit PIN code for security, featuring a servo-controlled lock, I2C LCD display, and membrane keypad interface.

## Features

- **Secure PIN Code System**: 4-digit numeric PIN stored in EEPROM (persists after power loss)
- **Servo-Controlled Lock**: Physical locking mechanism using a servo motor
- **I2C LCD Display**: 16x2 LCD with custom lock/unlock icons for visual feedback
- **Membrane Keypad**: 4x4 keypad for PIN entry
- **Code Management**: 
  - Set new PIN code when safe is unlocked
  - Confirm PIN code entry to prevent typos
  - Change existing PIN code at any time
- **Persistent State**: Safe remembers its locked/unlocked state even after power cycles

## Hardware Requirements

- Arduino Uno (or compatible board)
- 16x2 I2C LCD Display (address 0x27)
- 4x4 Membrane Keypad
- Servo Motor (for lock mechanism)
- Connecting wires

## Pin Configuration

### I2C LCD (0x27)
- **SDA**: Arduino A4
- **SCL**: Arduino A5
- **VCC**: 5V
- **GND**: GND

### Membrane Keypad
- **Rows**: Digital pins 5, 4, 3, 2
- **Columns**: Analog pins A3, A2, A1, A0

### Servo Motor
- **PWM**: Digital pin 6
- **VCC**: 5V
- **GND**: GND

## Required Libraries

Install these libraries through the Arduino IDE Library Manager:

- **LiquidCrystal_I2C**: For I2C LCD control
- **Keypad**: For membrane keypad input
- **Servo**: For servo motor control (built-in)
- **Wire**: For I2C communication (built-in)
- **EEPROM**: For persistent storage (built-in)

## How to Use

### Initial Setup
1. Upload the code to your Arduino
2. On first boot, the safe will be unlocked (no PIN code set)
3. Press `#` to initiate the lock sequence
4. Enter a 4-digit PIN code
5. Confirm the PIN code by entering it again
6. The safe will lock automatically

### Unlocking the Safe
1. When locked, the LCD displays "Safe Locked!"
2. Enter your 4-digit PIN code using the keypad
3. If correct, the safe unlocks and the servo opens
4. If incorrect, "Access Denied!" is displayed

### When Unlocked
- Press `#` to lock the safe (uses existing PIN)
- Press `A` to set a new PIN code

### Keypad Layout
```
1  2  3  A
4  5  6  B
7  8  9  C
*  0  #  D
```
- **Numbers (0-9)**: Enter PIN digits
- **# key**: Lock the safe
- **A key**: Change PIN code (when unlocked)

## How It Works

The system uses EEPROM memory to store:
- Lock state (locked/unlocked)
- PIN code length
- PIN code digits

This ensures the safe remembers its state and PIN code even after power loss. The servo motor physically controls the lock mechanism, rotating to different positions for locked (20°) and unlocked (90°) states.

## Security Notes

- The PIN code is stored in plain text in EEPROM
- This is a demonstration project, not suitable for securing valuable items
- For educational and hobby purposes only
- Physical access to the Arduino allows code/EEPROM modification

## Simulation

This project can be simulated on {Wokwi](https://wokwi.com/projects/447356084248392705) without physical hardware.

## Troubleshooting

**LCD shows nothing**: Check I2C address (try 0x3F if 0x27 doesn't work)  
**Keypad not responding**: Verify pin connections match the code  
**Servo not moving**: Check power supply (servo needs adequate current)  
**Code not saving**: EEPROM might be worn out (has ~100,000 write cycle limit)
