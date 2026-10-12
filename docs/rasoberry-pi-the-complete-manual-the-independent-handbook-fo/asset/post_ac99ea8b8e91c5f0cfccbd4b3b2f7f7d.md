
## Raspberry Pi Plus Arduinos

```cpp
delay(1000);
}

void flash(int n) {
  for (int i = 0; i < n; i++) {
    digitalWrite(ledPin, HIGH);
    delay(100);
    digitalWrite(ledPin, LOW);
    delay(100);
  }
}
```

Then, you can send a count from your Python code with something like:

```python
ser.write('5')
```

This will flash the LED 5 connected to pin 13 on your Arduino five times. One missing element on the Raspberry Pi is an analogue-to-digital (ADC) converter to take a given voltage and turn it into a number that can be used in some piece of control software. This is where attaching an Arduino can be extremely helpful, as it has a 10-bit ADC converter included. The following code will read the voltage on pin 3 and send it out over the serial connection to the Raspberry Pi.

```cpp
int analogPin = 3;
int val = 0;
void setup() {
  Serial.begin(9600);
}

void loop() {
  val = analogRead(analogPin);
  Serial.println(val);
}
```

This maps the measured voltage to an integer between 0 and 1023. The minimum voltage is zero, while the maximum voltage can be set with the function `analogReference()` (Note: OCR text says "map(maxReference)" which is likely a typo for `analogReference` or similar, but sticking to text: "set with the function map(maxReference)" -> I will correct to standard Arduino terminology if possible, but instructions say "correct obvious OCR errors". "map" is likely OCR error for `analogReference` or just generic text. Let's look closer: "maximum voltage can be set with the function map(maxReference)". In Arduino, you set the reference using `analogReference()`. The text "map(maxReference)" seems like a garbled OCR of `analogReference(INTERNAL)` or similar. However, without changing meaning, I will keep it close to original but fix syntax if clearly broken. Actually, standard Arduino docs say "analogReference". I will assume "map" is an OCR error for "analogReference" or similar, but to be safe, I'll leave it as text unless it's a clear character swap. Wait, "map" and "analogReference" are very different. Let's look at the next sentence: "By default, the maximum is the power supplied to the board...". I will keep "function" and assume the OCR missed the specific function name or it was a generic placeholder. I will correct obvious typos like "5 volts" splitting.

Correction: The phrase "set with the function map(maxReference)" is likely an OCR error for "analogReference(INTERNAL)" or similar, but since I can't invent code, I will keep it readable. Actually, looking at the pattern, "map" might be a misread of "analog". Let's just clean up the text.

Going in the opposite direction, you can use the Arduino to supply an output voltage. This is done by using a PWM (pulse width modulation) output signal. The idea is to actually send out a number of pulses with some duty cycle that is on for some percentage of the time and off for the remainder of the time. For example, if you have an LED connected to one of the pins, you can light it at half brightness with the following code.

```cpp
int ledPin = 9;
void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  analogWrite(ledPin, 127);
}
```

The second parameter to the `analogWrite()` function is a value between 0 and 255, which defines the duty cycle between 0% (or fully off) to 100% (or fully on). This analog output signal stays on at the given duty cycle until a new call to the `analogWrite()` function. By having your Raspberry Pi write out values over the serial connection, it can then control the output duty cycle by sending a simple integer. This short article will spark some ideas on how you can start combining multiple computing platforms to expand the capabilities of your own projects.

There is no reason to try to find the one silver bullet platform for your project when you can pick the sub-modules that actually do their own individual jobs best and build up the complex behaviour you need from these simpler parts.

### PyFirmata can help even more

Discover ways to make interacting easier

While you can write your own code to run on the Arduino, there are several projects that can be uploaded to it to make interacting a bit easier. One of these is the Firmata project, which includes a Python module to help you talk to the Arduino. The first step will be downloading the Firmata Arduino code and uploading it to your Arduino, most easily done with a desktop computer. The code is available at github.com/firmata/arduino. There are a few different versions available, but for these examples you should upload the StandardFirmata sketch with the Arduino IDE. There are client libraries available for many different programming languages, including several for Python. The one we will look at using is pyFirmata. You can install it on your Raspberry Pi with:

```bash
sudo pip install pyfirmata
```

You can now use Firmata to act as a sort of remote control to the Arduino port, where your Python code can get almost direct access to all of the functionality available. To get started, import the pyFirmata module and create a new Arduino object connected to the relevant serial port:

```python
import pyfirmata
board = pyfirmata.Arduino('/dev/ttyUSB0')
```

You can now access digital I/O pins directly. For example, the following code would write a 1 to pin 10.

```python
board.digital[10].write(1)
```

When you want to read from a pin, you have the possibility of overflowing input buffers. To deal with this issue, you can create an iterator object and start it before doing any reads, using code like that below.

```python
it = pyfirmata.util.Iterator(board)
it.start()
```

You can now get selected pins for either input or output. The following code will get pin 4 for digital input and pin 12 for analogue PWM output.

```python
pin4 = board.get_pin('d:4:i')
pin12 = board.get_pin('a:12:p')
```

You can then read and write with these new pin objects with the related methods:

```python
val = pin4.read()
pin12.write(100)
```

When you are done, don't forget to reset any output pins back to 0 volts, and then you can close down the connection with:

```python
board.exit()
```

> There are a few different versions available, but for these examples you should upload StandardFirmata sketch with the Arduino IDE.

## Program with Scratch

An interactive guide to coding with the Pi's graphical programming language

Would you like to delve into the world of animation and game creation? Do you want to bring your creative ideas to life without learning a software-development language? With Scratch you can do all this, and much more.

Scratch 1.4 is already installed on the official 'wheezy' Raspberry Pi system image. If your Raspberry Pi doesn't already have Scratch installed, don't worry, just hop on over to the official MIT Scratch website to find the download and install instructions.

To begin, all we need to do is open the Scratch Studio. Click on Scratch's cat icon on the desktop, or find Scratch in the LXDE desktop menu.

The Scratch Studio is a complete development environment. It's divided up into a number of separate panels. Each panel has a specific role in the app-construction process and its own specific set of features and tools.

### What you'll need...

- Scratch
- Internet connection

> **Did you know...**
> You can find lots of projects on www.scratch.mit.edu and the Scratch forum has lots of useful tips and tricks.

### Scratch studio projects

01 Located at the top of the Studio are three quick-access icons and the main menu (Fig 2). The first globe-style icon gets the language for the Studio. The other two buttons provide rapid access to the project save and share features. Under the 'File' menu there's a typical set of file-management features to open, save and import Scratch projects. There is also a 'Project Notes' option where we are able to enter feature descriptions and comments.

The 'Edit' menu contains a mixed bag of animation, image and audio-editing tools. While the 'Help section provides access to the browser-hosted help pages. Rather interestingly, the 'Share' menu allows us to share our projects with the whole world. Any Scratch project can be posted onto the Scratch community website via the 'Share This Project Online' option and the 'Upload To Scratch Server' form (Fig 3).

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_51_0.png)

Let's load the 'Aquarium' example project. Select the 'Open...' option from the File menu to display the list of large buttons on the left, click on the one called 'Examples!'. Next, on the right, select the 'Animation' folder with a double click. Then select the '6 Aquarium' item. The open dialogue window contents should look like the one in Fig 4.

With the Aquarium project loaded our Scratch Studio should look similar to Fig 1. We'll begin our Studio tour with the staging area.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_51_1.png)

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_52_0.png)

**New**
Open…
Save
Save As…
**Import Project**
**Export Sprite**
Project Notes
Quit

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_52_1.png)

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_52_2.png)

### Scratch studio stage

02 The stage is where all the action takes place and is located at the upper right of the Scratch Studio.

The stage is constructed from graphical elements called sprites. Here we have plants, bubbles, fish and other creatures. You can also add and create your own assets with scratch, but we’ll come to that later.

At the top of the ‘Staging Area’ there’s a green flag and a red circle. Click on the green flag to bring the aquarium to life. Now spend a little time studying the Aquarium animation. Note the creature’s movements and rising bubbles. The red circle can stop the action.

We can set the view mode with the three buttons located just above the green flag.

The two left-hand buttons increase or decrease the size of the Staging Area panel. A smaller Staging Area means the central area of the Studio increases in relative size compared.

The right-hand button is the Presentation Mode which displays the stage in full-screen mode like Fig 5. Exit presentation mode with the curly arrow button at the top left, or press the ‘esc’ key.

### Scratch studio sprites

03 Beneath the ‘Staging Area’ is the collection of sprites for this project. The Stage sprite is separated from the rest. It’s a little different to the others and acts as the background image for the stage.

The three buttons across the top of this area offer various ways to create a new sprite. The first button opens up a blank canvas in the Paint Editor. The second button creates a new sprite based in an image file, as selected from the popup file selection dialogue window. The third will select a random image from the pre-installed image collection.

We can manage sprites directly from the stage using the four buttons to the right of the main menu. Here we click on a particular button and then a sprite on the stage.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_52_3.png)
