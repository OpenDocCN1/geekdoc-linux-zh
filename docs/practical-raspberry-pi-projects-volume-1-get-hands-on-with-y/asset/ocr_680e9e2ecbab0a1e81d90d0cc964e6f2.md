# RUN SCIENCE EXPERIMENTS ON THE EXPEYES KIT

![](bbox=[0.11, 0.1, 0.83, 0.38])

**Left:** The kit itself is highly portable and great for taking down to Jams and hackspaces

# **02 Open it up**

The ExpEYES kit contains everything you need to get underway, with over 50 documented experiments from the ExpEYES website. The only other item that may come in handy is a breadboard. You will also need a Raspberry Pi or other computer with a USB port in order to run the digital oscilloscope software and connect to ExpEYES.

![](bbox=[0.11, 0.53, 0.44, 0.67])

# **03 What’s inside?**

As you may have guessed, the ExpEYES kit includes the main ExpEYES USB digital oscilloscope, but it also contains a wide range of other hardware including a DC motor, magnets, LEDs, coils, piezoelectric discs, wiring, a small screwdriver for opening the screw terminals and more. You also get a live CD which contains all the ExpEYES software and documentation ready to go on a bootable disc.

# **04 What can it do?**

The chip at the heart of ExpEYES is an AVR ATmega16 MCU (microcontroller unit), running at 8 MHz coupled to a USB interface IC (FT232RUL). These are low-cost but provide good value for money. As we have already mentioned, ExpEYES is therefore capable of acting as a four-channel oscilloscope but also has a built-in signal generator, 12-bit analog resolution, microsecond timing, resolution and a 250 kHz sampling frequency. At this price point, that’s an impressive set of features and certainly accurate enough for anything that is not mission critical (like learning, hobby projects, quick readings and so on).

# It pays dividends to make sure that your operating system is updated to the latest stable version, as this can save you a lot of hassle

![](bbox=[0.48, 0.535, 0.78, 0.645])

# **05 Using the live CD**

Perhaps the easiest way to get up and running with ExpEYES (if you have a computer with a CD drive) is to use the live CD which is included in the ExpEYES kit. Making sure that you are booting into the live CD from your BIOS boot menu, you should then be greeted with a Linux-based desktop. Plug in your ExpEYES by USB and you can open the software from the menu by going to Applications/Terminal/ExpEYES-Junior. Alternatively, you can run it from a terminal window using:

```
sudo python /usr/share/expeyes/expeyes-junior/croplus.py
```

# **06 Update your Raspberry Pi**

As with almost every project you undertake on the Raspberry Pi, it pays dividends to make sure that your operating system is updated to the latest stable version, as this can save you a lot of hassle further down the line. To do this, open an LXTerminal session and then type **sudo apt-get update**, followed by **sudo apt-get upgrade -y**, and then wait patiently for the upgrade process to complete.

# Other supported platforms

The ExpEYES software is mainly written in Python. This means that the core software to run your ExpEYES device is quite platform-agnostic – if the device can run a Python interpreter and has a Python module enabling it to access the serial port then it will work with ExpEYES. If you visit the ExpEYES website, there is a page that explains how to install the software on Linux and Windows – www.expeyes-info.expeyes-installation. In addition, there is a native Android app which will enable your ExpEYES to work with any Android device that has USB OTG on the go capability.