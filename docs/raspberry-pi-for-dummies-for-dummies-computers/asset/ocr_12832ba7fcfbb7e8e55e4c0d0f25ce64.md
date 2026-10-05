```
from Apa02bang import Apa02bang

dataPin = 23 ; clockPin = 24
lenX = 8 ; lenY = 8
length = lenX * lenY ; brightness = 1
half = int(length / 2)
patternDuration = 0.8
led = Apa02bang(length, dataPin, clockPin, brightness)
```

```
def main():
    print("APA02 8 by 8 matrix brooch - Cnt to stop")
    nextChange = time.time() + patternDuration
    pattern = 1
    while True:
        if pattern == 1:
            pattern1()
        if pattern == 2:
            pattern2()
        if pattern == 3:
            pattern3()
        if time.time() > nextChange:
            nextChange = time.time() + patternDuration
            pattern += 1
        if pattern > 3:
            pattern = 1
```

```
def pattern1():
    for side in range(0,lenX):
        for i in range(0,lenX):
            square(i,side,randCol())
            leds.show()
            time.sleep(0.1)
        time.sleep(0.6)
        leds.setAll((0,0,0))
        leds.setAll((0,0,0))
        time.sleep(0.6)
```

```
def pattern2():
    start = 0
    for side in range(start,start,lenX-1,0,-2):
        square(start,side,randCol())
        leds.show()
```

(continued)

CHAPTER 17 Lots of Multicolored LEDs 385