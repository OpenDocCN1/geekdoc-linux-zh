also use the offset to access the DMX ad-dresses. Listing 2 uses this ability to switch off the lamps again. In principle, you could use a little shell script magic to control the lights automatically, but because shell programming is not every-one's cup of tea, I'll look at how to con-trol the DMX lamps with a Python script in the next section.

# ## Program

The Python script (Listing 3) first loads all the required libraries. The block that follows creates some variables and con-stant for the offset. As seen in the previ-ous section, values on the RevPi Core can be accessed by their plain text names and by offsets.

With the help of the `fcntl` library, the script could be designed in such a way that it determines the offset in the back-ground and uses it instead of the plain text name. The script here avoids this complex procedure by using the offsets directly. Because these values always increase by 1 in the example, you do not have to determine all values by trial and error. A code example demonstrat-ing the use of the plain text names can be found on the Kunbus homepage [5].

Two classes (lines 17 and 23) establish the connection to the RevPi (`RevPi`) and control color changes of the lights (`DMX`). The `open()` command lets you open a connection to the hardware driver and store it in the `_rev_pi` variable. All access to the hardware will then be through this variable.

In the `DMX` class, the `do_<color>` meth-ods use the `update_color()` statement to ensure that the appropriate color is sent to the light. The color is calculated by the `set_step()` method and controlled by the `mode_va` variable. Because the lamps can only handle fairly coarse dimming, the values for each color are always increased or decreased by 16. Two lights and three colors allow six possible color transitions, which is why the `mode` variable is reset to 1 as soon as it reaches a value of 7 (line 72). The `time.sleep(0.85)` com-mand controls the speed of the color transitions. The `__init__` method of the `DMX` class sets the master dimmer to 100 percent, to make full use of the dim-mers for each color. The `while` 1 command tells the pro-gram to run in an infinite loop, which you can cancel with the Ctrl + C key-board combination. Inside this loop, the code changes the variable `mode` and passes it to the objects for the two lights, turning a particular color on or off. When a color reaches its new value, the `mode` variable is incremented by 1. To cycle through a color transi-tion fully, you need to call the `set_step()` method 16 times, as in the second for loop (line 75). You can launch the demo program with the command

```
python3 dmx_demo.py
```

at the RevPi Core's command line. You can find a video on YouTube showing the demo program in action [6].

# ### Conclusions

The `DMX` module for the Revolution Pi Core 3+ makes creating your own lighting show easy. A little browsing on the Internet reveals many interesting devices that can be controlled by DMX. Besides classic stage lighting, the prod-ucts also cover lighting systems for home automation. One genuine high-light among the DMX devices is a mov-ing, talking skull [7]. Have fun with your own DMX experiments.

# #### Info

+   1.  DMX lights:
+       [https://www.aliexpress.com/item/100502449259723.html?gatewayAdapt=glo2deu](https://www.aliexpress.com/item/100502449259723.html?gatewayAdapt=glo2deu)

+   2.  RevPi Core 3+:
+       [https://revolutionpi.com/revpi-core/](https://revolutionpi.com/revpi-core/)

+   3.  DMX module user manual:
+       [https://www.kunbus.com/files/media/bedienungsanleitungen/DO0262R00-MGW-UM-DMX-EN.pdf](https://www.kunbus.com/files/media/bedienungsanleitungen/DO0262R00-MGW-UM-DMX-EN.pdf)

+   4.  PuTTY: [https://www.putty.org](https://www.putty.org)

+   5.  Python example:
+       [https://revolution.kunbus.com/download/114/](https://revolution.kunbus.com/download/114/)

+   6.  Video for the program:
+       [https://youtu.be/2i2Httpwc1E](https://youtu.be/2i2Httpwc1E)

+   7.  Talking skull:
+       [https://www.hauntedhousecreations.com/full-motion-talking-skull/](https://www.hauntedhousecreations.com/full-motion-talking-skull/)

# #### Author

Martin Mohr has had a fondness for everything that flashes since his early youth, reinforced by an apprenticeship as an electronic technician. After studying computer science, he has mainly developed Java applications, but the Raspberry Pi rekindled his old love of electronics.