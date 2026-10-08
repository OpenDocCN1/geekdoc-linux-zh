# Use Python with Pi

![](bbox=[0.08, 0.11, 0.61, 0.59])

> > “ Action figures and plushy or cuddly toys both lend themselves well to this kind of maker project, especially if they accompany a film or TV show”

![](bbox=[0.64, 0.4, 0.89, 0.59])

# Full code listing

```
import os
import sys
import time
import RPi.GPIO as GPIO
import PiFm
GPIO.setmode(GPIO.BCM)
import time

GPIO.setup(15, GPIO.IN, GPIO.PUD_DOWN) #checks for a change on pin 7

###Reset Motor
GPIO.setup(9, GPIO.OUT)
GPIO.output(9, GPIO.HIGH)

###Reset LED
GPIO.setup(21, GPIO.OUT)
GPIO.output(21, GPIO.LOW)

###Controls the LED eye
def LED_Eye():
GPIO.output(3, GPIO.HIGH)
time.sleep(5)
```

```
GPIO.output(21, GPIO.LOW)

print ("Welcome to R2D2")
while True:
if GPIO.input(15) == 1:
print ("You touched R2D2!")
`"Enable LED`"`
GPIO.output(3, GPIO.LOW)
LED_Eye()
"Enable the Haptic Motor"`
GPIO.output(9, GPIO.HIGH)
``start webcam``
os.system(`service motion start`)
`"Play the Star Wars Theme"`
PiFm.play_sound("sound.wav")
``Stop the Webcam``
os.system(`service motion stop`)
```