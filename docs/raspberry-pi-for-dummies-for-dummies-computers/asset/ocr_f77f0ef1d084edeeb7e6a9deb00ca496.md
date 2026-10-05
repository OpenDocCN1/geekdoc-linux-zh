Although the units for calculation are volts, amps, and ohms, 1 amp (A) is in practice a lot of current, and it's more common to talk of milliamps, or mA. There are 1,000 mA in 1A. Similarly, 1000 R is one kilogram, or 1 K.

# Calculating circuit values

Although the circuit in Figure 15-5 is all very well because it describes what's actually wired up, it's not useful for calculating anything using ohms because it has no resistances. However, each real component has associated with a resistance. We say it has an equivalent circuit. These are shown in Figure 15-6. All components, even the wires, have some series resistance. In other words, they behave like they have a resistor in line with the component. Sometimes- this is important, and sometimes it is not. The trick is in knowing when to ignore them.

![](bbox=[0.137, 0.376, 0.597, 0.638])

When resistors are placed in series, or in line with each other, you can find the resistance by simply adding up all the individual resistance values. Figure 15-6 shows our circuit with the series resistance values shown. If we add up all the values around the circuit, we get 18R105. (That's 18.105 ohms.) Note that virtually all of the resistance in the circuit comes from the bulb. The series resistance of the switch is negligible, as is the resistance of the battery. This is not always the case. So, with 18R resistance and 6V, we can calculate that the current through the circuit should be

```
I = E/R -->
Current = 6/18 = 0.333 Amps or 333mA
```