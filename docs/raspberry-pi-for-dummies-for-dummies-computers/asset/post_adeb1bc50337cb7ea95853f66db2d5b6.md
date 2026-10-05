
for the next bit. You can do this with a shift-to-the-right operator (>>), so you can have a little loop that generates the pattern:

```
LEDnumber = [23,4,25,10,17,8,22]
for i in range(0,len(LEDnumber)):
    io.output(LEDnumber[i],pattern & 1)
    pattern = pattern >> 1
```

And that's all there is to it — no turgid code at all. It's short, concise, and easy to write.

Finally, we have added the small, fun feature of a dice roll display. This shows several random dice patterns in quick succession, to give the impression that the dice is being rolled.

We're all ready to show you how to write the full code. This is shown in Listing 16-8.

# LISTING 16-8: LED Dice

```python
#!/usr/bin/python3
# Electronic dice. By Mike Cook
import time, random
import RPI.GPIO as io
```

```python
LEDnumber = [23,4,25,10,17,8,22]
dicePattern = [0,0x08,0x41,0x2A,0x63,0x6B,0x77]
pushButton = 7
```

```python
def main():
    print("Electronic Dice Ctrl C to quit")
    initGPIO()
    number = 1
    while True:
        displayNumber(number)
        number = generateNumber()
```

```python
def displayRoll(): # pattern to show when rolling
    for i in range(0,20):
        displayNumber(random.randint(1,6))
        time.sleep(0.1)
```

```python
def displayNumber(number):
    pattern = dicePattern[number]
    for i in range(0,len(LEDnumber)):
        io.output(LEDnumber[i],pattern & 1)
        pattern = pattern >> 1
```

```python
def generateNumber(): # wait for a push
    throw = random.randint(1,6)
    while io.input(pushButton) == 1:
        pass
    time.sleep(0.030) # debounce delay
    while io.input(pushButton) == 0:
        throw = 1
        if throw > 6: # wrap the number
            throw = 1
    return throw
```

```python
def initGPIO():
    io.setmode(io.BCM)
    io.setwarnings(False)
    for pin in range(0,len(LEDnumber)):
        io.setup(LEDnumber[pin],io.OUT) # make pin into output
    io.setup(pushButton,io.IN,pull_down=io.PUD_UP) # make pin into an input
```

- Main program logic:
```python
if __name__ == '__main__':
    main()
```

When this code runs, it loads in the libraries, defines all the functions, and finally, starts running the main function. This is where the action is coordinated, and it's a good idea to make it as short as you can. The main function prints out a message, initializes the GPIO pins and number display, and then starts an infinite loop, displaying the roll number and generating the next number when the button is pressed.

Beginners often try to cram everything into the main function, but using some well-named functions makes it much easier to see what's going on. These functions could, be called anything, but for readability, make them descriptive as you can. This benefits not only others reading your code but, more importantly, in six months' time, when you have forgotten what is going on.

![](img/df9a01bf057d58c2401b5edabd6e8829_360_0.png)

One thing that might puzzle you is that the dice pattern starts off with a 0. This was not shown in Figure 16-12, so why is it there? All, lists are numbered starting at, and the first pattern you're interested in is the pattern for a throw of 1. So, in order to align the position of the pattern information with the position in the list, you must start out with a blank entry — so that, for example, the information for the number 4 is in the fourth position on the list. The rest of the code ensures that it will never be required to be displayed.

Looking closely at Listing 16-8, the display function is a simple loop that calls the displayNumber function 20 times, giving it a random number between 1 and 6. It shows each number for one-tenth of a second. The displayNumber function should be familiar to you from earlier mentions in this chapter. The one function that may need close examination is generateNumber. It starts out generating a random number called throw, and then it waits in a loop until the button is pressed. When this is, a 30ms delay ensures that any contact bounce is finished before another while loop to see if the button has been released. Though the program is in this loop, it increments the throw variable, and when the maximum value of 6 is exceeded, the throw variable is reset to zero. The last line returns this to the calling line.

```python
number = generateNumber()
```

ensures that this return value is placed in the variable called number.

# Taking it further

We encourage you to play around with all the code you find in this book, making your own changes and extensions. One area that's fun to play with is the roll animation. Instead of showing random numbers, you can make any sort of display you like in the same way you defined the patterns for the dice display. As a start, we have written an alternate function for the display roll, as shown in Listing 16-9. You should use this to replace the function de name in Listing 16–8. You should save any changes you make using a different filename if you want to keep them.

Listing 16-9: An Alternate displayRoll Function

```python
def displayRoll(): # a pattern to show when rolling
    rollPattern = [0x01,0x03,0x07,0x0F,0x1F,0x3F,0x7F,0]
    for i in range(0,len(rollPattern)):
        pattern = rollPattern[i]
    for i in range(0,len(LEDNumber)):
        io.output(LEDNumber[i],pattern & 1)
        pattern = pattern >> 1
    time.sleep(0.2)
```

This has a new list of patterns to be used in the roll — called, rollPattern. You can change the numbers in here and the speed of the dice roll display, making longer between display changes. If you want to use binary numbers to define the pattern, you can use

```python
rollPattern = [0b1,0b11,0b111,0b1111,0b11111,0b111111,0b1111111,0]
```

Note that there's no need to specify leading os, but personally, we find binary much harder to read in a line than it's easy to lose your place amongst all those 1s. If you like this project, we encourage you to put all electronics in a box and connect it up to the Pi with a multi header and ribbon cable.

# Pedestrian Crossing

The dice project covered in the preceding section is all about displaying patterns. The Pedestrian Crossing project is about time and sequences. It simulates a U.K. pedestrian crossing — basically, a traffic-light-controlled crossing initiated by the pedestrian pressing a button. The crossing has a three-light traffic control — red, amber, green — and the pedestrian has a two-light system — Cross (or Walk), which is green, and Don't Cross (or Don't Walk), which is red. The normal state of the crossing is that the green light is on for the traffic and all the other lights are off. There's a button at crossing for the pedestrian to request a stop, and a traffic sensor is buried in the road. This sensor controls how quickly the crossing sequence will start after testrian presses the button. If no traffic has been detected recently, the sequence starts immediately, otherwise, there's a delay. This ensures ab busy road isn't stopped too many times by pedestrians or jokers, whereas a quiet road will not make pedestrians wait before they can cross. Once the Request button is pressed, the Don't light immediately comes on.

When the crossing sequence begins, the green light turns to amber and to red. Then the green crossing light comes on, and at many crossings, a sound "bleeps" to help blind people cross. After a period of time, it may be safe to continue crossing but not be safe to start a crossing, so the green light and
