pygame.init() = initialise graphics interface

os.environ['SDL_VIDEO_WINDOW_POS'] = 'center'
pygame.display.set_caption("Dress Up")
pygame.event.set_allowed([pygame.KEYDOWN,pygame.QUIT])
pygame.key.set_repeat(500, 80)

```
screenWidth = 240
screenHeight = 550
screen = pygame.display.set_mode ([screenWidth,screenHeight]), 0, 32
needsRedraw = False
enrol = False
```

rfidReader = Rc522rfid()

```
def main():
    global xPlot,yPlot,enrol,needsRedraw
    print("Dress up doll Enrolling Cards")
    print("Space next one, e - Enroll card")
    init()
    xPlot = int(screenWidth / 4)
    yPlot = int(screenHeight / 4)
    while 1:
        checkEvent()
        for i in range(1,len(clothes)):
            done = False
        needsRedraw = True
        while not done:
            checkEvent()
            if needsRedraw:
                drawScreen(i)
        if enrol:
            enrol = False
            print("enrolling")
            enrolCard(clist[i])
```

```
def drawScreen(i):
    global needsRedraw
    pygame.draw.rect(screen, (210,210,210),(0,0,screenWidth,
    screenHeight), 0)
    screen.blit(clothes[0],(0,0))
    screen.blit(clothes[i],(xPlot,yPlot))
    pygame.display.update()
```

(continued)