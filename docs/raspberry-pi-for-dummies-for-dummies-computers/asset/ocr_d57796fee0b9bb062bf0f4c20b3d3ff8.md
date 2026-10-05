as high) or OV (known as low). If you connect an input to the output from some other chip, that's fine, but if you want to detect whether a switch is made or broken, you have to give the input pin some help. This is normally done with a resistor connected from the input to either the 3V3 or the ground.

When a resistor is used in this way, it's called a pull-up or pull-down resistor, as shown in Figure 15-9. Of the two arrangements, pull-up is preferable, mainly switches are normally on the end of long wires and it is safer to have a ground a 3V3 voltage on a wire. This is because it tends to cause less damage if you accidentally connected a ground wire to the wrong place than a power wire. This arrangement of pull-up or pull-down resistors is so common that the computer processor in the PI has them built-in, and there is a software method for connecting or enabling internal pull-up or pull-down resistors. We show you in Chapter 16 how to control this software.

![](bbox=[0.129, 0.363, 0.809, 0.666])

Figure 15-9:
Two ways of using a GPIO as input.

# Learning which is hot: Getting grips with a soldering iron

Although you can do some interfacing without resorting to the soldering iron to join components together, get serious, you'll have to do some soldering at some stage or the other. This often induces fear and panic in the newcomer, even a beginner can solder successfully. In fact, Mike made his first soldering iron at the age of nine and by large turned that himself. Soldering involves two parts, the *solder*, which is an alloy of two or more metals, and the flux, a chemical cleaning agent. If you are soldering something like a gas pipe, you would apply the flux around the joint, heat the joint with a blow torch, and apply the rod of solder to the