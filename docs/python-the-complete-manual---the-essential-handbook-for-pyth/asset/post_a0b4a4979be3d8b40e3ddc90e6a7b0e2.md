
# Use Python with Pi

# Program a quadcopter

# Code and reality

In this case, there are nine PIDs in total. The horizontal plane, for both the X and Y axes, the horizontal speed PID converts the user-defined speed to require horizontal acceleration/angle of tilt; the angle PIDs then convert the rotation that the rotation speed PID converts to changes in speed for forward/back and left/right motors.

headwind will drift backwards towards the force applied to the wind. To compensate for this, it must tilt down at some angle so that some of the propellers' thrust is applied horizontally to counteract the wind. In doing so, some of the quadcopter hovering at a fixed height is now battling the wind; the overall power is reduced, the quadcopter will start drifting.

In the vertical direction, a single PID converts the rate of ascent/descent to the acceleration output applied to each plate. Finally prevention of yaw (like a spinning top) uses two PIDs – one to set the desired angle of yaw, and one to set the rotation speed. The output of these controls the yaw motors which spin in the same direction. The most critical is the pitch/roll stability. This ensures that whatever requirements enforced by other PIDs and external factors, the quadcopter is stable in achieving those targets; without this stability, the rest of the PIDs cannot work. Pitch is controlled by differences between the front and back propellers; yaw by left and right directions, and by clockwise/counterclockwise differences from the corresponding PID' outputs. The net of all three PIDs are then applied to the appropriate combination of motors' PWM channels to the individual pulse widths.

Horizontal movement is more complex. The target is to move at 1 metre per second. The initial requirement is the headwind compensation – down nose plus increased power will apply a force leading to forward acceleration. But once horizontal speed is attained, the motor needs to stop or at the same time, friction in the air will slow the movement. So there's a dynamic tilt/aft to maintain this stable forward velocity.

With stability being achieved, some level of take-off, hover and landing achieved using the vertical speed PID. Placing the quadcopter on a horizontal surface, set the target to 0 m/s and she offs into the air, while the speed PID ensures the horizontal angle of take is maintained throughout the short flight, and landing.

Both-wind suppression and control horizontal movement use some nested PIDs; the X and Y axis speed PID inputs are outputs of the forward and roll angle PID targets; the output feeds the pitch and roll angle PID to ensure stability while meeting the other targets. The sensor feedback ensures that the desired horizontal speed is approached, the horizontal speed PID errors shrink, reducing the targets for the angular PID, thus bringing the quadcopter back to horizontal again.

Up to this the PIDs are independent. But what about horizontal movement, and suppression of drifting in the wind?

Hopefully it becomes clearer why accurate angle tracking is: in the nose-down, headwind example, the vertical speed PID ensures the sensors are reduced by the cosine of the measured angle of tilt with respect to the horizontal.

This is when get more complicated. Taking the drift suppression first, a quadcopter in the

> Taking the drift suppression first, a quadcopter in a headwind will drift backwards towards the force applied by the wind

Similarly, X and Y axis speed PID inputs compare with pitch and roll angles when comparing speeds against acceleration. Don't forget to check the diagrams in the article, clear graphical representations of many of the themes we're covering.

![](img/c72194f2c3aec198936695a665a5167c_119_0.png)

# Program a quadcopter

# Use Python with Pi

![](img/c72194f2c3aec198936695a665a5167c_120_0.png)

# # Experimentation and tuning

09 While the code accurately reflects everything we've described here, there's one critical set of steps which can only be found through live testing: these are the PID gains. For each PID tuning, there is an independent Proportional, Integral and Differential gain that can only be found with estimation/experiment. The results for every quadcopter will differ. Luckily there is a relatively safe way to proceed.

Tweak the P gain accordingly. Once P is good, a touch of I gain – this will ensure return to O as well as stability. D gain is optional, but adds firmness and crisp response. Tapping a D-gain stable quad is like clicking on a table – it doesn't move.

First, find the PWM take-off speed – by sitting your quadcopter on the ground and slowly increasing the PWM value until it starts looking light-footed – for your expert, this was about 1590us pulse width (or 1000us+590us, as shown in the code).

Vertical speed can be guestimated. 1590us is taking off; desired take-off speed is 0.5m/s so a P gain of 100 is okay. No I or D gain needed. With that a real take-off, hover and landing are safe, which is good as these are to tune the directional PIDs. The quadcopter alarming themselves walls or performing maneuvers in mid-air powering themselves into the ground. Best executed outside in a open field/garden/park where the ground is soft after overnight night

Next, sorting out the stability PIDs – assuming your quadcopter is square and its balance is roughly central, the result of pitch tuning also applies to yaw. For pitch tuning, disable two diagonally opposed motors and rest – the quadcopter horizontal in power. By powering the dangling motors with PWM to get just under take-off speed (1550us pulse width in your case). The quad may rock wildly, wobble so much pretence of control, self-right when nudged, or do nothing?

There's no shortcut to this, so just accept there will be crashes and damage the engine as best you can

Assuming all the above has gone to, then you will have a quadcopter that takes off, hovers and lands in breezy conditions. Next step is to add a remote control, we'll see for that another day!

# Use Python with Pi

# Code your own Twitter bot

# What you'll need...

- Internet connectivity
- Latest version of Raspberry Pi: www.raspberrypi.org/downloads

# Code your own Twitter bot

Create your own Twitter bot that can retweet chunks of wisdom from others

![](img/c72194f2c3aec198936695a665a5167c_121_0.png)

Twitter is a useful way of sharing information with the world and it's our favourite method of giving our views quickly and conveniently. Millions of people use the microblogging platform from their computers, mobile devices and possibly have it on their televisions.

You don't need to keep pressing to retweet button, though. With a sprinkling of Python, you can have your Raspberry Pi do it for you. Here's how to create your Twitter bot...

# Installing the required software

# Full code listing

01 Log into the Raspberry system with the username PI and the password raspberry. Get the latest package lists using the command sudo apt-get update. Then install the Python Package installer using sudo apt-get install python-pip. You've done that, run sudo pip install twytwitter to install the Twitter library we will be using.

```python
# /usr/bin/env python2
```

```python
# A Twitter Bot for the Raspberry Pi that retweets everything from content
```

```python
import sys
import time
from datetime import datetime
from twytwitter import Twthon
```

```python
class bot:
    def __init__(self, key, c_key, secret, token, token_secret):
```

> Create a Twitter API instance
self.api = Twthon(key, c_key, secret, token, token_secret)

```python
# Make sure we are authenticated correctly
self.api.verify_credentials()
except:
    sys.exit("Authentication Failed")
```

```python
self.last_run = datetime.now()
```

# Registering your 'app' with Twitter

02 We need to authenticate with Twitter using OAuth. For this, you need to go to https://twitter.com/apps and sign in with your account you'd like your Pi to tweet. Click the 'Create a new application' button: LUD Pi Bot and set the website to www.limuxuser.co.uk.

```python
@staticmethod
```
