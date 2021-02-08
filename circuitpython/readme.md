# My circuitpython assignments
## Hello CircuitPython
### Description
I got the Metro M0 Express board working, and coded a simple fade with the built in LED
### Code
import board
import neopixel
import time
x = 0
change = 1

dot = neopixel.NeoPixel(board.NEOPIXEL, 1)

while True:
    if x > 254:
        up = -1
    if x < 1:
        up = 1
    x += up
    dot.fill((0, -x+255, x))
    time.sleep(.1)
    print("Green Level: ", -x+255)
    print("Blue Level:", x)
 
 ### Distance sensor
 
 ### Description
I used a distance sensor to change the color of the neopixel LED
 ### Evidence

 ### Image
<img src="https://github.com/adent11/CircuitPython/blob/master/Media/DistanceSensorLEDMapping.png" alt="The Base" width="380">
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
