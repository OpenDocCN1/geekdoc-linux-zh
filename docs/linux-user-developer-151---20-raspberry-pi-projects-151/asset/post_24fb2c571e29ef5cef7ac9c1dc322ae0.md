
# Tutorial: Make a Raspberry Pi 2 HTPC

Finally create a more powerful and capable HTPC using the Raspberry Pi 2 and the excellent OpenELEC project.

**Rob Zwetsloot** models complex systems and is a web developer proficient in Python, Django, and PHP. He loves to experiment with computing.

We know people who just have a great idea and a great use for the Pi – it works just well enough that you can easily play media locally or over the network. The biggest issue comes with GUI response on the original Model Bs, and a lack of USB ports for connecting up everything that you want.

While optimization over the last few years has helped, the leap to Raspberry Pi 2 has basically solved all of these problems by giving you much more powerful hardware to play with. So if you're looking to upgrade or finally take the plunge, this handy guide will help you create the perfect Raspberry Pi 2 HTPC.

### 01 Choose the software
In the past, Pi HTPCs were just a choice between RaspBMC and OpenELEC. However, RaspBMC is on a bit of a hiatus, and OpenELEC is your best bet for getting the most up-to-date software. There's not a massive difference between the two, as they both run XBMC.

### 02 Get the software
Head over to openelec.tv and look for the Download section. There's a specific Raspberry Pi section which is split up into original (ARMv6) Pi and the newer Raspberry Pi 2 (ARMv7). Grab the image file from this page for the Pi 2.

![](img/c9d26cf718256f071c3af699b9670538_65_0.png)

## What you'll need
- OpenELEC openelec.tv
- HDMI cable
- USB IR receiver
- IR remote
- Case
- Dedicated power supply
- Optional USB storage

www.linuxuser.co.uk

![](img/c9d26cf718256f071c3af699b9670538_66_0.png)

### 03 Install to card
Open up the terminal and use `fdisk -l` to determine where your SD card is located on your system. Something like `/dev/sdb` or `/dev/mmcblk0` will be ideal. Navigate to the image using `cd` and install it with `dd` using:

```bash
$ dd bs=1M if=OpenELEC-RPi2.arm-5.0.5.img of=/dev/mmcblk0
```

### 04 First boot
Plug in your Raspberry Pi, either to your TV or to another screen just to begin with, and turn it on. OpenELEC will resize the SD card partitions and write a few extra programs before finally booting into Kodi.

![](img/c9d26cf718256f071c3af699b9670538_66_1.png)

*Above*
Kodi really is designed to be used with a remote, and there are some great guides to using them on the OpenELEC site: **bit.ly/1BOARv**

### 05 Configure Kodi
Go through the basic wizard to get through the interface - if you are connecting via wireless you will need to go to OpenELEC in the System menu and activate the wireless receiver before selecting your network and then entering your password.

### 06 Add network shares
You can stick a portable hard drive or USB stick into the Pi for storage, but the best method is really to stream over the network. Go to File manager under System and Add source. Go to Browse and choose your network protocol to browse the network or alternatively, add it manually.

### 07 Build your media centre
Placement of your Raspberry Pi is important. As it's going to be out all the time, we highly recommend getting a case for it - the Pibow cases from Pimoroni are quite well suited for this type of use as they are sturdy and can be attached to the rear of some TVs.

### 08 IR sensors and controllers
Kodi can be controlled with a number of different things - including USB game controllers and compatible IR sensors. We've used FLIRC in the past, but if you have your Pi behind the TV, you'll need a sensor on a wire that can stretch to a useful position.

### 09 Future updates
OpenELEC has the excellent ability to update itself without needing you to re-install it every few months, meaning you won't need to do much maintenance on it at all. Now you can sit back and enjoy your media much easier than before.

## Live TV
Kodi does have the ability to play live TV via a TV tuner, and you can also record stuff as well as long as you have the local memory. The main thing you'll need to invest in is a compatible TV tuner, a list of these is available here: **bit.ly/1r3mEj**

![](img/c9d26cf718256f071c3af699b9670538_67_0.png)

## What you'll need
- Breadboard & wires
- 16x16 LED Matrix
- 2x 74HC238
- 2x 74HC244
- 16x 220 Ohm Resistor
- Source code **FileSilos.co.uk**

# Build a complex LED matrix

LED Matrix display systems find use everywhere from gaudy kebab shops to impressive steampunk-styled systems.

![](img/c9d26cf718256f071c3af699b9670538_67_1.png)

**Tam Hanna**
has worked in IT since the Palm IIc days. A journalist, tutor, speaker and author, Tam has seen every aspect of the mobile market more than once.

Driving LEDs in an efficient fashion is a science of its own. The common availability of single-board computers has put the necessary technology within reach of everyone.

When dealing with LED displays, two different systems must be considered. We will focus on traditional matrix-based systems made up of one or more LEDs. Their affordable nature makes them ideally suited to classic display applications: they communicate currency prices, provide stock-brokers with updates from the trading floor and have even been used as basic displays for primitive oscilloscopes.

Finally, we will also provide you with an overview of electronic basics. This tutorial is a bit more advanced than the ones we usually run in this section of the magazine, and it's also worth noting that we're going to be programming with C rather than Python. Follow along using the code listing annos.

### 01 Think about LEDs
Standalone LEDs are primitive – they light up once current flows through them. Driving a few LEDs is as easy as connecting them to GPIO pins along with a resistor. Sadly, this method becomes wasteful once more than a few of them get involved – driving 16 diodes ties up 16 pins.

### 02 Arrange your diodes
Methods were devised to reduce the number of pins needed. Matrix-based systems are resilient to individual diode failures, and provide a pin-to-LED ratio of n=(n/2)². The following steps assume a 16x16 LED matrix which is made up according to Figure A. Since LEDs permit current in only one direction, you can enable a single LED by bringing the corresponding pins high and low.

![](img/c9d26cf718256f071c3af699b9670538_68_0.png)

*Above* The extended version of this schematic is inside FileSilo.co.uk – just sign in and head to the issue #151 page

### 03 Harness the MUX
Our LED module has a total of 32 inputs, which overwhelms older versions of the RPI. The first way to restrict their number comes in the shape of the 74HC238, a component described as a 3-to-8 line decoder/demultiplexer. Its function is described in the Figure B image on the next page.

### 04 Separate concerns
Chip two goes by the name of 74HC244, which is described as an octal buffer with tri-state capability. Tri-State outputs can physically disconnect themselves from the bus line. This permits you to tie their outputs together without fear of short circuits. As long as all but one chip are in tri-state mode, no current can flow between high and low output pins.

### 05 Round them up
Four GPIO pins control the currently-enabled ‘line’ of the display. Three pins configure the address which is to be emitted, while the signal emitted from the fourth pin is connected to the activity inputs. This ensures that but one IC is active. The 74HC244 ensures that but one of the two groups is active at any given time.

### 06 Configure the pins
We used a library from Hussam Al-Hertani’s Hertzville blog (hertzville.com/2014/07/07/rpimmapgpio). The first step involves setting output functions. As the GPIOs are set to outputs, the tri-state feature might connect the internal state to the output pins of the IC. This could lead to internal shorting if the output is not turned off.

## Full code listing

Step 12
```c
#include <mmapgpio.h>
#include <stdio.h>

#define PINA0 2 // 3
#define PINA1 3 // 5
#define PINA2 4 // 7
#define PINA3 14// 8
#define PINS0 17// 11
#define PINS1 18// 12

#define PIND0 23// 16
#define PIND1 24// 18
#define PIND2 10// 19
#define PIND3 9 // 21
#define PIND4 25// 22
#define PIND5 11// 23
#define PIND6 8 // 24
#define PIND7 7 // 26
```

Step 07
```c
void setAddress(unsigned char _which, mmapgpio* _where)
{
if (_which&1)
{
    _where->writePinHigh(PINA0);
}
else
{
    _where->writePinLow(PINA0);
}
if (_which&2)
{
    _where->writePinHigh(PINA1);
}
else
{
    _where->writePinLow(PINA1);
}

if (_which&4)
{
    _where->writePinHigh(PINA2);
}
else
{
    _where->writePinLow(PINA2);
}

if (_which&8)
{
    _where->writePinHigh(PINA3);
}
else
{
    _where->writePinLow(PINA3);
}
}
```

Step 08
```c
void safelySetRow(unsigned char _which, mmapgpio* _where)
{
    _where->writePinHigh(PINS0);
    _where->writePinHigh(PINS1);
    if (_which==0)
    {
        _where->writePinLow(PINS0);
    }
    else
    {
        _where->writePinLow(PINS1);
    }
}
```
