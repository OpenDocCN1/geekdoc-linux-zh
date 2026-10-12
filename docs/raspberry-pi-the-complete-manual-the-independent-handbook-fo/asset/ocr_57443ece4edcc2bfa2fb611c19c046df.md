# Build a Raspberry Pi-powered car

**Projects**

# Attach the servo cables to the new controller

**02** We soldered our 16-channel DC servo controller board from www.modmypi.com as per its instructions and simply plugged channel 0 (steering) and channel 1 (motor) headers onto it. These are six cables in total: the bottom two are ground; the middle two are the power and the top two are the PWM (pulse-width modulation) signals. This is a good time to think of places to mount the extra components and the best fixing method seems to be sticky-back Velcro.

![](bbox=[0.45, 0.14, 0.93, 0.36])

# Connect the I2C bus to the Raspberry Pi

![](bbox=[0.07, 0.42, 0.35, 0.61])

**03** We’re using the Raspberry Pi’s I2C bus to control the servo interface board, which only needs four cables – they all go between the Raspberry Pi and the servo controller board as pictured. Visit http://bit.ly/ N3nq4j for a tutorial on how to set up I2C on the Raspberry Pi.

From top to bottom we need to use the 1_GND, 2_SCL, 3_SDA and 4_VCC, which map directly to the same ports on the Raspberry Pi. Essentially this is power, ground and two communication channels.

# Hook it up to the Raspberry Pi

**04** On a Rev 1 Raspberry Pi the cables look the same. Though the Rev boards have different labelling, the physical pins are in the same places. Bottom left (closest to the RPi power connector) is the 3.3V power; next to that is the SDA header, which is the data channel. Next to that in the bottom right is the SCL channel which controls the clock of the I2C devices. And finally – on the top-right port – is the Ground. We recommend printing a labelled image of the GPIO pins.

# Overview of the main components

**05** You should now have the servo board in the middle with the steering servo and speed controller on one side and the Raspberry Pi on the other. The motor is connected to the other end of the speed controller (that end should have much thicker wires); the speed controller also has two thick wires going to the main car’s battery – in this case a 7.2V NiCad. We now have two very separate power systems with the high current motors on one side and the low current electronics on the other. Let’s make sure it stays that way!

# Find everything a home

**06** We can now put it together. Use plenty of sticky-back Velcro, two strips of elastic bands to keep everything secure and tidy spaces in the car’s body to hide the wires where possible. While it is possible to stick or screw the Raspberry Pi directly to the car, we recommend to use at least the bottom half of a case for added protection and ease of access. Insert our SD card, network cable or Wi-Fi dongle and power supply. Sit back and admire your hacking skills!

![](bbox=[0.45, 0.88, 0.93, 0.97])