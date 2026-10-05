# LISTING 18-8: (continued)

```
fixed[i].play()
waitFinish()
if i == 3 or i==5 or i==9:
 noises[farm[index]].play()
 numDisplayed +=1
drawScreen(numDisplayed,level,index)
waitFinish()
 noises[farm[index]].play()
waitFinish()
if i == 7 or i == 8:
 noises[farm[index]].play()
 numDisplayed +=1
drawScreen(numDisplayed,level,index)
waitFinish()
index = -1
level = -1
numDisplayed = 0
if verse < len(farm)-1: # more verses
 fixed[0].play()
waitFinish()
time.sleep(0.2)
fixed[11].play() # well
drawScreen(-1,0,0) # clear the frame
else:
 fixed[10].play()
waitFinish()
time.sleep(0.3)
```

```
def waitFinish():
    while pygame.mixer.get_busy():
        checkEvent()
```

```
def terminate(): # close down the program
    print("Closing down wait")
    pygame.mixer.quit()
    pygame.quit() # close pygame
    os._exit(1)
```

```
def checkForEvent(): = : see if we need to quit
    global play, farm, cardsRead
    event = pygame.event.poll()
    if event.type == pygame.QUIT :
        terminate()
```

422 PART 5 Exploring Electronics with the Raspberry Pi