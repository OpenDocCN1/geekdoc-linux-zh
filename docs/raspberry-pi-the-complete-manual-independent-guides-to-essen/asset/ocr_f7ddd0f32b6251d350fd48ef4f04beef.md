# ## Code Arduino with Python

Enjoy all the features and benefits of the Arduino microcontroller in your Raspberry Pi projects

# ### What you'll need...

+   *   Arduino Uno
+   *   Internet connectivity
+   *   Nanspy [https://github.com/happy](https://github.com/happy)

# ### Did you know...

> > The Arduino is better than the Raspberry Pi at controlling lights and motors, but the Pi is more powerful elsewhere.

# ### Final preparations

#### 03 Since the communication between the Arduino and Raspberry Pi will happen over the USB serial connector, we need to get the Python serial library. Open a terminal and type:

```
```
 easy_install pyserial
```
```

We also need to install the Arduino software so the Pi knows how to deal with the device when it's plugged in. Next, in the terminal, type:

```
```
sudo apt-get update
sudo apt-get install arduino
```
```

# ### Install Nanspy

#### 04 There are only two steps remaining in the configuration. First, we need to get the Nanspy package downloaded and installed on the Pi. Our preferred way is to clone it with Git. Navigate to your home

![](bbox=[0.05, 0.55, 0.4, 0.7])

# ### Grab an Arduino

#### 01 Before you can do anything, you need an Arduino. We recommend the Uno, since it's the default choice with the best balance of features, convenience and affordability. Since you'll want to put it to use straight away, we recommend investing in a 'starter kit' that includes LEDs, servos and all that fun stuff. Just Google 'Arduino Starter Kit' and you'll be inundated with results.

# ### Satisfying dependencies

#### 02 We're assuming you're using Raspbian, so open your terminal. At the terminal, type:

```
```
 wget https://bitbucket.org/psya/setuprepoA2l/raw/py/
 bootstrapping/e2/setup.py
```
```

Then type:

```
```
 python ez_setup.py user
```
```

Once this is complete, you'll be able to use the easy\_install command to install pyserial...

You might be wondering why we want to attach an Arduino to our Raspberry Pi. While there are lots of reasons, probably the most poignant is the extra six PWM-capable pins and another six analogue pins that a standard Arduino Uno offers. While the Raspberry Pi has an excellent array of pins and capabilities, it can't do analogue and we can't do real-time processing out of the box. With an Arduino, additions like servos, potentiometers and a whole array of analog sensors are trivially easy to trigger and control. With this guide you can control it from your Raspberry Pi and you don't even have to program in C++!