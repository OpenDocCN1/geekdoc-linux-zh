original speed. This makes it more interesting and difficult to play. The code for
the game is in Listing 17-6.

# LISTING 17-6: Keepy Uppy Game

```
#!/bin/env /usr/python3
# KeepyUppy by Mike Cook

import RPi.GPIO as io
import time, random
from apa102bang import Apa102bang
stripLength = 8

def main():
    global beam, gameOn,ballHeight,ballCol
    print("Keepy Uppy")
    init()
    gameOn = True
    ballDirection = -1 ; ballHeight = stripLength
    foot = 0 ; kicks = 0
    currentGameSpeed = gameSpeed
    led.setTied(0,footCol[foot]) = foot color
    led.show()
    time.sleep(gameSpeed)
    nextBallMove = time.time()+gameSpeed
    lastKickMade = not(io.input(kick))
    while gameOn:
        kick = not(io.input(kick))
        if kick and not(lastKickMade):
            if ballHeight == 0 #: kick
                ballDirection = ballDirection * -1
                #speed up if you are late pressing
                if nextBallMove - time.time() < currentGameSpeed/2:
                    currentGameSpeed = currentGameSpeed / 2
            else:
                currentGameSpeed = gameSpeed
            nextBallMove = time.time()-1.0
            foot = 1
            kicks = 1 # add to your score
        else:
            foot = 2
        if time.time()>nextBallMove:
```

376 PART 5 Exploring Electronics with the Raspberry Pi