
be connected between the computer's power supply of 3.3V or ground (that's 0V). This is sometimes called the common ground or reference, and it is the basis of all measurements in a circuit. Basically, it's the other end of the battery – the negative terminal, if you will. Between this switch and the output is in effect a series resistor, one that is in line with the voltage coming from the Pi. It limits the current you can get through the output pin.

On the Pi, the value of this resistor can be changed over a limited range. The default value is 33Ω, but note that resistor, by itself, is insufficient to protect the Pi from giving too much current if you connect it to too low a resistance load. If you did this, then your Pi would be permanently damaged. So an output pin can switch between two voltages — 0V and 3.3V. These are known as logic levels, and they have a number of names: high and low, true and false, zero and even up and down.

![](img/df9a01bf057d58c2401b5edabd6e8829_325_0.png)

## FINDING A SAFE VALUE OF CURRENT

There is a value of current that would instantly destroy at least the circuitry of the pin, if not the whole Pi itself. But, there is also a value of current that would not instantly kill the Pi but would damage the circuitry and lead it to fail prematurely. Lower the current, and the damage is lowered, until you get to a point where no damage occurs. However, these values are not known for the chip used on the Pi. In fact, they are not known for the vast majority of chips. It's best to stick to the "safe" value or lower.

Beware of people who say that they have a circuit that takes 30mA or more from a pin and still working. They tend to be idiots who confuse whether a pin is dead with whether a pin is safe. It is just like smoking: You can do it and it doesn't kill you immediately, but it does do harm and eventually it can kill, if nothing else gets you first. No one would pretend that it's safe.

310 PART 5 Exploring Electronics with the Raspberry Pi

Although logic voltage levels on the Pi are simple, the current these outputs can supply more complex, with a current limit of about 16mA. This limit is how much the Pi should supply into a load, not how much it can supply or will supply. That depends on the resistance of the load connected to the Pi. We say that the limit is about 16mA, but this is a bit of a gray area. This value is considered safe for the Pi to supply, but that not to say a value of 17mA would be considered dangerous or excessive.

## Putting an output pin to practical use

Can you do with a switched output? Well, you can drive a small current through a load, or you can control another device that can control a bigger current through a load. Put like that, it doesn't sound exciting, but it's what physical computing is all about — it is the gateway to all control. The load can be a light, a motor, a solenoid (an electromagnetic plunger used to prod or strike things), or anything that uses electricity. Because that includes everything in the modern world, it is safe to say that it uses electricity, it can be controlled, and more importantly for our purposes, controlled by a Pi.

Take a look at controlling a light — not the current-heavy flashlight bulb we looked at, but rather a component known as a light-emitting diode (LED). These can light up from a tiny bit of current, and the 16mA we have available is more than enough for that task. In fact, you're going to limit the current to less than 10mA by adding a 330R-series resistor.

For the moment, just look at the circuit in Figure 15–8. This shows two ways to wire an LED — or other load — directly to a GPIO pin. Here we just show the GPIO pin and not the equivalent series resistance of the power source as discussed earlier — in the context of a 330ohm resistor, 31Ω is negligible.

The first way to it, called current sourcing, is perhaps a beginner might think of as natural. When the GPIO pin is set by the program to produce a high voltage (that is, when the switch is set to connect the 3.3V line to the output pin), current flows from the pin through the LED, through the resistor and to ground, completing the circuit, causing current to flow and so lighting the LED. When the GPIO pin is set by the program to produce a low voltage (that is, when the switch is set to connect the 0V or ground line to to the output pin), no current flows and the LED is not lit. This method is known as current sourcing because the source of the current — the positive connection of the power — is the GPIO pin.

![](img/df9a01bf057d58c2401b5edabd6e8829_327_0.png)

The second way of wiring (refer to Figure 15-8) is known as current sinking. When the GPIO pin is set by the program to produce a low voltage, the current flows through the LED, through the resistor, and to ground, the GPIO pin. To turn off the LED, set the output to a high voltage. There's no way current can flow round the circuit, because both ends of the load (LED and resistor) are connected to 3V — so there is no voltage difference to push the current through the components.

Note in both circuits that the position of the resistor and LED can be interchangeable — it makes no difference. You might like to think of these two approaches as switching the plus and switching the ground.

Now an LED is a non-linear device in a similar way to the filament of a flashlight bulb, but in the case of an LED we need a resistor to limit the current to a value; it important thing to know is the LED's voltage drop — the voltage that will appear across when the LED is on. This changes with different colours of LED, so to get the same current through LEDs of different colours, you need different resistors.

Getting the same brightness is not the same as getting the same current, because different LEDs have different current–to–light efficiencies. Modern LEDs are a lot more efficient than they are used to, so you need less current.

With a red LED, there is about a 2V2 voltage drop across it. This leaves the remaining voltage from the GPIO pin (3.3–2.2 = 1.1V) to be dropped across the resistor. With a 330R resistor, Ohm's law tells you the current will be −1.1 / 330 = 3.3mA, which is plenty bright to see.

312 PART 5 Exploring Electronics with the Raspberry Pi

![](img/df9a01bf057d58c2401b5edabd6e8829_328_0.png)

Don't try to run the LEDs at too much current. Although you will be able to take 20mA, if you did this your GPIO pin would be supplying too much current and your Pi could be damaged. There should be no need to run an LED harder than 10mA.

## Using GPIOs as inputs

The other basic mode of operation for a GPIO pin is as an input. In this case, you don't have to worry about the current, when the pin is an input, and it has a high input impedance, or a high value of series resistance, and therefore little or no current can flow with normal logic voltages. A resistance is a special form of impedance, as its name implies, the flow of electricity. There is a bit more to impedance than simple resistance, but at this stage, you can think of them as the same sort of thing. They are both measured in ohms.

Resistance is the property of a material, whereas impedance is the property of a circuit and includes how it behaves with AC as well as DC. So input pin has a very high impedance. It allows hardly any current to flow through it, so much that we can connect it directly to 0V or 3.3V with no extras. In fact, an input is so high-impedance that if you leave it unconnected, it picks up very tiny radio waves and other forms of interference and gives random values when you try to read it.

In fact, the human body can act as an antenna when close to or touching a high-impedance input, causing any readings to go wild. This often amazes beginners, who think that have discovered something mysterious. They in fact, the tiny amounts of energy in the radio waves that are all around us are not absorbed by the high-impedance circuits as they would be by low-impedance circuits. A low impedance would cause current to flow, but it would absorb all the power, leaving minuscule amounts of voltage. The fact that you have a wire carrying AC power (mains) is close enough for that wire to radiate radio interference.

To explain why this is so, consider that interference of 2V is over the signal from a chip and cause it to malfunction. With a resistance of , in order to develop 2V across, it has a current of 2mA (Ohm's law) flowing through it. This represents a power (volts × I)=4mW of interference. However, with a resistance of 1M, you can get 2V across by only having 2UA flowing through it. So a high resistance is more sensitive to interference because it requires less power from the interfering source to develop the same voltage. This underlines an important fact about inputs: They't simply be left alone; they must be driven to one voltage state or the other; that is, either 3.3V (known

CHAPTER 15 Understanding Circuits 313
