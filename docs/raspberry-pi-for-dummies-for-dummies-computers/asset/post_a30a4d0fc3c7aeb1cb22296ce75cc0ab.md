
# LISTING 18-5: (continued)

```python
needsRedraw = False

def init():
    global clothes,cList
    path = os.path.realpath(__file__)
    path = os.path.dirname(path) + "/doll/"
    # get a list of files
    cList = [fn for fn in next(os.walk(path))[2]]
    list.sort(cList) # put in alphabetical order
    print("files found")
    for i in range(0,len(cList)):
        clothes = pygame.image.load("doll/"+cList[i]).convert_alpha()

def enrolCard(name):
    print("Enrolling", name, "place a card on the reader")
    data1 = []; data2 = []
    for i in range(0,16): # fill with sectors worth of zeros
        data1.append(0); data2.append(0)
    for i in range(0,len(name)):
        data1[i] = ord(name[i])
    # save position of this item
    data2[0] = xPlot >> 8
    data2[1] = xPlot & 0xFF
    data2[2] = yPlot >> 8
    data2[3] = yPlot & 0xFF

    # This is the (default) key for authentication
    key = [0xFF, 0xFF, 0xFF, 0xFF, 0xFF]
    rfReader.RC522_WriteSector(key,8,data1)
    rfReader.RC522_WriteSector(key,9,data2)
    print("finished encoding")

def terminate(): # close down the program
    print("Closing down")
    pygame.quit()
    os._exit(1)

def checkForEvent(): # see if we need to write done, enrol
    global xPlot,yPlot,needsRedraw,enrol
    event = pygame.event.poll()
    if event.type == pygame.QUIT:
        terminate()
    if event.type == pygame.KEYDOWN :
        if event.key == pygame.K_ESCAPE :
            terminate()
        if event.key == pygame.K_SPACE :
            done = True
            enroll = False
        if event.key == pygame.K_e :
            done = True
            enrol = True
        if event.key == pygame.K_UP :
            yPlot -= 1
            needsRedraw = True
        if event.key == pygame.K_DOWN :
            yPlot += 1
            needsRedraw = True
        if event.key == pygame.K_RIGHT :
            xPlot += 1
            needsRedraw = True
        if event.key == pygame.K_LEFT :
            xPlot -= 1
            needsRedraw = True
```

- Main program logic:
```python
if __name__ == '__main__':
    main()
```

You need to make only one change: Set the dimensions of the window to the dimensions of your doll image. Double-click on the doll to bring up a window that specifies the image size in pixels in the top bar. Make sure those numbers are used to set the values of the screenWidth and screenHeight variables in the code.

When you run the code, you will see your doll and the first piece of clothing. The cursor keys to maneuver this piece into the exact spot where you want it to appear on the doll. Place a card on the reader and press the E key, to store the filename in Section 8 and the position in Section 9. Remove the card and press the spacebar for the next piece of clothing.

> Keep pressing the spacebar to cycle through the clothes until you find the one you want to enroll. This way, if you find a piece that isn't quite right you can go and enroll that piece again. Also, if you add the files to the doll folder, you can just enroll the new piece on a new card.

![](img/df9a01bf057d58c2401b5edabd6e8829_420_0.png)

Finally, print out each piece of clothing onto paper and use spray glue to mount onto each card. Cover the card with a transparent plastic film and trim off any surplus with a sharp blade, holding the card face down on a cutting mat. Some of our cards are shown in Figure 18–4.

![](img/df9a01bf057d58c2401b5edabd6e8829_421_0.png)

FIGURE 18-4:
Doll clothes RFID cards.

Reproduced by permission of Imani Osman

# Runway time

Now it's time to actually dress up the doll. The program for doing this is in Listing 18–6.

LISTING 18-6: Dress Up Doll
```python
#!/usr/bin/python3
# Dress Up by Mike Cook

from rc522rfid import rc522rfid
import pygame
import os

pygame.init() # initialise graphics interface

os.environ['SDL_VIDEO_WINDOW_POS'] = 'center'

pygame.display.set_caption("Dress Up")
pygame.event.set_allowed([pygame.KEYDOWN,pygame.QUIT])
pygame.key.set_repeat(500, 80)

screenWidth = 240
screenHeight = 550
screen = pygame.display.set_mode([screenWidth, screenHeight], 0)
xPlot = [0]
yPlot = [0]
garment = []
 what to display
rfidReader = Rc522rfid()

def main():
    global xPlot,yPlot,done,enroll
    print("Dress up doll")
    print("Space bar to start over")
    init()
    drawScreen()
    while 1:
        checkForEvent()
        readCard()
        if needsRedraw:
            drawScreen()
        rfidReader.WaitForCard()

def readCard():
    global needsRedraw
    status = -1
    while checkEvent() == -1:
        status = rfidReader.ReadCard()
        # This is the (default) key for authentication
        key = [0xFF, 0xFF, 0xFF, 0xFF, 0xFF]
        block1 = rfidReader.RC522_GetSector(key,8)
        block2 = rfidReader.RC522_GetSector(key,9)
        if block1 != -1 and block2 != -1:
            x = block2[0] << 8 | block2[1]
            y = block2[2] << 8 | block2[3]
            lookAtNew(block1,x,y)
            needsRedraw = True
    return -1
```

# LISTING 18-6: (continued)

```python
def lookAtNew(s1,x,y): # look at the new element
    global garment,xPlot,yPlot
    name = ""
    i = 0
    notDone = True
    while notDone and i < 16:
        c = s1[i]
        i+=1
        if c != "":
            name = chr(c)
        else:
            notDone = False
            # look up name in list of files
            for i in range(1,len(cList)):
                if cList[i] == name: # find the name on the card
                    if i in garment: # remove already in the list
                        place = garment.index(i)
                        del garment[place]
                        del xPlot[place]
                        del yPlot[place]
                    else: # otherwise add it
                        garment.append(i)
                        xPlot.append(x)
                        yPlot.append(y)
    return

def drawScreen():
    global needsRedraw
    pygame.fill((210,210,210), screen)
    for g in range(0,len(garment)):
        screen.blit(clothes[garment[g]], (xPlot[g],yPlot[g]))
    pygame.display.update()
    needsRedraw = False

def init():
    global clothes,cList
    path = os.path.realpath(__file__) # path of this program
    path = os.path.dirname(path) + "/doll/" # path of images
    # get a list of files
    cList = [fn for fn in next(os.walk(path))[2]]
    list.sort(cList) # put in alphabetical order
    for i in range(0,len(cList)):
        clothes = pygame.image.load("doll/"+cList[i] ).convert_alpha()

def terminate(): # close down the program
    print("Closing down")
    pygame.quit() # close pygame
    os._exit(0)

def checkForEvent(): # see if we need to quit
    global xPlot,yPlot,garment
    event = pygame.event.poll()
    if event.type == pygame.QUIT:
        terminate()
    if event.type == pygame.KEYDOWN:
        if event.key == pygame.K_ESCAPE:
            terminate()
        if event.key == pygame.K_SPACE :
            xPlot = [0]; yPlot = [0]
            garment = [] # clear lists
            drawScreen()
```

- Main program logic:
```python
if __name__ == '__main__':
    main()
```

Make that the values of the screenWidth and screenHeight are set to the same values as in the enroll code. Presenting an enrolled card adds that piece of clothing on the doll; presenting it removes it. Pressing the spacebar starts again from scratch. Note that the clothes are drawn in the order that the clothes are presented. This might look odd if one item is partially covered another. The doll should be dressed as in life, with garments that are worn under other items first. It's fun to build up your own collection of dolls and accessories. Figure 18-5 shows some of the dressed-up dolls we created.

![](img/df9a01bf057d58c2401b5edabd6e8829_425_0.png)

![](img/df9a01bf057d58c2401b5edabd6e8829_425_1.png)

![](img/df9a01bf057d58c2401b5edabd6e8829_425_2.png)

![](img/df9a01bf057d58c2401b5edabd6e8829_425_3.png)
