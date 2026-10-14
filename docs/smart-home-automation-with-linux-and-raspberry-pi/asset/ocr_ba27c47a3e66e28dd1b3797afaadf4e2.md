> **Note**  Servo motors that work through pulses may only be able to turn around a portion of their axis, maybe less than 270 degrees, and so can not be used in all applications.

ServoBlaster (https://github.com/richardghirst/PiBits/tree/master/ServoBlaster) is a library that is capable to driving up to eight servo motors through the GPIO port of the Raspberry Pi, meaning it requires no additional hardware. In its most basic form, it is nothing more than a user space daemon (which still needs to be run as root, given it needs access to the GPIO) that detaches from the shell when you first run it:

```
$ sudo ./servod
```

However, you can also use the kernel space implementation that works by creating a new device /dev/servoblaster that handles all the timing, and you just need to specify the pulse width. A 1.3ms pulse width, on motor 4, would be addressed:

```
$ echo "4=130" > /dev/servoblaster
```

A value of zero will turn it off. With 8 servos, each taking 2.5ms to be serviced at the maximum latency—the time from issuing a command to seeing the effect—will be the cycle time, 8 * 2.5ms, or 20ms.

Given this cycle time, it is not possible to have a longer pulse than 2.5ms, or 12.5%. If you're working with LEDs, then longer pulses are necessary and made possible with a fork of the servoblaster code, called Pi-Blaster (https://github.com/sarfata/pi-blaster). Give it's obvious heritage, it is invoked in an identical manner, but using a fractional percentage for the pulse width, instead of an absolute time. A 12.5% pulse would therefore be:

```
echo "0=0.125" > /dev/pi-blaster
```

To expand the number of motor controllers, for building a robot perhaps, you will need to switch out your debugger for a soldering iron and install a physical add-on such as the Adafruit motor shield at http://adafruit.com/products/815 that provides up to 16 channels for servo motors.

For a more advance analogue I/O you could do well to consider a more recent development—the Gertboard. Although it is a very expensive board, it does come with a wealth of interfacing options using the full scope of the GPIO. The SPI is pressed into service for both an A2D (MCP4002) and a D2A (MCP4802) converter, while the sole PWM pin is used as a motor controller (L6203, buffered to a mighty 48V/4A). The UART is configured to take with an Atmel AVR microcontroller, and the remaining GPIO pins used for various buttons and LEDs for utility purposes. Being a predominantly analogue controller this is a better match for most projects because our (real) world is analogue, not digital!

> **Tip**  If you plan on including an Arduino in your Raspberry Pi setup at some point, then it’s worth considering getting just the Gertboard and the chip, as this will probably work out cheaper than buying a separate/additional shield and Arduino board.