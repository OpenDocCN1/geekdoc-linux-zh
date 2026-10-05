# LISTING 17-5: (continued)

```
setBombCol()
  return score
```

```
def setBombCol():
    global bombCol
    gameSound[0].play() # bomb incoming
    while t:
        r = random.randint(0,1) * 128
        g = random.randint(0,1) * 128
        b = random.randint(0,1) * 128
        if not(r==0 and g==0 and bombCol != (r,b)):
            break
        bombCol = (r,g,b)
```

```
def init():
    global fireR,fireG,fireB,beam,sky,gameSpeed,base
    random.seed()
    io.setmode(io.BCM)
    fireR = 4 ; fireG = 3 ; fireB = 2
    io.setup([fireR,fireG,fireB],io.IN,pull_up_down=io.PUD)
    beam = getBeam()
    length = 8 ; brightness = 4
    sky = Apa102bang(26,23,24,brightness)
    gameSpeed = 0.3 * the speed of game in
    pygame.mixer.quit()
    pygame.mixer.init(frequency=22050, size=-16, channels=2)
    base = [[0,0,0],[32,0,32],[0,64,0],[0,128,128]] # base colors
    soundEffects = ['ComputerBeeps2','Layer1','Pop','Screech']
    gameSound = [pygame.mixer.Sound("sounds/" + soundEffects[i] + ".wav")]
```

```
# main program logic:
if __name__ == '__main__':
    try:
        main()
    except KeyboardInterrupt:
        pass
    # turn off all LEDs
    sky.setAll((0,0,0))
    sky.show()
```

374 PART 5 Exploring Electronics with the Raspberry Pi