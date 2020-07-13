# Flipclock
Arduino-powered clock using split-flap mechanical displays.

https://www.youtube.com/watch?v=v2_D-W6b9TM

![Flip clock image](images/1.jpg)
![Flip clock image](images/3.jpg)
## Features
- Automatic time setting on sketch upload
- RTC module keeps track of time even when unpowered
- US DST support - clock automatically skips forward/back 1 hour as needed
- Runs off of Arduino's USB power - no separate power input needed
- Automatic calibration once per rotation using mechanical endstops
- Steppers turned off when not moving for power savings
- Endstop failure detection - shuts down if homing takes over 2 full rotations

# Non-printed parts
|  Part | Quantity   | Notes  |
|---|---|---|
|  M3x10mm button head bolt | 19  |   |
|  M3 lock nut | 19 |   |
| 28byj-48 stepper motor | 3 |   |
| ULN2003 stepper driver | 3 |   |
| Pro Micro or similar small Arduino (5V) | 1 |
| DS3231 RTC module | 1 |
| PCB endstop | 3 | Will need to cut the switches off and solder leads to the C and NO pins |
| Zip ties | Varies | |
| Wires (22AWG or similar) | Varies | |
| Double-sided tape | Varies | |

# Printing
The parts are designed to print without supports. Recommended layer height is 0.2mm or lower.

The numbers on the flaps are inset by 0.2mm, so these parts are recommended to be printed at a 0.2mm height. If you don't want to color in the numbers manually, you can pause the print after the first layer and swap to a different filament color. Make sure to pause before the last layer to swap the original color back in.

# Assembly
## Displays
1. Use 2 M3x10mm bolts and lock nuts to attach a motor to the motor mount.
1. Install the rotor end cap onto the motor shaft, with the protruding nub facing the motor body.
1. Press the rotor onto the motor shaft. The rotor should interlock with the rotor end cap.
1. Snap the flaps onto the rotor. If having trouble attaching the flaps, it may help to slightly back the rotor off the shaft for a bit more clearance. The top halves of the display should be the side that was facedown on the print bed, and the opposite should be true for the bottom halves. If installed correctly, the numbers should count up when the display turns. (Note: the tens display (the one in the middle) has 2 identical sets of numbers. For 1 rotation of the display, it should count from 0 to 5 twice.)
1. If you haven't already, cut the switch off of each endstop circuit board and solder leads to the C and NO pins.
1. Slip the endstop switch through the rectangular cutout above the motor. The switch can be moved forward and backward to control how close it is to the rotor end cap. Adjust the switch position so that the nub on the end cap triggers the switch. Lock the switch in position with another M3x10mm bolt and lock nut.

## Frame
1. Attach each display to the faceplate using 2 bolts and lock nuts each.
1. Attach the stand pieces to the sides of the faceplate and electronics tray. Use bolts and lock nuts to secure everything in place (4 total).

## Electronics
1. To make cable management easier, the faceplate and stand pieces have zip tie attachment points. The hours display cables should be routed by the left stand, and the other displays should be routed towards the right stand. Due to the length of the stepper motor cables, it is cleaner to wire the stepper drivers in the opposite order of the displays, i.e. the rightmost driver is attached to the leftmost display.
1. The stepper drivers attach with zip ties. At first, only attach the zip ties near the front of the clock, as the rear zip ties will also be used for cable management.
1. Wire the RTC module to the I2C pins on the Arduino. On the Pro Micro, connect SDA to pin 2 and SCL to pin 3. Ground and VCC on the RTC should be wired to the corresponding pins on the Arduino.
1. Wire the 5V and ground pins of the stepper driver to the VCC and ground pins, respectively, on the Arduino.
1. Wire the steppers to the Arduino. On the Pro Micro, the recommended pins are 4, 5, 6, 7 for the hours display; 8, 9, 10, 16 for the tens display; and 14, 15, A0, A1 for the ones display.
1. Wire one side of each endstop to ground on the Arduino, and the other side to an IO pin. On the Pro Micro, it's recommended to connect the hour endstop to A3, the tens endstop to A2, and the ones endstop to TX0 (digital 1). If you want to keep the TX/RX pins free for something else, the endstops for the tens and ones displays can be wired together and share the A2 pin.
1. After everything is wired up, use double sided tape to stick the Arduino and RTC module to the electronics tray.
1. Use zip ties through the rear stepper driver holes to secure the cables.

# Calibration and operation
The driver code is provided in the 'flipclock' folder. The configurable parameters, as well as their descriptions, are at the top of the file. Edit these as needed. When uploading the sketch, be ready to quickly unplug the clock if any of the displays are turning backwards, as this could damage the endstop switches. If a display turns backwards, reverse the order of the pins for that display in the sketch file.
