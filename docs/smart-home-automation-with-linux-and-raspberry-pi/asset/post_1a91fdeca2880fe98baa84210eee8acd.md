
Programming the Gertboard is much like the low-level Arduino code. That is, you are writing directly to the memory-mapped IO and therefore need the careful skill of an assembly programmer. This code might appear banal like this:

```
PWMLCK_DIV   = 0x5A000000  ; (32<<12);
PWMLCK_CNTL  = 0x5A000011;

PWM_CONTROL  = 0;    // i.e. off
PWM0_RANGE   = 0x400; // all values between 0 and 1023

PWM0_DATA    = 0x100; // write output
```

This seemingly natural code (albeit a little heavy on the magic numbers), is all that's necessary to set up the PWM. However, hiding behind these macros are pointer indirections such as:

```
#define PWM_CONTROL *pwm
#define PWM0_STATUS  *(pwm+1)
#define PWM0_RANGE   *(pwm+4)
#define PWM1_RANGE   *(pwm+8)
#define PWM0_DATA    *(pwm+5)
#define PWM1_DATA    *(pwm+9)
```

So all that's necessary is a missed warning about incorrect data types, and you’ll be corrupting the subsequent register and be tracing nonexistent bugs for hours! More information on this board can be found on the Element14 site at http://www.element14.com/community/docs/DOC-5172?ICID=raspi-group.

Naturally, other interfacing boards are available, with Pi-Face from Manchester University, Pi Crust, and Quick2Wire. More are coming out each month, so a quick web search for “buffer boards” or “expansion boards” will let you know of the current state of the art.

## With the Arduino

The simplest way to connect the Raspberry Pi to the outside world is through an Arduino, as we already have many years experience with the device. Furthermore, there are many useful shields already available. For most people, this is a waste of effort because the Arduino is capable of processing most input devices that we care about. However, it does provide a level of security knowing that if you make an error, it is the (cheaper) Arduino that will blow up, and not your beloved Raspberry Pi!

## USB

Despite the issues mentioned previously about USB on the Raspberry Pi, this is the simplest and safest way to connect the two machines. You simply plug one into the other!

As far as software goes, the Arduino processes its input and writes data out using the traditional:

```
Serial.begin(9600);
pinMode(inputSwitchPin, INPUT);
pinState = digitalRead(inputSwitchPin);
Serial.println(pinState ? '1' : '0');
```

And there is a program on the Raspberry Pi reading this from the serial device. You’ll need to set-up the device with:

```c
char *szUSBDevice = "/dev/ttyUSB0";
```

```c
FILE *fp = fopen(szUSBDevice, "r");
```

and then read data from the serial device in a tight loop, executing something not dissimilar to:

```c
if (fread(&v, 1, 1, fp)) {
    if (v == '0') {
        if (v == '1') {
        }
    }
}
```

Naturally, this is very slow and has considerable latency between an event occurring, being discovered by the Arduino, and then transmitted and processed on the Raspberry Pi. To improve this, you need to look at using the I²C bus.

## I²C

I²C is a two-wire interface called Inter-Integrated Circuit. It is a bus protocol, designed originally by Philips, to connect slow peripherals directly to a computer motherboard. By putting data directly onto the bus, latency between devices can be drastically reduced. Furthermore, you can connect up to 128 devices on an I²C bus which far exceeds the rather timid USB solution we covered earlier.

> **Caution** When connecting devices directly onto the bus of another, you have no isolation or protection that other methods (such as USB) provide. It is therefore easier for one device to (physically) harm another, or allow, through inaction, harm to come to it. In the specific case of connecting Arduino and Raspberry Pi, remember that they work at 5V and 3.3V respectively, and need a level shifter to correctly harmonize the voltages.

The hardware component is as easy as it should be for a two-wire protocol—you connect the SDA of the Raspberry Pi to the SDA of the Arduino, and the SCL of the Raspberry Pi to the SCL of the Arduino, and that’s it. Granted, you need the level shifters that we used previously (and you might like to add some pull-up resistors for safety) but, otherwise, all that’s necessary is as it appears in Figure 8-6.

![](img/cbcdf34138bb96edef7aa6057d0d0d0e_303_0.png)

*Figure 8-6.* Connecting a Raspberry Pi to an Arduino

Build it, then power on and run the software on the Arduino, so that it is able to register itself on the I²C bus:

```cpp
#include "Wire.h"

int i2cAddress = 0x03;

void setup() {
  Wire.begin(i2cAddress);
}
```

The rest of the software is as simple as the hardware! First check that the Arduino can be found on the bus. So, on the Raspberry Pi, simply run:

```text
$ sudo modprobe i2c-dev
$ sudo i2cdetect -y 0
```

|     | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | a   | b   | c   | d   | e   | f   |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| 00: |     |     | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  |
| 10: | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  |
| 20: | --  | --  | --  | 03  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  |
| 30: | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  |
| 40: | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  |
| 50: | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  |
| 60: | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  |
| 70: | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  | --  |

From this, you can see that your Arduino is successfully connected to the bus, and on address 03. If you don’t see the Arduino, then it’s likely you’re using a revision 2 board, and therefore need to use bus 1, and not bus 0, so change the i2cdetect command above, and SMBus reference below.

Sending data from the Raspberry Pi uses the smbus library and code such as:

```python
#! /usr/bin/python
import smbus
bus = smbus.SMBus(0)

address = 0x03
dataToSend = 42

bus.write_byte_data(address, 0xC9, dataToSend)
```

Notice that we send two bytes, even though only one is needed. This first byte (0xC9) is like a header that indicates the type of data we’re sending. The Arduino can then watch for data on the I²C bus, at address 3, and respond accordingly. We therefore amend our program above to read:

```cpp
#include "Wire.h"

int i2cAddress = 0x03;

void setup() {
  Wire.begin(i2cAddress);
  Wire.onReceive(receiveEvent);
}

void receiveEvent(int size) {
    if (size == 2) {
        int header = Wire.read();
        int dataRead = Wire.read();
        if (header == 0xC9) {
            // Do something
        }
    }
}
```

The equivalent, but more rare, code to send data from the Raspberry Pi back to the Arduino is left as an exercise for the reader!

## With SPI

As a de facto standard, the Serial Peripheral Interface Bus is a method of communicating between a single master (the Raspberry Pi in our case), and an arbitrary number of slave peripherals. Although it is only possible to control, or query, one slave at a time, its high speed of operation along with full duplex operation makes this a useful approach for many microcontrollers and other such projects.

The hardware necessary involves just five pins of the Raspberry Pi’s connector, SCLK (the clock), MOSI (master out), MISO (master in), and CE0/CE1 (both select which slave to use.) The MOSI/MISO pair provides the transmit/receive pairing for the full-duplex communication channel, while the SCLK is used to keep all the slaves in sync with the master. As a consequence of this, there is no need to run separate clocks on the slave machines, which makes it easier to find suitable oscillators and they don’t need to be precise. This effort of simplifying the circuitry is also demonstrable by the fact that, unlike I²C, no pull-up or pull-down resistors are needed; you can simply connect the MOSI on the master to the MOSI on the slave (repeat for MISO and SCLK) and you’re nearly ready!

The slave select indicates to which of the slave devices the master is talking. The Raspberry Pi hardware provides two of these, CE0 and CE1, which utilize /dev/spidev-0.0 and /dev/spidev-0.1. As a protocol, however, SPI allows you to control as many slaves as you like. Therefore, it is possible (and indeed, suggested) that you use the other GPIO pins to select the necessary slave, using a low logic 0 to indicate the slave in question. Since you can’t use the standard SPI library, you must manually handle the slave selection by writing to the GPIO as we saw earlier. Timing between the GPIO and SPI is a question of ordering it correctly—first take all the GPIO pins used in slave selection high to logic 1, wait, and then take the appropriate pin low.

> **Tip** If you write your own slave select driver, then you should always begin by sending the selection pins high, and then low, since some slaves are only awoken by the falling edge.

The projects possible with SPI are much the same as if you were using GPIO or I²C. What you gain in the simplified electronics, you lose on the software, so you need to write your own error handling and hand-shaking code since there is no way of knowing if the slave received the messages sent to it, nor is there any error checking in the protocol itself. If your project is to be in an electrically noisy environment (maybe the utility room, with the powerful motors of a washing machine and tumbler dryer), then this is a valid concern, since SPI is more susceptible to noise. If you have no SPI slaves with which to experiment, then you’re probably wrong (!) because anything capable of communicating on four different pins can be pressed into service . . . the Arduino is a suitable candidate for this. A proof of concept can be found at http://hackaday.com/2013/01/06/hardware-spi-with-python-on-a-raspberry-pi.
