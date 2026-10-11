# # 10 PRACTICAL RASPBERRY PI PROJECTS

![](bbox=[0.0, 0.09, 1.0, 0.52])

> The Arduino is better at dealing with things like servos and analog input

# # Program your Arduino with Raspberry Pi

Enjoy all the features and benefits of the Arduino microcontroller on your Raspberry Pi projects

# **What you’ll need**

+   - Arduino Uno
+   - Internet connectivity
+   - Numpy (https://scp.org/numpy)

You might be wondering why you might want to attach an Arduino to your Raspberry Pi. While there are lots of reasons, probably the most poignant is the extra six PWM-capable pins and another six analogue pins that a standard Arduino Uno offers.

You see, while the Raspberry Pi has an excellent array of pins and capabilities, it can’t do analogue and it can’t do real-time processing out of the box. With an Arduino, additions like servos, potentiometers and a whole array of analog sensors are trivially easy to trigger and control.

The best part is that you don’t even have to program in Arduino’s quasi-C++ language. All you need is a standard USB connection between your Raspberry Pi and Arduino and a small Python package called Numpy. Here’s how it’s done...

+   01. **Grab an Arduino**
+       Before you can do anything, you need an Arduino. We recommend the Uno, since it’s the default choice with the best balance of features, convenience and affordability. Since you’ll want to put it to use straight away, we recommend investing in a “starter kit” that includes LEDs, servos and all that fun stuff.
+   02. **Satisfying dependencies**
+       We’re assuming you’re using Raspbian (recommended), so open your terminal because we need to get...