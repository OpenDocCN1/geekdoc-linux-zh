
## ELECTRONICS

![](img/a1548a579bd09ff29b2b92de3f565e63_131_0.png)

### 07 Power the mux
Create a convenience function taking an address ranging from zero to 15. It is converted into pin outputs for our 3-to-8-demultiplexer. The effect of this is that all but one of the sixteen rows is to be supplied with energy.

### 08 Select a row
In the 74HC244, we first disable both units and proceed to turning on the one which is needed. This sequence prevents ghosting during the switching process.

### 09 Do the main loop
The outer part of the loop consists of logic that manages the addressing of the individual rows. Our program must flash the individual LED groups one after another using the building blocks described in the next step.

### 10 Complete the loop
Writing out data is accomplished in a sequence of three commands. We select the row, configure the column and then write out the data bits that are to be displayed. A small pause is observed in order to give the LEDs some time to 'burn into' the viewer's eyes.

![](img/a1548a579bd09ff29b2b92de3f565e63_131_1.png)

### Full code listing

```cpp
// Step 38
    _where->writePinLow(PINS1);
}

// Step 17
void setdata(uint8_t char_which, rtmpGpio_rpiGpio** _where)
{
    if(_which&1)
    {
        _where->writePinHigh(PIND0);
    } else
    {
        _where->writePinLow(PIND0);
    }
    if(_which&2)
    {
        _where->writePinHigh(PIND1);
    } else
    {
        _where->writePinLow(PIND1);
    }
    if(_which&4)
    {
        _where->writePinHigh(PIND2);
    } else
    {
        _where->writePinLow(PIND2);
    }
    if(_which&8)
    {
        _where->writePinHigh(PIND3);
    } else
    {
        _where->writePinLow(PIND3);
    }
    if(_which&16)
    {
        _where->writePinHigh(PIND4);
    } else
    {
        _where->writePinLow(PIND4);
    }
    if(_which&32)
    {
        _where->writePinHigh(PIND5);
    } else
    {
        _where->writePinLow(PIND5);
    }
    if(_which&64)
    {
        _where->writePinHigh(PIND6);
    } else
    {
        _where->writePinLow(PIND6);
    }
    if(_which&128)
    {
        _where->writePinHigh(PIND7);
    } else
```

### LED stripes
Two versions of LED stripes are offered.
'Primitive' ones are based on analogue technology. In it, an entire strip of diodes has the colour set by the three input pins. Systems such as the mega display shown on the left- hand image require the use of the digital version. They are based on the concept of the shift register. Your system inputs individual colour values which are then pushed on along the strip.

## BUILD A COMPLEX LED MATRIX

![](img/a1548a579bd09ff29b2b92de3f565e63_132_0.png)

Above This is the full schematic of the LED matrix that we're working with here (you can also view it at its full size on FileSilio).

### Full code listing

```cpp
{
    _where->writePinLow(PIND7);
}

int main(void)
{
    rtmpGpio rpiGpio;
    // Set outputs
    rtmpGpio_setPinDir(PINA0, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PINA1, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PINA2, rtmpGpio::OUTPUT);
    // Data out RS491
    rtmpGpio_setPinDir(PINCS0, rtmpGpio::OUTPUT);
    rtmpGpio_writePinHigh(PINCS0);
    // Data out RS491
    rtmpGpio_setPinDir(PINCS1, rtmpGpio::OUTPUT);
    rtmpGpio_writePinHigh(PINCS1);
    rtmpGpio_setPinDir(PIND0, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND1, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND2, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND3, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND4, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND5, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND6, rtmpGpio::OUTPUT);
    rtmpGpio_setPinDir(PIND7, rtmpGpio::OUTPUT);
    
    unsigned char dataStore[2][16];
    
    for(int j=0; j<2; j++)
    {
        for(int k=0; k<16; k++)
        {
            dataStore[j][k] = 64;
        }
    }
    
    int blockCounter = 0;
    int rowCounter = 0;
    while(1)
    {
        blockCounter++;
        if (blockCounter == 16)
        {
            if (rowCounter == 0)
            {
                blockCounter = 0;
                rowCounter = 1;
            }
            else
            {
                blockCounter = 0;
                rowCounter = 0;
            }
        }
        
        safelySetRow(rowCounter, &rpiGpio);
        setAddress(blockCounter, &rpiGpio);
        setData(dataStore[rowCounter][blockCounter], &rpiGpio);
        usleep(50);
    }
    return 0;
}
```

### 11 Energy control
LEDs light up if current flows through them. SetData pulls the pins of the 74HC244 low to ensure that the energy supplied from the 74HC238 can flow through the diode.

### 12 Avoid GPIO trouble
The Raspberry Pi Foundation has a tendency to change the layout of the expansion header regularly, a habit which professional manufacturers of process computers abhor. It's recommended to handle the mapping between pins and functions via a set of defines. Our code is optimised for a Rev2 Raspberry Pi with a 'short' header - 40-pin variants will require readjustments making sure the physical pin numbers correspond to the logical GPIO numbers.

### 13 Add example data
Test the code by setting the datastore to a value of your choice. Setting 64 to all fields will disable one row in each part of the display.

### 14 Kick it off
Check all connections between the planar and the single-board computer, and proceed to starting the compiled app. Don't forget to use the sudo command - direct memory access is restricted to root in order to prevent apps from causing havoc in the physical memory. Users are accustomed to this, so requiring them to put a sudo in front of the command doesn't cause concern.

### 15 Notice a flicker
Sharp-eyed readers will notice an occasional flicker where one line appears brighter than the others. This is caused by the stalling of the program - if the kernel does other work, the switching routine can't run. We could solve this problem by using a real-time Linux kernel.

## Add gesture control to your Raspberry Pi

Hover is an impressive add-on board for your Raspberry Pi that allows you to easily add touch and gesture control to any project

![](img/a1548a579bd09ff29b2b92de3f565e63_133_0.png)

### What you'll need
- Raspberry Pi
- Hover
- Breadboard
- Male to female jumper cables
- Speaker or headphones

People often ask **what the best way is for them to get started with Raspberry Pi**. Obviously this does depend on the individual user and what they want to achieve and get out of any project, but in a more general sense it’s often the hardware projects that win out for getting to grips with it. They teach a variety of skills (including programming, circuit building, soldering, hardware design and much more!) and are also varied enough to both keep beginners interested and allow them to work out for themselves exactly what aspect they love best. Even a seasoned professional will get a serious kick out of a bit of physical computing and automation! This is one of the unique features of the Pi compared to traditional “black box” computers: you can break out of the usual boundaries and interface with everyday objects like never before.

One of the most important aspects of a hardware project is often the user input mechanism, and as technology is refined we see new and more intuitive ways to accomplish this task. Gesture and touch control is now present in a large number of consumer devices and even the biggest technophobes are starting to embrace the ease of this technology. It is time to bring your Raspberry Pi projects into the 21st century with Hover!

## ADD GESTURE CONTROL TO YOUR RASPBERRY PI

![](img/a1548a579bd09ff29b2b92de3f565e63_134_0.png)

**The physical pins you should be using on the Raspberry Pi are 1, 3, 5, 6, 16 and 18**

**Above** You can tap the Hover or swipe in four directions just above it

![](img/a1548a579bd09ff29b2b92de3f565e63_134_1.png)

### Plenty of platforms

#### 01 Get the gear!
The Hover add on board is available to purchase direct from Hover (http://www.hoverlabs.co/#shop) for $39 (£25), however this will ship from Northen America and therefore if you are based in the UK or Europe it will likely be quicker and cheaper to order from one of the other retailers listed via the above link.

The added benefit of ordering from a retailer is that if you need any of the other items you can likely get those at the same time!

Hover will work perfectly with any Raspberry Pi, including both the new plus versions and the older models – just make sure your system is fully up to date with:

```bash
sudo apt-get update
sudo apt-get upgrade
```

#### 02 Update GPIO and I2C
When making use of GPIO and I2C (or any other interfacing technique on the Raspberry Pi) it is always good practice to update to the very latest software versions possible. Newer versions typically have bug fixes and additional features which can come in very handy. GPIO and the RPi.GPIO Python library are installed by default on Raspian, but you may need to enable I2C if you haven't already. This is a fairly standard process and has been covered many times so we won't go into it here. We would, however, highly recommend the brilliant I2C setup tutorial from Adafruit (https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

#### 03 Set up the hardware
Make sure your Raspberry Pi is powered down and not connected to power before starting this step, to avoid any unnecessary damage to your Raspberry Pi. Pick up your Hover, breadboard and wires and connect the as shown in the Fritzing diagram. The physical pins you should be using on the Raspberry Pi are 1, 3, 5, 6, 16 and 18. Whilst a Model B Pi is shown, this will be the same connection on a Model A, B, A+ or B+ of any revision. Once completely set up like the image, reconnect the power cord and open an LXTerminal session.

#### 04 Check the connection
Hover connects to the Raspberry Pi through the I2C interface located on the main 26 or 40 pin GPIO bank (depending on which version of the Raspberry Pi you are using). There is a very easy way to check if your Raspberry Pi is correctly connected to Hover using the simple command line I2C tools. Issue the following command:

```bash
sudo i2cdetect -y 1
```

If you see 42 in the response then you are successfully connected to Hover!

The Hover board has intelligent on-board level shifting, meaning that it can be used with either 3.3V or 5V logic levels which means it can be used with pretty much any microcontroller your heart desires. There are connection examples and code snippets available for Arduino, Sparkcore and PCduino on the Hover website (hoverlabs.com) and these can also be adapted to suit other devices fairly easily.

If you decide to create your own example with another device then why not submit a pull request to the Hover GitHub (github.com/jonesdb91)? If you are happy to share!
