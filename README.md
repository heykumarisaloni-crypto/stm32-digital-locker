# STM32 Digital Locker

A password-based digital locker built on the STM32 NUCLEO-C031C6. The user types a 4-digit password on a 4x4 keypad. If it is correct, a servo motor opens the lock. After 3 wrong attempts, the system locks out for 10 seconds with a buzzer alert.

## Features
- 4-digit password entry using a 4x4 keypad (`#` = enter, `*` = clear)
- Password digits are hidden on the LCD as `*`
- Servo motor works as the lock (locked 20°, unlocked 90°)
- Green LED for unlocked, red LED for locked
- Door locks again automatically after 5 seconds
- 3 wrong attempts start a 10-second lockout with buzzer and a countdown on the LCD
- State messages are printed on the Serial Monitor (115200 baud)

## Components
| Component | Details |
|---|---|
| Microcontroller | STM32 NUCLEO-C031C6 |
| Keypad | 4x4 matrix keypad |
| Display | LCD with I2C module (address 0x27) |
| Lock | Servo motor |
| Alerts | Buzzer, green LED, red LED |
| Simulator | Wokwi |

## Pin Connections
| Component | Pin | Board Pin |
|---|---|---|
| Servo | Signal | 6 |
| Buzzer | + | 7 |
| Green LED | Anode | 8 |
| Red LED | Anode | 9 |
| Keypad | Rows R1-R4 | 5, 4, 3, 2 |
| Keypad | Columns C1-C4 | A3, A2, A1, A0 |
| LCD (I2C) | SDA, SCL | I2C pins of the board |

## Working
1. At start, the door is locked and the LCD shows "Enter password:".
2. The user types 4 digits and presses `#`.
3. Correct password: servo moves to 90°, green LED turns on, buzzer beeps, LCD shows "Access granted". After 5 seconds the door locks again.
4. Wrong password: buzzer beeps and LCD shows "Wrong password".
5. After 3 wrong attempts in a row, the system enters lockout for 10 seconds. The LCD shows "LOCKED OUT" with a countdown.
6. After lockout, the system returns to the locked state.

Default password: `1234` (can be changed in the code)

## How to Run
1. Open the Wokwi project: https://wokwi.com/projects/480610082215250945
2. Click the green Start button.
3. Click the keypad buttons to enter the password and press `#`.

## Demo Video
[Watch the demo video](simulation)

The video shows the circuit running in Wokwi: correct password, wrong password and the 10-second lockout.



## Test Results
| Test | Input | Expected | Result |
|---|---|---|---|
| Correct password | 1234 + # | Servo opens, green LED on, "Access granted" | [ ] |
| Wrong password | 1111 + # | "Wrong password", door stays locked | [ ] |
| Clear key | 12 + * | Typed digits are cleared | [ ] |
| Auto relock | After unlock | Door locks after 5 seconds | [ ] |
| Lockout | 3 wrong attempts | "LOCKED OUT" for 10 seconds with buzzer | [ ] |

## Note
This project was verified in Wokwi simulation. It has not been tested on physical hardware.

## Future Improvements
- Change password from the keypad
- Store the password in flash memory
- Add a fingerprint or RFID option

## Author
**Saloni**
4th-year ECE student, Government Engineering College, Rajkot

## License
MIT License
