# 10 Inspiring Raspberry Pi projects

![](bbox=[0.0, 0.0, 1.0, 0.44])

# Dusklights

Use your Raspberry Pi to control outdoor lights that automatically come on when it’s dark

# What you’ll need

+   - 1.2 k resistor
+   - 2.2 k resistor
+   - Light dependent resistor
+   - 1 μF capacitor
+   - Breadboard and wires

You’ve probably all seen those cheap, solar-powered lamps that you can stick into your garden to try and give it a classy bit of illumination during the night. If you’ve actually got one then you may have found out that they don’t shine very brightly and the plastic stakes can be very flimsy. So why not make your own version? What we’ll show you on this page is the beginning of an array of light-sensitive LEDs using a single LED, so that you can understand how the system works. We’ll use a special resistor called a light dependent resistor (LDR) or photosistor that changes its resistance based on the levels of light it’s receiving.

There’s no extra software you’ll need for this, so just make sure your Pi is up to date with an apt-get update and apt-get upgrade. Turn it off, unplug it from the power source and get to work wiring up the circuit as shown in the Fritzing diagram. Take special note of the placement of the components, especially the LDR and the capacitor. What you’ll need to do is measure the time it takes for the capacitor to fully charge between pin three of the GPIO ports and ground. Also, make sure the negative end of the capacitor is hooked to the ground side of the circuit.

Once that’s done, turn your Raspberry Pi back on and download the code we’ve created for this project using:

```
```
$ wget http://www.linuxuser.co.uk/wp-content/uploads/2014/08/dusklight.zip
```
```

![](bbox=[0.45, 0.59, 0.82, 0.73])

Unzip it and run it. We’ve made it so the Python shell will print out the values that the circuit returns, with a higher number meaning it’s darker and the capacitor takes longer to charge.

See how the circuit reacts to you covering the LDR with a finger or shinning a torch on it in order to get an idea of how your version will work.

To get this working for outdoor use it will require a bit of trial and error. The easiest way is to set it up when it’s getting to about the level of darkness you’d want the light to turn on and record the output from the sensor. Change the if statement so that it activates the LED over a certain number and you’ll be set. With some external power and more LEDs you can have a Raspberry Pi power an entire array of shining lights around your garden.

# Put ’em together

Linking up the AirPi with your dusklights allows you to have the ultimate outdoor Raspberry Pi device, allowing you to predict the weather and control your outdoor lighting.

With humidity and pressure sensors will be able to tell if it’s foggy or not, giving you more control over when your lights turn on.