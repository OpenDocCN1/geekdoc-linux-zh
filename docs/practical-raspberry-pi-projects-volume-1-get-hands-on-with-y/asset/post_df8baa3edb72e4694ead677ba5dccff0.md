
## Why Python?

Python is extremely useful for beginners due to its easy-to-understand syntax, fairly prose-like format and the flexibility and ease of acquiring existing software libraries to help your projects. It is also the official programming language of the Raspberry Pi and is therefore very well supported within the community. That is not to say that Hover will not work with other programming languages, simply that the creators of Hover have not yet released any code libraries in other languages.

![](img/a1548a579bd09ff29b2b92de3f565e63_135_0.png)

![](img/a1548a579bd09ff29b2b92de3f565e63_135_1.png)

**Above** This MGC3130 chip works as the 3D tracking and gesture controller

## 05 Using a Rev 1 Pi?

In the code, we have passed an option "-y 1" which tells the operating system which I2C bus to look at (there are two on the BCM2835 processor on the Pi). The first revision Raspberry Pi (the one that initially launched in February 2012 with 256MB of RAM) made use of I2C bus 0, whereas all other versions of the Raspberry Pi since have used I2C bus 1. So the above code would change to:

```
sudo i2cdetect -y 0
```

And you should expect the same output (42) as in step 7. Additionally you will need to edit line 27 of the Hover_library.py file, changing `bus = smbus.SMBus(1)` to `bus = smbus.SMBus(0)`. A patch that automatically detects the Raspberry Pi version and makes this change for you has been submitted, but not yet accepted into the master branch so this may not be necessary in future versions.

## 06 Download the sample code

Now you have everything hooked up correctly and your Raspberry Pi is fully up to date, it is time to get the Hover Python library, which makes using the board from Python scripts extremely easy. You can get this using the following command:

```
git clone https://github.com/jonco91/hover_raspberrypi.git
```

This should download a folder called `hover_raspberrypi` to your `/home/pi` directory containing all of the files needed for this article. Alternatively you can download the zip file from [https://github.com/jonco91/hover_raspberrypi/archive/master.zip](https://github.com/jonco91/hover_raspberrypi/archive/master.zip).

## 07 Run the example file

The current Hover library is simply a Python file with all of the necessary functions included within it, rather than an installable package (however, this may change in the future). In order to use the functions contained within the Hover_library.py script discussed above, it is therefore necessary to make sure that the Hover_library.py script is located in the same folder as any script you have written that makes use of any of the Hover functions. In a terminal session, navigate to the folder containing the Hover_example.py file and run it using:

```
sudo python Hover_example.py
```

The Hover board will initialise and you will then see a message "Hover is ready", meaning you are good to go.

# ADD GESTURE CONTROL TO YOUR RASPBERRY PI

## 08 Investigate the output

Once you have completed step 7, if you touch the Hover board or make gestures above it you will begin to see output in the terminal which is a bunch of 0s and 1s and then a description of what it has seen – right swipe, north tap, etc. The way the Hover works is that it can sense any one of nine different actions and these are sent to the Raspberry Pi over I2C as an 8-bit binary value. The first three bits describe whether it was a touch or gesture event and the remaining five bits describe the specific type or direction of the event. The exact breakdown can be seen in the code listing to the right.

## 09 Enable 3.5mm audio

Grab your speakers and plug them in to the 3.5mm jack plug on the Raspberry Pi. You will then need to route audio to the 3.5mm jack using the following command (you can skip this step if you are using an HDMI display, which has in-built audio):

```
sudo amixer cset numid=3 1
```

![](img/a1548a579bd09ff29b2b92de3f565e63_136_0.png)

## Full code listing

```python
import time
from Hover_library import Hover

hover = Hover(address=0x42, ts=23, reset=24)

try:
    while True:
        # Check if hover is ready to send gesture
        # or touch events
        if (hover.getStatus() == 0):
            # Read i2c data and print the type of
            # gesture or touch event
            message = hover.getEvent()
            print(type(message))

            if (message == "01000010"): # code for west touch goes here
                pass
            elif (message == "01010000"): # code for centre touch goes here
                pass
            elif (message == "01001000"): # code for east touch goes here
                pass
            elif (message == "01000011"): # code for south touch goes here
                pass
            elif (message == "01000010"): # code for north touch goes here
                pass
            elif (message == "00100010"): # code for swipe right goes here
                pass
            elif (message == "00100010"): # code for swipe left goes here
                pass
            elif (message == "00100100"): # code for swipe down goes here
                pass
            elif (message == "00100011"): # code for swipe up goes here
                pass

            # Release the t pin until Hover is
            # ready to send the next event
            hover.setRelease()
            time.sleep(0.0008) # sleep for 1ms

except KeyboardInterrupt:
    print("Exiting...")
    hover.end()

except Exception:
    print("Something has gone wrong...")
    hover.end()
```

## 10 Make a drum machine

In the hover_raspberrypi folder is another folder called examples that contains code and sounds to turn Hover into a drum machine! Navigate to the hover_raspberrypi directory and then copy the Hover_library.py file into the examples folder by using:

```
cp Hover_library.py examples
```

You can then move into the examples folder and run the Hover_drum.py file using:

```
cd examples
sudo python Hover_drum.py
```

Make some gestures and taps on and around Hover and you will have your own basic drum machine!

## 11 Create your own responses

The great thing about having a Python library available is that it is easy to integrate this device into any of your existing or future projects. The code shown is all you need to get started with Hover. You will see that on line 15 and onwards there are comments saying “code for ... goes here”. Essentially all you need to do is insert the actions you want to occur on the particular event mentioned in the comment and you will be up and running... it really is that easy!

## 12 Other project ideas

Most of you are probably now wracking your brains for projects you could use Hover in, so let’s face it – pretty much any project that requires physical interaction would be made better with touch and gesture control. If you think it is cool but lacking inspiration, we recommend looking at the projects section of the Hover website at http://www.hoverlabs.co/projects, where there are projects by the creators and community alike. If you make something cool, be sure to send us the pictures!

## Where are the hoverboards?

Did you come here looking for information on how to build your space age transportation device? We can’t help you with that, but we don’t want to leave you disappointed!

Hoverboards were first popularised as a fictional personal transportation method in the 1989 film *Back To The Future Part II* and took the appearance of a levitating skateboard with no wheels. 25 years later it seems we might be getting close to turning this dream into a reality. Hendo Hoverboards have created a $10,000 hoverboard which uses a principle similar to that of maglev trains to generate lift (kck.st/ZMdr9AA), and more recently RyanCrawen has created a much cheaper alternative using four leaf blowers and some other cheap parts (mkr.vw/9B9dA.com/about).

![](img/a1548a579bd09ff29b2b92de3f565e63_137_0.png)

> **Chords** You can play chords by manipulating three thumbsticks at once – how you move them affects the sound of the notes in the chord

> **Thumbsticks** Push forward/backward to switch between triangles and reverse sawtooth waves or push left/right to affect the oscillators

![](img/a1548a579bd09ff29b2b92de3f565e63_137_1.png)

> **Isomorphic** All the chords and scales you can play have the same geometric shape, no matter what key you’re playing them in

> **Hexagonal grid** The Jotype one uses a hexagonal layout for the notes like electronic musical instruments such as Rainboard or app-like Mu:zix

**Above (Inset)** Getting to know the musical distances between adjacent thumbsticks is the key to learning to play the Jotype one

**Right** There’s a marathon lab session behind this six-note demo unit that Sharplee and Glazman presented at the OIS Senior Design Fair

![](img/a1548a579bd09ff29b2b92de3f565e63_137_2.png)

## Components list

- Raspberry Pi Model B
- Cypress PSoC 4
- Arduino Micro
- 57 Xbox 360 thumbsticks
- 57 NeoPixel Diffused 8mm
- Through-Hole LEDs (Adafruit)
- 8 16-channel analogue multiplexers
- 5 16mm illuminated Pushbuttons (Adafruit)
- 200mm SoftPot Membrane Potentiometer
