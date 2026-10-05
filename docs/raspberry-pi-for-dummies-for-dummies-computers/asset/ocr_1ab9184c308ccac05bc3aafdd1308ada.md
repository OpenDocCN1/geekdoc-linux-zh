```
def checkForEvent(): # see if we need to quit
global xPlot, yPlot, needsRedraw, done, enroll, currentA
global currentType, seeAll
event = pygame.event.poll()
if event.type == pygame.QUIT:
    terminate()
if event.type == pygame.KEYDOWN:
    if event.key == pygame.K_ESCAPE:
        terminate()
    if event.key == pygame.K_RETURN:
        currentA += 1
        if currentA >= 5:
            currentA = 0
            enroll = False
    if event.key == pygame.K_SPACE:
        done = True
        enroll = False
    if event.key == pygame.K_e:
        done = True
        enroll = False
    if event.key == pygame.K_a:
        seeAll = not seeAll
        needsRedraw = True
    if event.key == pygame.K_UP:
    yPlot[currentType] -= 1
    needsRedraw = True
if event.key == pygame.K_DOWN:
    yPlot[currentType] += 1
    needsRedraw = True
if event.key == pygame.K_RIGHT:
    xPlot[currentType] += 1
    needsRedraw = True
if event.key == pygame.K_LEFT:
    xPlot[currentType] -= 1
    needsRedraw = True
if event.key == pygame.K_s :
    print(xPlot[currentType][currentA], yPlot[currentType][currentA])
```

+   - Main program logic:
if __name__ == '__main__':
    main()