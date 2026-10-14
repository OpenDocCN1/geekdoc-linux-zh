> **Note** When you’re interested in the state change from off to on, this is known as a *rising edge trigger*. And changes from on to off are called *falling edge triggers*.

# Reading Analog Inputs

These detect a continuous range of values. Unlike the digital pins, which can be used as either input or output, the analog pins on an Arduino are hardwired, so there is no need for initial configuration. This leaves you nothing to do except read their value:

```
int analogInputPin = 2;
int value = analogRead(analogInputPin);
```

The result of value will be in the range 0 to 1023 and represents the voltage on the pin, between 0 and 5v. If you reuse circuit from Figure 2-3, feeding the input to an analog pin instead of a digital one, you can watch the range of values being output by using this:

```
Serial.print("LDR brightness = ");
Serial.println(value);
```

This allows you to determine the precise brightness of the light empirically. You will notice a lot of fluctuations with this data, so the best approach is to determine whether it’s bright or dark enough to control the light, by having two limits and a dead band in the middle. That is, if the number drops from greater than X to less than X, then it’s considered light, and if it increases from less than X+N to greater than X+N, then it’s dark.
You can then add a variable resistor into the circuit to fine-tune this brightness, as shown in Figure 2-4. In addition to light, you can also measure temperature (thermistors), distances (ultrasonic range finders), and rotary positions (by attaching a handle or wheel to the spindle of a potentiometer).

![](bbox=[0.066, 0.571, 0.246, 0.817])

**Figure 2-4.** *Controlling the brightness at which the Arduino is controlled*