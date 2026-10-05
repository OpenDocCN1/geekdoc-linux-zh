The screenWidth and screenHeight variables must be set to the size of the farm png image.

To start enrolling, use the cursor keys to position the first occurrence of an animal. When it's in the right position, press Return and position the next move on. After all animals of the type have been positioned, press the spacebar to move to the next animal. At any time, you can see all the animals at the same time by pressing the A key. After you have defined the position of all animals, you can use the spacebar to step through them, pressing the E key to enroll each one. After you have enrolled all the cards, it's ready for your sing-song. The final program is shown in Listing 18-8.

It has been reported that this program does not exit properly using Thny and just hangs at the end. Running this IDLE 3 works perfectly.

# LISTING 18-8: Old McDonald's Farm Sing-Song

```
#!/usr/bin/python3
# Old McDonald's Farm --- a song by Mike Cook

from rc522rf import Rc522rf
import pygame, time, os

pygame.init()             # initialise graphics interface
pygame.mixer.quit()
pygame.mixer.init(frequency=22050, channels=2, buffer=512)
os.environ['SDL_WINDOW_POS'] = 'center'
pygame.display.set_caption('Old McDonald's Farm')
pygame.event.set_allowed(None)
pygame.event.set_allowed([pygame.KEYDOWN, pygame.QUIT])
screenWidth = 723 ; screenHeight = 369
screen = pygame.display.set_mode([screenWidth,screenHeight],0,32)

rfReader = Rc522rf()

farm = [] # what animals are on the farm today
play = False
cardsRead = -1
verse = 0

def main():
    global play, xPlot, yPlot, cardsRead, farm
    print("Old McDonald's Farm")
    print("Present cards then Press p = Play - n = New")
```

PART 5 Exploring Electronics with the Raspberry Pi *