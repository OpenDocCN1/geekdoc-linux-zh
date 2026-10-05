```
rawNames = []
for i in range(len(animalNames)): # remove file extension
rawNames.append(animalNames[i][:len(animalNames[i])-4])
# load in the sounds
animals = pygame.mixer.Sound("farmSounds/") +rawNames \ 
[sound]+".ogg"
    for sound in range(0,len(rawNames))
noises = pygame.mixer.Sound("farmSounds/") +rawNames \ 
[sound]+"Sound.ogg"
    for sound in range(0,len(rawNames))
files = ["start", "and", "ee_ee_oh", "here", "anda", \
"there", "therea", "everywhere", "end", "well" ]
fixed = [pygame.mixer.Sound("farmSounds/fixed") +files \ 
[sound]+".ogg"]
    for sound in range(0,len(files))
# load in the pictures
animalPictures = [pygame.image.load("farmPictures/") \ 
+animalNames[i].convert_alpha()]
for i in range(0,len(animalNames)):
farmBuilding = pygame.image.load("farmPictures/fixed/") \ 
arm.png\).convert_alpha()
farmFence = pygame.image.load("farmPictures/fixed/") \ 
fence.png\).convert_alpha()
xPlot = [ ]; yPlot = [ ]
```

```
def singSong():
    global verse
    verse = 0
    while verse < len(farm): # repeat for each verse
        for i in range(0,3): # start part
            fixed[i].play()
            waitFinish()
        if i == 1:
            animals[farm[verse]].play()
            waitFinish()
        if i == 2:
            farmYard(verse, verse)
            verse += 1
```

```
def farmYard(index,verse): # sing verse
    numDisplayed = 0
    level = 0
    while index != -1:
        for i in range(3,10)
```

(continued)