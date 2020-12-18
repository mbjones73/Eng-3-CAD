# Eng-3-CAD
# BasicCAD

We are creating a caster.

---
## Table of Contents
* [Table of Contents](#Table-of-Contents)
* [Base](#Base)
* [Mount](#Mount)
* [Fork](#Fork)
* [Tire](#Tire)
* [Wheel](#Wheel)
* [AxleCollarBearings](#AxleCollarBearings)
* [CircuitPython](#CircuitPython)
## Base

### Description

The first assignment is to create the caster base.  The base's dimensions are 200 mm x 120 mm and 8 mm thick.  It has 6 holes 10 mm wide and 20 mm from the edge equally spaced along the edges.

### Evidence
[The Base in Onshape](https://cvilleschools.onshape.com/documents/0d70f655203ca304cb3c5b7d/w/f55603f962f6fc74f5548a68/e/41d730c570a8d75fce9f51b6)

### Image

<img src="images/Base.jpg" alt="The Base" width="200">

### Reflection

This was my first Onshape part and [following along with Dr. Shields made it super easy.](https://www.youtube.com/watch?v=93BFUD-HAG8&feature=emb_title&scrlybrkr=5670f0b4)  I learned about 
* sketching (shortcut **shift-s**)
* constructions lines (shortcut **Q**)
* dimensions (shortcut **D**)
* extruding both add and remove (shortcut key **E**)
* linear patterns (no shortcut)

Onshape is awesome.  I found it really helpful to rename all my sketches.  It is going to be a GREAT year in engineering.

---


## Mount

### Description

### Evidence

### Image

### Reflection

---


## Fork

### Description

### Evidence

### Image
<img src="blob:chrome-untrusted://media-app/c59253fe-f114-436d-9957-3b9ab5322572" alt="The Base" width="380">
### Reflection

---


## Tire

### Description

### Evidence

### Image

### Reflection

---


## Wheel

### Description

### Evidence

### Image
<img src="https://github.com/mbjones73/Eng-3-CAD/blob/main/images/wheel.png?raw=true" alt="The Base" width="389">
### Reflection

---


## AxleCollarBearings

### Description

### Evidence

### Image

### Reflection

---
## CircuitPython

### Description
Cricuit Python is a great learning experience for you. During these assignments I learned how to Code a LCD screen and make my ultrasonic sensor read the distance of a object.
### Evidence

### Image

### Code
##### Distance sensor
import time
import board
import neopixel
import adafruit_hcsr04
import simpleio
ultrasonic = adafruit_hcsr04.HCSR04(trigger_pin=board.D6, echo_pin=board.D5)
neopixel = neopixel.NeoPixel(board.NEOPIXEL, 1, brightness=.1)

r = 0
b = 0
g = 0

while True:
    try:
        dist = ultrasonic.distance
        print(dist)
        if dist <= 20:
            r = simpleio.map_range(dist, 0, 20, 255, 0)
            b = simpleio.map_range(dist, 5, 20, 0, 255)
            g = simpleio.map_range(dist, 20, 35, 0, 255)
        else:
            r = simpleio.map_range(dist, 0, 20, 255, 0)
            b = simpleio.map_range(dist, 20, 35, 255, 0)
            g = simpleio.map_range(dist, 20, 35, 0, 255)
        neopixel.fill((int(r), int(g), int(b)))
        print(dist)
    except RuntimeError:
        print("Retrying!")
    time.sleep(.1)
##### Servo
import board
import servo
import time
import pulseio
import touchio #capacitive touch

pwm = pulseio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50) #Setting the PWM

#myServo = servo.ContinuousServo(pwm) #Defines the servo as a continuous servo rather than a standard
myServo = servo.Servo(pwm)

touch_A0 = touchio.TouchIn(board.A0)  # Defines the pin which the first wire is in.
touch_A1 = touchio.TouchIn(board.A1)  # Defines which pin the second wire is in.

min_val = 0
max_val = 180
myServo.angle = 5
val = myServo.angle


def constrain(val, min_val, max_val):   # Define min_val, max_val, and val before constrain function. Then, put constrain after setting myServo.angle

    if val < min_val:
        return min_val
    if val > max_val:
        return max_val
    return val

while True:
    if touch_A0.value:
        print("Forward! ; " , myServo.angle) #Allows me to see which wire is being touched in the Serial Monitor, and what the value is..
        myServo.angle = constrain((myServo.angle +4), min_val , max_val) # Moves it to 180
        time.sleep(0.1)
    if touch_A1.value:
        print("Backward! ; " , myServo.angle)#Allows me to see which wire is being touched in the Serial Monitor, and what the value is.
        myServo.angle = constrain((myServo.angle -4), min_val , max_val) #Moves it to 0
        time.sleep(0.1)     
### Reflection
Cricuit Python is a great learning experience for you
