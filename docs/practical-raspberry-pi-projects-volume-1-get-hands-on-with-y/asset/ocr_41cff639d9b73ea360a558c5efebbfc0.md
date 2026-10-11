# **ELECTRONICS**

![](bbox=[0.09, 0.12, 0.42, 0.36])

**07 Power the mux**
Create a convenience function taking an address ranging from zero to 15. It is converted into pin outputs for our 3-to-8-demultiplexer. The effect of this is that all but one of the sixteen rows is to be supplied with energy.

**08 Select a row**
In the 74HC244, we first disable both units and proceed to turning on the one which is needed. This sequence prevents ghosting during the switching process.

**09 Do the main loop**
The outer part of the loop consists of logic that manages the addressing of the individual rows. Our program must flash the individual LED groups one after another using the building blocks described in the next step.

**10 Complete the loop**
Writing out data is accomplished in a sequence of three commands. We select the row, configure the column and then write out the data bits that are to be displayed. A small pause is observed in order to give the LEDs some time to 'burn into' the viewer's eyes.

![](bbox=[0.09, 0.68, 0.42, 0.91])

# Full code listing

```
Step 38

\_where->writePinLow(PINS1);
}

Step 17

void setdata(uint8 char\_which, mm\_cpLo\*\_where)
{
if(_which&1)
{
\_where->writePinHigh(PINDO);
} else
{
\_where->writePinLow(PINDO);
}
if(_which&2)
{
\_where->writePinHigh(PIND1);
} else
{
\_where->writePinLow(PIND1);
}
if(_which&4)
{
\_where->writePinHigh(PIND2);
} else
{
\_where->writePinLow(PIND2);
}
if(_which&8)
{
\_where->writePinHigh(PIND3);
} else
{
\_where->writePinLow(PIND3);
}
if(_which&16)
{
\_where->writePinHigh(PIND4);
} else
{
\_where->writePinLow(PIND4);
}
if(_which&32)
{
\_where->writePinHigh(PIND5);
} else
{
\_where->writePinLow(PIND5);
}
if(_which&64)
{
\_where->writePinHigh(PIND6);
} else
{
\_where->writePinLow(PIND6);
}
if(_which&128)
{
\_where->writePinHigh(PIND7);
} else
```

# LED stripes

Two versions of LED stripes are offered.
'Primitive' ones are based on analogue technology. In it, an entire strip of diodes has the colour set by the three input pins. Systems such as the mega display shown on the left- hand image require the use of the digital version. They are based on the concept of the shift register. Your system inputs individual colour values which are then pushed on along the strip.