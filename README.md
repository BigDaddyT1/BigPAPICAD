# CircuitPython
This repository will actually serve as a aid to help you get started with your own template.  You should copy the raw form of this readme into your own, and use this template to write your own.  If you want to draw inspiration from other classmates, feel free to check [this directory of all students!](https://github.com/chssigma/Class_Accounts).
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello_CircuitPython](#Hello_CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_LCD](#CircuitPython_LCD)
* [NextAssignmentGoesHere](#NextAssignment)
---

## Hello_CircuitPython

### Description & Code
Make the led blind and display diffrent colors 
```python
import board
import neopixel

dot = neopixel.NeoPixel(board.NEOPIXEL, 1)
dot.brightness = 0.9

print("Make it red!")

while True:
    dot.fill((255, 0, 255))

```


### Evidence
https://user-images.githubusercontent.com/113116205/193277510-51cd98da-7194-460c-923c-f6c57916cff6.mov

image credit goes to [ Nick P](https://github.com/nbednar2929/CircuitPython)

### Wiring
there was no wiring requierd it was only the use of the metro express

### Reflection
The hardest thing about this part of this project was the code part and getting the color to change at diffret distances in the project. And the fact that i kept having to go in and change things constantly when it was just a simple camma made my life way harder than it had to be. Overall now i undrstand what ground is and how it works with making things work.




## CircuitPython_Servo

### Description & Code
Assignment: Get a 180° micro servo to slowly sweep back and forth between 0 and 180°.   Spicy part: Now control the servo with buttons. 

Extra Spicy:  Control the servo with just 2 raw wires (no buttons, etc), using some awesome tech called "capacitive touch!" 
```python
# SPDX-FileCopyrightText: 2018 Kattni Rembor for Adafruit Industries
#
# SPDX-License-Identifier: MIT

"""CircuitPython Essentials Servo standard servo example"""
import time
import board
import pwmio
from adafruit_motor import servo

# create a PWMOut object on Pin A2.
pwm = pwmio.PWMOut(board.D8, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

while True:
    for angle in range(0, 180, 5):  # 0 - 180 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)
    for angle in range(180, 0, -5): # 180 - 0 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)

```

### Evidence


https://user-images.githubusercontent.com/113116205/193280881-95fc62a1-6e4d-4037-910c-9e835337cc94.mp4



### Wiring
![193046598-dc07286b-8199-4008-a6be-15ca5dddda87](https://user-images.githubusercontent.com/113116205/193279246-1bdcef29-3793-4aa1-8a2b-57f2e2336061.png)

image credit goes to [ jack h](https://github.com/jhelmke45/CircuitPython)
### Reflection
this code waspretty easy because all you had to do was do the code once abd duplicate it and then change the and to reverse and go backwords the opposite way and buttons were very fun to play wwith as well.



## CircuitPython_LCD

### Description & Code
The Assignment:

Use your fancy new LCD screen for output and make two inputs (buttons, switches, capacitive touch??)  
Tripping one of the inputs will cause your Metro to count and that count will be displayed on the LCD. 
Touching the other input should toggle whether your Metro is counting up or down. 
The count direction should also be displayed on the LCD.  
```python

import board
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
import time
from digitalio import DigitalInOut, Direction, Pull

# get and i2c object
i2c = board.I2C()
btn = DigitalInOut(board.D2)
btn.direction = Direction.INPUT
btn.pull = Pull.UP
clickCount = 0

switch = DigitalInOut(board.D7)
switch.direction = Direction.INPUT
switch.pull = Pull.UP
# some LCDs are 0x3f... some are 0x27...
lcd = LCD(I2CPCF8574Interface(i2c, 0x27), num_rows=2, num_cols=16)

lcd.print("on")
print("son, i am disapoint.")
while True:
    if not switch.value:
        if not btn.value:
            lcd.clear()
            lcd.set_cursor_pos(0, 0)
            lcd.print("Click Count:")
            lcd.set_cursor_pos(0,13)
            clickCount = clickCount + 1
            lcd.print(str(clickCount))
        else:
            pass
    else:
        if not btn.value:
            lcd.clear()
            lcd.set_cursor_pos(0, 0)
            lcd.print("Click Count:")
            lcd.set_cursor_pos(0,13)
            clickCount = clickCount - 1
            lcd.print(str(clickCount))
        else:
            pass
    time.sleep(0.1) # sleep for debounce

```
Eligah helped me build my code so he gets credit 

### Evidence
![193345352-4096a970-db47-4673-9544-dc9b4a12b061](https://user-images.githubusercontent.com/113116205/193828477-2783f1ba-ee4e-47db-8fad-5688ba9ee2b4.gif)
image credit goes to [ sahana g ](https://github.com/sgupta70/CircuitPython#CircuitPython_LCD)

### Wiring
![WIN_20221004_09_16_51_Pro](https://user-images.githubusercontent.com/113116205/193829316-6ca97b57-b974-4309-9832-44bd76cc9d0a.jpg)

### Reflection
this was the hardest assignment of all because it used all of the components of our first 3 assighnments but it made it way eisier in the end. plus i learned how to brighten and dim the led screen on the back of the lcd




## NextAssignment

### Description & Code
Use the HC-SR04 to measure the distance to an object and print that out to your serial monitor or LCD in cm.
Next, you will get the neopixel to turn red when your object is less than 5cm, blue when between 5 and 20cm, and green when farther than 20cm.
For your final version of this code, you'll smoothly shift the color of the onboard neopixel, corresponding to the distance, according to the graphic below.
(Neopixel should stay red when below 5cm and green when above 35cm)
Here's how you make code look like code:

```python
Code goes here
##Troy Brown
##DistanceSensor 
##this code will madke the LED change colors depending on the distance from the sensor

import board
import time 
import neopixel
import adafruit_hcsr04
import simpleio
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6)
dot = neopixel.NeoPixel(board.NEOPIXEL, 1)
dot.brightness = 0.5

while True:

    try:
        distance = sonar.distance
        (print (distance))
    except RuntimeError:
        print("Retrying!") 
        time.sleep(0.1)

    if distance < 5: ## if distance is less than 5cm then the light will turn red
        r = 255
        g = 0 
        b = 0 
        print("<5")
    elif distance < 25 and distance > 20: ## if the distance is greater than 5cm and less than 20cm the led goes from red to blue  
        r = int(simpleio.map_range(distance, 5, 20, 255, 0))
        g = int(0)
        b = int(simpleio.map_range(distance, 5, 20, 0, 255))
        print(">5<20")
    elif distance < 20 and distance > 35: ## if the distance is greater than 20cm and less than 30cm the led goes from blue to green 
        r = int(0)
        g = int(simpleio.map_range(distance, 20, 35, 0, 255))
        b = int(simpleio.map_range(distance, 20, 35, 255, 0))
        print(">20<35")
    elif distance > 35: ## if the distance is greater than 35cm the led is green 
        r = 0 
        g = 255
        b = 0
        print(">35")
```python
Code goes here

```

### Evidence
![distance sensor](https://im4.ezgif.com/tmp/ezgif-4-5d4eb8646d.gif)

### Wiring
![WIN_20220929_09_39_10_Pro](https://user-images.githubusercontent.com/113116205/193047288-5445088d-7f41-438e-9c31-efef13f636ea.jpg)

### Reflection
\The hardest thing about this part of this project was the code part and getting the color to change at diffret distances in the project. And the fact that i kept having to go in and change things constantly when it was just a simple camma made my life way harder than it had to be. Overall now i undrstand what ground is and how it works with making things work.

