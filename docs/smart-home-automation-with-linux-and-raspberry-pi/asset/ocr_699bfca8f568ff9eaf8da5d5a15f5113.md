and there is a program on the Raspberry Pi reading this from the serial device. You’ll need to set-up the device with:

```
```c
char *szUSBDevice = "/dev/ttyUSB0";
```
```

```
```c
FILE *fp = fopen(szUSBDevice, "r");
```
```

and then read data from the serial device in a tight loop, executing something not dissimilar to:

```
```c
if (fread(&v, 1, 1, fp)) {
    if (v == '0') {
        if (v == '1') {
        }
    }
}
```
```

Naturally, this is very slow and has considerably latency between an event occurring, being discovered by the Arduino, and then transmitted and processed on the Raspberry Pi. To improve this, you need to look at using the I²C bus.

# I²C

I²C is a two-wire interface called Inter-Integrated Circuit. It is a bus protocol, designed originally by Philips, to connect slow peripherals directly to a computer motherboard. By putting data directly onto the bus, latency between devices can be drastically reduced. Furthermore, you can connect up to 128 devices on an I²C bus which far exceeds the rather timid USB solution we covered earlier.

> **Caution**  When connecting devices directly onto the bus of another, you have no isolation or protection that other methods (such as USB) provide. It is therefore easier for one device to (physically) harm another, or allow through inaction harm to come to it. In the specific case of connecting Arduino and Raspberry Pi, remember that they work at 5v and 3.3v respectively, and need a level shifter to correctly harmonize the voltages.

The hardware component is as easy as it should be for a two wire protocol-you connect the SDA of the Raspberry Pi to the SDA of the Arduino, and the SCL of the Raspberry Pi to the SCL of the Arduino, and that’s it. Granted, you need the level shifters that we used previously (and you might like to add some pull-up resistors for safety) but, otherwise, all that’s necessary is as it appears in Figure 8-6.

![](bbox=[0.1, 0.692, 0.636, 0.882])

*Figure 8-6.* Connecting an Raspberry Pi to an Arduino