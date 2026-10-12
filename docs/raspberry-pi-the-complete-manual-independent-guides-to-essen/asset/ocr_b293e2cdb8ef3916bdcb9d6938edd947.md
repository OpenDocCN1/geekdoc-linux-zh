# Control an LED using GPIO

# Wiring the board

07 Plug one wire into the number 1 pin, and the other end into the breadboard. Note that it doesn't matter where on the breadboard you plug it in, but make sure there are enough empty slots around it to add the LED and resistor to. Now get another wire ready.

# Adding another wire

08 Place the female end of the wire into pin number 6 (ground) and the other end into the breadboard, making sure to leave room for the resistor, depending on how large it is. Next, get your resistor ready. You can use a little higher or lower than 270 ohms, but not using a resistor at all will likely blow the LED.

# Add the resistor

09 Next we need to add our resistor. Place one end next to the ground wire on the breadboard, and the other one silt below the 3V3 wire connection. This will sit next to the LED when we add it in a second. Note that there is no correct or incorrect way to add a resistor.

# Add the LED

10 Grab your LED and place the 'bent' leg next to the 3V3 wire in the breadboard. Place the other leg next to the resistor leg opposite the ground wire. This now completes the circuit and we are ready to test out our little task.

# Power it up

11 Now get your micro-USB cord and either plug the main end into the wall, or plug it into a computer or laptop port (and powered on!). You should see the LED light up. If not, then check your connections on the breadboard or Pi, or try a different LED.

# Setting up programming environment

12 Now, we need to be able to do a little bit more than just turn a light on — we want to be able to control it via code. Set up a new Raspbian installation (a guide to this is found on page 278). You don't need a GUI for this — it can be all done via the terminal if you so wish. Before starting, it's best to check everything is up-to-date with:

```
```
sudo apt-get dist-upgrade
```
```

# Open up terminal

13 Assuming we want to use the GUI, rather than SSH into the Pi, open up a new terminal window by double-clicking on the XTerm icon. We need root access to control the LEDs, so either enter `su now`, or remember to prefix any commands with sudo.

```
```
su
sudo
```
followed by password or add `sudo` to the start of each command
```

# Downloading GPIO library

14 There is a handy GPIO library that makes manipulating the GPIO pins a breeze. From within your terminal window, use wget to download the tarball file, then extract it using `tar`. This will give us all the files in a new directory:

```
```
wget https://pypi.python.org/packages/source/R/RPI.GPIO/RPI.GPIO-0.5.2a.tar.gz
tar zxf RPI.GPIO-0.5.2a
cd RPI.GPIO-0.5.2a
```
```

# Install the library

15 Now we need to install the library. This is simply a case of using Python's install method, so we need the dev version of Python. Make sure you are in the directory of the library before running this command:

```
```
sudo apt-get install python-dev
sudo python setup.py install
```
```

# Importing the library in a script

16 Create a new Python script. Next import the main GPIO library and we'll put it in a try-except block. Save the file using Ctrl-X and choosing 'yes':

```
```
cd /
cd Desktop
sudo nano gpio.py
try:
    import RPi.GPIO as GPIO
except RuntimeError:
    print("Error importing GPIO lib")
```
```