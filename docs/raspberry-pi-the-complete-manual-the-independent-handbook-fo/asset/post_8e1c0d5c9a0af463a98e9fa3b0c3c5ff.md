
# Use graphical installations

## Update the system

Unfortunately, if you have an aversion to dropping into the command-line terminal, then you're going to be stuck at the first step. Before we install anything, we need to make sure that the Raspberry Pi is fully updated and any existing packages are upgraded. Simply enter the following into the LX Terminal.

```
sudo apt-get update
sudo apt-get upgrade
```

## Installing Synaptic

To install Synaptic, you first need to enter the LX Terminal and run the command below – don't forget to type 'Y' to any prompts asking you to accept the installation.

```
sudo apt-get install synaptic
```

## Running Synaptic – Part 1

In essence, that's all you need to do. Synaptic is now installed and ready to use. However, due to its complexity, there may be some bugs that need ironing out first, so it's best to follow these steps. To test if Synaptic is working okay, first enter the following command into the terminal.

```
gksudo synaptic
```

## Running Synaptic – Part 2

You should be now looking at the Synaptic program window, where you can scroll through the list of available programs and click on each to download and install. Now we need to test whether it will run from the LXDE menu. Click on the icon in the bottom left, then go to Preferences > Synaptic Package Manager.

## Running Synaptic – Part 3

Running Synaptic from the LXDE menu results in an error. Don't panic, however - all it's doing is asking for a password. Enter the following password into the box.

```
raspberry
```

This is the default Pi password so we're assuming you haven't changed it!

## Fixing Synaptic – Option 1

This will temporarily fix the issue, but to permanently resolve it, do one of the following. First, right-click the Synaptic icon in the menu and left-click Properties. In the Command text box, change the text to add the gksudo command. So instead of 'synaptic-pkexec', it will read:

```
gksudo synaptic-pkexec
```

## Fixing Synaptic – Option 2

The second, and best, option is to drop back into the terminal and alter the way in which the program is executed from the menu. All that's needed is to change line 8 to use gksudo, so that the gksudo command is again used instead of the plain synaptic-pkexec. From the terminal, type:

```
sudo nano /usr/share/applications/synaptic.desktop
Change Exec=synaptic-pkexec to Exec=gksudo synaptic-pkexec
```

## Synaptic fully working

After you've entered those changes, exit nano via Ctrl+X, followed by 'Y' to accept the changes, and then press Enter a couple of times to get back to the command prompt. You can now launch Synaptic from the menu or by entering the following command when you're in the terminal.

```
gksudo synaptic
```

![](img/f11b7dbb71886af07ef87126037ebe98_34_0.png)

## What you'll need...

- Prototyping equipment
- RPi.GPIO
- [https://pypi.python.org/pypi/RPi.GPIO](https://pypi.python.org/pypi/RPi.GPIO)

![](img/f11b7dbb71886af07ef87126037ebe98_35_0.png)

*Above: The Pi's GPIO port comprises 36 pins, used to connect it with all manner of electronic components/devices*

# GPIO port explained

Learn how to harness the power of the GPIO port on your Raspberry Pi. It's easier than you think...

The general-purpose input/output (GPIO) pins on your Raspberry Pi are often central to the success of the projects you'll find in this book. Without them you have no way of interfacing with the real world, be it to trigger lights, buttons or buzzers or read sensors.

GPIO pins aren't special to the Pi; they're actually a standard designed to help control input and output behaviour with all kinds of integrated circuits. Usually you'll find that any one GPIO pin has no particular use pre-defined and they tend to be turned off by default.

## Raspberry Pi GPIO

The GPIO pins on the Raspberry Pi can be controlled and triggered in many ways. You can use them from the terminal directly and through Bash scripts, or you can control them using specially designed modules for popular programming languages. Since Python is the official language of the Raspberry Pi, you'll find the GPIO module for Python gives you among the best control for inputs and outputs available. The library is called RPi.GPIO and is installed by default on all Raspberry Pis, but can otherwise be installed in exactly the same way you'd install any useful Python library. The project is hosted on SourceForge and can be found at [sourceforge.net/projects/raspberry-gpio-python](sourceforge.net/projects/raspberry-gpio-python). You'll also find useful links, information and examples of how to use and control the GPIO pins from within simple Python scripts. It helps to have a basic understanding of Python if you plan to use RPi.GPIO, so we'd recommend a basic introductory course like the one found at [www.codeacademy.com](www.codeacademy.com) or by reading the official Python documentation at [www.python.org/doc](www.python.org/doc).

There are 26 GPIO pins on the Raspberry Pi and you can use the vast majority of them in any way you want. There are a few pins that have special purposes, though, so we recommend you familiarise yourself with their layout. For example, the very top row of pins are designed to offer power to external devices like buttons and lights. Since an earth line (often called 'ground') is needed to safely create a circuit, you'll also find several ground pins located in the GPIO port.

## How to use GPIO pins

To exploit the power of the GPIO port you'll need a few essential components, the most important of which are jumper leads. Since the pins on the port are 'male', you'll need to purchase either 'female to male' or 'female to female' cables, depending on what hardware you intend to connect to your Pi. Assuming the device you're connecting to also has male connectors, 'female to female' jumper leads will do nicely, and often you'll be using a breadboard to prototype your circuits, in which case 'female to male' connectors are preferred. Cables and breadboards can be bought very cheaply from just about any online store that sells Raspberry Pi accessories and can usually be found in the 'prototyping' section of the store.

## Naming conventions

Once you're ready to connect your device, the next task is to find the right pin for the job. While it's true that all GPIO ports are multipurpose, some are more multipurpose than others! As we've already discovered, some pins are reserved for 5V, 3.3V and ground. Others also have special capabilities, but what's worse is that they can also be called different things. For example, GPIO 18 is also known as pin 12 and PGM_CLK. This particular pin (around halfway down the right side of the GPIO port) is capable of hardware pulse-width modulation (PWM), and is useful for controlling LED lights and motors among other things.

The pin-naming convention you use in your Python scripts can be set manually. This can either be set as BCM (the Broadcom pin name) or the physical pin locations (BOARD).

You'll see in any of the projects where we're using the GPIO port, the following line with either BCM or BOARD in the brackets:

```
GPIO.setmode(GPIO.BCM)
```

The easiest way to deal with the GPIO pin-naming issues is to pick a convention and stick with it!

![](img/f11b7dbb71886af07ef87126037ebe98_36_0.png)

*Below: Become familiar with the layout of the GPIO pins and what they do - some have special purposes, such as ground pins*

> **Did you know...**
> The RPi.GPIO library has some really useful localisation allows, such as that we can set the "out" or "input".

# Top four add-on boards

Get more out of your Raspberry Pi by using these add-on boards to extend its functionality.

![](img/f11b7dbb71886af07ef87126037ebe98_37_0.png)

## Pi Supply Switch £15

The Raspberry Pi has been so popular, in part, because of the extremely good value for money of the hardware. It packs a lot of punch for the price point and, because it is designed by a charity, they don’t need to inflate the price with high profit margins (consider how much it would cost as a commercial product). Unfortunately, as with any low-cost item, some compromises had to be made in order to bring it in at such an affordable and small form factor.

When comparing it to your more standard desktop or laptop computer, two things that it is obviously lacking are a power switch and power management functionality. It is surprising how something as simple as a power switch can be so very useful, and it is not until you do not have one that you realise this!

The Pi Supply Switch is a self-solder kit which provides an on, off and soft-off (file-safe shutdown) button to give you basic power management functionality for your Pi. With some provided sample scripts you can make sure your Pi is correctly shut down when you switch off – without the need to open any menus or issue any commands in the terminal – and the circuitry in the switch ensures that power is only removed after the Pi has been shut down. As well as making it more convenient for you, it also reduces the possibility of corruption to your SD card from prematurely pulling the power cable.

## PiTFT Mini Kit £30

This is a 2.8-inch capacitive TFT LCD touchscreen that’s been specifically designed with the Raspberry Pi in mind by the project gurus over at Adafruit. It’s capable of slotting directly on top of the Raspberry Pi and is about as big as the Pi itself.

There are numerous reasons why you’d want to add such a screen to a Raspberry Pi but they all generally come down to the fact that the Pi is very small and very portable and most monitors are not. While you could remote connect via VNC from a phone if you’re on the go, the screen is connected directly to the Pi and doesn’t involve awkward wireless networking. Also as a touchscreen you don’t need to bring along other input devices, as it’s powered from the Raspberry Pi as well.

This opens it up to a world of possibilities. Portable computer, touchscreen control pad, video camera – anything that could benefit from your Raspberry Pi having a screen and human input while away from your main monitor.

![](img/f11b7dbb71886af07ef87126037ebe98_37_1.png)
