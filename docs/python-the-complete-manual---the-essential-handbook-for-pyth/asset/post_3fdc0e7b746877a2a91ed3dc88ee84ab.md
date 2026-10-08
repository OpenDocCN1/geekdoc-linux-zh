
# Code your own Twitter bot Use Python with Pi

## Creating an access token

```python
def timestr_to_datetime(timestr):
    # Convert a string like Sat Nov 09 09:25:53 +0000
    # 2013 to a datetime object. Get rid of the timezone
    # and make the year the current one
    timestr = "%s %s".format(timestr[:19], datetime.now().year)
```

Go to the Settings tab and change the Access type from 'Read only' to 'Read and Write'. Click the 'Update Twitter application's settings' button. Next create an access token. Click 'Create token' button to refresh the details page, you will have a consumer name, consumer secret and access token, this is everything you need to authenticate with Twitter.

```python
# We have Sat Nov 09 09:25:53
return datetime.strptime(timestr, "%a %b %d %H:%M:%S " + year + "%Y")
```

```python
def retweet_task(self, screen_name):
    # Retweets any tweets we've not seen
    for user in tweets:
        print("Checking for new tweets from {}".format(screen_name))
        pass
```

## Authenticating with Twitter

We're going to create our bot as a class, we authenticate with Twitter in the constructor. We take the tokens from the previous step as parameters and use to create an instance of the Twitter API. We also have a variable, last_run, which is set to the current time. This is used to check if there are new tweets since last.

- Get a list of the users latest tweets
- timeline = self.api.get_user_timeline(screen_name = screen_name)

- Loop through each tweet and check if it was posted since we were last called
- for t in timeline:

```python
tweet_time = timestr_to_datetime(t['created_at'])
if tweet_time > self.last_run:
    print("Retweeting {}".format(t['id']))
    self.api.retweet(id = t['id'])
```

## Retweeting a user

The first thing we need to get is list of the user's tweets. We loop through each string, then we get its creation as a datetime object. We then check if the tweet's time is newer than the function was last called - and if so, retweet.

- __name__ == "main__":
- The consumer keys can be found on your application's Details page located at https://dev.twitter.com/apps
- consumer_key="(OAuth 4 Settings)
- consumer_secret=""

- The access tokens can be found on your application's Details page located at https://dev.twitter.com/apps
- (located under "Your access token")
- a_token=""
- a_secret="="

## The main section

The main section is straightforward. We create an instance of the bot using our tokens, and then we go into an infinite loop. In each loop, we run the retweet task with different users, the users we are monitoring (we) then update the time everything was last run, and sleep for five minutes.

- Create an instance of the bot class
twitter = bot(c_key, c_secret, a_token, a_secret)

- Retweet anything new by @LinuxUserMag every 5 minutes
while True:
    # Update the time after each retweet_task so we're only retweet was new
    twitter.retweet_task("LinuxUserMag")
    twitter.last_run = datetime.now()
    time.sleep(5 * 60)

![](img/c72194f2c3aec198936695a665a5167c_122_0.png)

# Use Python with Pi

## Control an LED using GPIO

### What you'll need...

- Breadboard: www.proto-pic.co.uk/half-size-breadboard
- 3mm LED light: www.ultraleds.co.uk/led-product-catalogue/basic-3-5-10-mm.html
- Wires: www.picomake.com/product/breadboard-wires
- 270-ohm resistor: http://goo.gl/ox4ftp5nj0091

## Control an LED using GPIO

An introduction into an external output, such as an LED, on the Pi

After you have fired up your Pi, may have installed XBMC and had a play around streaming, you might be ready for your next challenge. One to go down is to find interesting uses for one of the many desktop OSs available for the little computer, perhaps using it as a web server, an NAS or retro console. This is all great fun, but an often-overlooked feature of the Pi is its hardware pinouts. If you've never done electronics before, then the Pi is a great place to start. Or you may have used a programmable microcontroller such as Arduino in the past; the Pi, with its increased CPU and RAM over Arduino, opens up many more possibilities for projects.

The Raspberry Pi features a single PWM (pulse width modulation) output pin, along with a series of GPIO (General Purpose Input/Output) pins. These enable electronic hardware such as buzzers, lights and switches to be controlled via the Pi. For people who are used to either just 'using' a computer, or only programming software that only acts on the machine itself, controlling a real physical item such as a light can be a revelation. This tutorial will assume no prior knowledge of electronics or programming, and will take you the steps needed to control an LED using the Raspberry Pi, from setting it up to coding a simple application.

- Fig 1: All the items you will need to get an LED using PWM. The wires should have male and female ends ![](img/c72194f2c3aec198936695a665a5167c_123_0.png)

- Fig 2: Place the female end onto the Pi, noting pin number 1 is identified by the small Pi: The blue wire is ground ![](img/c72194f2c3aec198936695a665a5167c_123_1.png)

- Fig 3: Once everything is connected, plug in your USB power cable ![](img/c72194f2c3aec198936695a665a5167c_123_2.png)

- Fig 4: Switch the power on, The LED will light up. If it's dim, use a lower-rated resistor ![](img/c72194f2c3aec198936695a665a5167c_123_3.png)

> "We’ll take you through the steps needed to control an LED using the Pi, from setting it up to coding” ![](img/c72194f2c3aec198936695a665a5167c_123_4.png)

# Control an LED using GPIO Use Python with Pi

- Breadboard or prototype board provides an easy-to-use and solderless environment for creating and changing your development circuits
- Breadboard wire for any budding engineer, these male-to-male and male-to-female wires make for fast and easy circuit building
- GPIO header provides a mechanism for both input and providing output to electrical circuits, enabling reactive program
- Coloured LEDs are a great way to physically pair which part of the software is running and help you understand the program flow ![](img/c72194f2c3aec198936695a665a5167c_124_0.png)

## The Pi's pins

### Pin numbers
### GPIO pins

- 01 Before we dive into writing code, let's take a look at the layout of the pins on the Pi. If you have a Pi in case, take it out and in front of it with the USB ports on the right. The next few steps'll look at some of the issues you'll encounter when using the GPIO port.
- 03 If you take a look at the small white label, 'P1'. This is pin 1 and above it is pin 2. The right of pin 1 is pin 3, and above 3 to 4. This pattern continues until you get to pin 26 at the end. As you'll see in the next step, some pins have important uses.
- 05 The other pins on the board are GPIO (General Purpose Input/Output). These are used for other tasks that you need to do as your projects become more complex and challenging. Be aware that the power supply doesn't offer much scope for powering large items.

## Pi revision 1 or 2?

- 02 Depending on when you purchased your Pi, you may have a 'revision 1' or 'revision 2' model. The GPIO layout is slightly different for each, though they have the same functionality. Here we have a revision 1; revision 2 became available towards the end of 2012.

## Basic LED Lighting

- 04 Pin 1 is 5V3, or 3.3 volts. This is the main pin we will use in this guide to provide power to our GPIO. Pins 2 and 4 are 5V Pi is pin we will use here, which is ground. Ground pins are 9, 14, 20 and 25. You should always ensure your project is properly grounded.
- 06 Okay, let's get down to business and start making something. Firstly, get your breadboard, two wires, a 220 resistor and an LED. Note the slightly bent on one side of the LED; this is important for later. Make sure your Pi is unplugged from the mains supply.

# Use Python with Pi

## Control an LED using GPIO

### Wiring the board

Plug one wire into the number 1 pin, and the other end into the breadboard. It doesn't matter where on the breadboard you plug it, but make sure there are empty slots around it to add the LED and resistor. Now get another wire.

### Set up programming environment

Now, we need to be able to do a little more than just turn a light on - we want to be able to control it via code. Set up new Raspberry installation (a guide to this is on page 28). You don't need a GUI for this - it can be done via the terminal if you wish. It's best to check everything is up to date:

```bash
sudo apt-get dist-upgrade
```

### Open up terminal

### Add another wire

Place the end of the wire into pin number 6 (ground) and the other end to the breadboard, making sure to leave room for the resistor, depending on how large it is. Get your resistor ready.

## Download library

There is a handy GPIO Python library that makes manipulating the GPIO pins a breeze. From within the terminal, use wget to download the tar file; extract it to get all the files in a new directory.

```bash
wget https://raspberrypi.org/source/RPI.GPIO/RPI.GPIO-0.5.2a.tar.gz
tar xzf RPI.GPIO-0.5.2a.tar.gz
cd RPI.GPIO-0.5.2a
```

### Install the library

Next we need to install the library. This is a simple case using Python's install method so we need the dev version of Python. Make sure you are in the directory of the library before running command:

```bash
sudo apt-get python-dev
sudo python setup.py install
```

### Add the resistor

Grab your LED and place the 'bent' leg to the 3v3 wire in the breadboard. Place the other leg to the resistor opposite the ground. This completes the circuits and we are ready to test out our little

## Import the library in a script

### Power it up

Now get your micro-USB script and plug the main pins into the wall, or plug it into a computer or laptop (port powered on). You should see the LED light up. If not, check your connections on the breadboard or Pi, or try a different LED.

Create a new Python script. Next import the main GPIO library and we'll put it in a try-block. Save the file using Ctrl+X and choosing 'yes'.

```python
cd /
cd Desktop
sudo nano gpio.py

try:
    import RPI.GPIO as GPIO
except RuntimeError:
    print("Error importing GPIO lib")
```
