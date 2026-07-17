![](cover.jpeg)

![](images/00001.jpeg)

**Arduino Meets Linux: The User’s Guide to Arduino Yún Development**

Copyright © 2015 Bob Hammell.

EBooks are not transferable. All rights reserved. No part of this publication may be reproduced, distributed, or transmitted in any form or by any means, including photocopying, recording, or other electronic or mechanical methods, without the prior written permission of the publisher, except in the case of brief quotations embodied in critical reviews and certain other non-commercial uses permitted by copyright law.

Trademarked names, logos, and images may appear in this book. Rather than use a trademark symbol with every occurrence of a trademarked name, logo, or image, the names, logos, and images are used only in an editorial fashion and to the benefit of the trademark owner, with no intention of infringement of the trademark.

The information in this publication is provided by Bob Hammell on an “AS IS” basis. Bob Hammell makes no warranties, express or implied, regarding use of the information alone or in combination with your products. Neither the author nor the editors nor the publisher can accept any legal responsibility for any errors or omissions that may be made.

Published in the United States of America by Bob Hammell.

ISBN-10 (Print): 1-514-23022-4
ISBN-13 (Print): 978-1-514-23022-0
ISBN-13 (ePub): 978-1-329-19359-8

Any source code or supplementary materials referenced by the author in this text are available for readers at [www.arduinomeetslinux.com](http://www.arduinomeetslinux.com).

# Table of Contents

[Preface](#part0003_split_000.html_tpr1)

[Getting Started](#part0004_split_000.html_tc1) Features and connectors of the Arduino Yún • Connecting the Arduino Yún to a network • Changing your password • Opening the advanced configuration panel • Uploading sketches to the Arduino

[Introducing OpenWRT and Linux](#part0005_split_000.html_tc2) Connecting to the Arduino Yún and transferring files from another computer • Using the command prompt • Editing text files with GNU nano • Writing shell scripts • Installing Linux software • Resetting the operating system • Backing up the Arduino Yún

[Programming in Python](#part0006_split_000.html_tc3) Running Python scripts on the Yún • Writing your own Python functions • Working with classes and objects • Using packages and modules • Reading and writing to files • Handling the errors in scripts

[Using the Bridge Library](#part0007_split_000.html_tc4) Storing data in the AR9331’s memory from the ATmega32u4 • Running Linux commands and scripts • Working with files in the Linux file system • Using the Mailbox and sending messages • Communicating over local networks and the Internet

[Hosting Websites and Services](#part0008_split_000.html_tc5) Setting up a website on the Arduino Yún • Server-side scripting with CGI and Python • Project 1 – Building a web-based temperature monitor • Making web services and APIs • Project 2 – Controlling an LED matrix through a web API

[Project 3 – Making an MP3 Jukebox](#part0009_split_000.html_tp3) Connecting a parallel 16x2 LCD display to the Arduino Yún • Using a USB audio interface • Playing MP3 files from Python scripts

[Project 4 – Hosting a USB Game Controller](#part0010_split_000.html_tp4) How USB devices communicate • Using PyUSB to communicate with a USB device • Working with Microsoft Xbox 360®, Sony PlayStation®, and PC game controllers

[Project 5 – Making a USB Accelerometer Mouse](#part0011_split_000.html_tp5) Connecting to an accelerometer module • Using pin headers to fit a ProtoShield to an Arduino Yún • Using the Mouse class to turn the Yún into a USB mouse

[Project 6 – Making a Translating Keyboard](#part0012_split_000.html_tp6) Hosting a USB keyboard • Using Temboo and Microsoft Translator • Translating text from an Arduino sketch • Using the Keyboard class to turn the Yún into a USB keyboard • Reading the position of a rotary switch

[Project 7 – Controlling your Arduino Projects with Voice Commands](#part0013_split_000.html_tp7) Recording from a microphone • Translating speech to text with the AT&T Speech API • Responding to voice commands • Translating text to speech • Playing a .wav file

# Preface

The Arduino Yún is a very powerful and very flexible development board. It combines the best aspects of the Arduino platform – an easy-to-use integrated development environment (IDE), simple access to hardware pins, and a helpful community – with the power and customization options of a Linux-based computer.

To do this, the Arduino Yún includes both an ATmega32u4 microprocessor from the Atmel Corporation (as used in other Arduinos) and a 400 MHz, 32-bit MIPS central processing unit (CPU) from Atheros. The inclusion of the MIPS chip means that the Yún can perform tasks that other Arduinos do not have the speed or memory resources to do. And because the Yún runs the Linux operating system, you can use programming languages and software programs that you cannot run on other Arduinos.

The Yún gives you a choice:

*   You can use the Linux side of the Yún to add faster processing and more-capable networking to your ATmega32u4 projects – writing the main parts of your projects in Arduino sketches;
*   Or you can use the ATmega32u4 to add a friendly hardware interface to your Linux-based projects.

For Arduino users who do not have experience and knowledge of running Linux on embedded devices and programming in that environment, it can be difficult to learn how to make use of the extra power.

* * *

## What’s in this Book?

My aim in writing Arduino Meets Linux is to show you how you can use the full power of the Arduino Yún. The chapters and projects in this book guide you through:

*   Working with the Arduino Yún;
*   Using the Linux operating system; and
*   Developing projects that use both the ATmega32u4 and the Atheros AR9331 to create devices that are extremely difficult (or even impossible) to build using other Arduinos.

To program the ATmega32u4 on the Yún, you can use the Arduino IDE. This book introduces the libraries and functions that are specific to the Yún and that are built-in to the Arduino IDE. Every feature of the Yún is included, with sample code to help you learn to use these features.

To write programs and build projects on the Linux side of the Yún, you can use a variety of techniques and programming languages. Arduino Meets Linux concentrates on using the Linux command line and the Python scripting language. If you don’t have any experience of using Linux operating systems or programming in Python, don’t worry. You can find introductions to these subjects in the book.

Because the Yún is extremely capable at communicating over local networks and over the Internet, I have also included projects that demonstrate:

*   Hosting your own web sites and web services on the Yún;
*   Fetching information from third-party web services across the Internet; and
*   Using Temboo to simplify how you can access many web services.

I hope that you find these projects interesting. But remember, my hope is that you learn how to make use of the Arduino Yún and develop your own ideas. The techniques and explanations in my projects are intended to help you build your own. For that reason, I recommend that you read through all of the chapters in this book and build the projects. You can learn far more by making and experimenting than I can put into words.

* * *

## Who Should Read this Book?

If the Yún is your first Arduino, you should take some time to study the beginners’ tutorials at [http://www.arduino.cc](http://www.arduino.cc). If you ignore the Atheros AR9331, the Arduino Yún works almost identically to an Arduino Uno or Arduino Leonardo.

To an extent, Arduino Meets Linux assumes that the Yún is not your first Arduino. Although I have taken precautions to explain concepts that may be new to you, you should have a basic grasp of the fundamentals of building projects on the Arduino platform. This includes: writing sketches in Arduino C in the IDE; and safely building simple, electronic circuits.

If your main computer is a Windows PC or Apple Mac, and you have never used Linux before, then this book will help you. Everything you need to know is included. And the skills that you learn working with Linux on the Arduino Yún will help you if you ever want to use a Linux operating system on another development board or computer.

Arduino Meets Linux is for Arduino users who want to expand their skill set and learn to take advantage of the extra power and resources that only the Arduino Yún has.

* * *

## Online Resources

*ArduinoMeetsLinux.com* is the companion website for this book. You can contact me there if there’s anything I can help you with, or if you want to let me know about the great things you build with the Arduino Yún. I’ve also put all of the project sketches and scripts up there for you to download. It’ll be worth your while to visit the site regularly – news, updates, and addendum to this book will be posted there first.

To the best of my ability, I have verified the accuracy of all of the information in this book. And I have tried to ensure that the code samples are robust enough for you to use, but not so full of optimized programming and error-checking that it is difficult to understand the code. However, things do change and mistakes do happen. You can help me to improve future editions, for the benefit of other Arduino fans, by contacting me at *ArduinoMeetsLinux.com* if you find any errors, inaccuracies, or places where information is not as easy to understand as you would have liked.

* * *

## Conventions Used in this Book

The following table describes the text conventions used in this book.

| Convention | Meaning |
| --- | --- |
| *Italic* | Text that appears in italics refers to file names, variable and function names, or other code that exists in the project sketch, Python scripts, or Arduino libraries. Within the context of giving instruction, italic text should be typed exactly as shown. |
| **Bold** | Within the context of giving instruction, items in bold text are user interface elements, such as key strokes, menu items, or button labels. In other contexts, words may be emboldened for emphasis. |
| Monospace font | A monospace font is used for Arduino C, Python, and Linux command line code that you may need to type. |
| Colored text | Items shown with colored text are links to other pages in this book. |

# Getting Started

The Arduino Yún is a microcontroller-based development board that combines the flexibility and ease-of-use of the Arduino with a powerful MIPS[1](#part0004_split_006.html_fn1) central processing unit (CPU). It is two computers on one, small board.

The “Arduino side” is powered by an ATmega32u4 – the same chip that is on the Arduino Leonardo – and this is similar to the microcontrollers you have worked with before if you are an Arduino user.

The other processor is an Atheros AR9331\. This is a system-on-chip (SoC) comprising a MIPS-compatible central processor, internal memory, and built-in support for universal serial bus (USB) and networking over Ethernet and Wi-Fi. The AR9331 is capable of running GNU/Linux and is often used in routers and network devices running the OpenWRT Linux distribution. In this book, the combination of the AR9331 SoC and OpenWRT Linux are referred to as the “Linux side”.

The two sides of the Yún can communicate with each other, and you use can both in your projects at the same time.

In This Chapter

[Examining the Yún](#part0004_split_000.html_tc1s1)

[Updating OpenWRT](#part0004_split_002.html_tc1s2)

[Connecting the Arduino Yún to a Network](#part0004_split_001.html_tc1s3)

[Changing the Superuser Password](#part0004_split_003.html_tc1s4)

[Opening the Advanced Configuration Panel](#part0004_split_004.html_tc1s5)

[Uploading Sketches to the Arduino](#part0004_split_005.html_tc1s6)

* * *

## Examining the Yún

The various features of the Yún are divided between the Arduino side and the Linux side.

| Arduino side | Linux side |
| --- | --- |
| 20 digital input/output pins 12 analog input pins 7 pulse width modulation (PWM) output pins | microSD card reader Ethernet (10/100 Mb/s) Wi-Fi (802.11b/g/n) |
| 32 KB Flash memory 2.5 KB internal SRAM 1 KB internal EEPROM | 16 MB Flash memory 64 MB DDR2 RAM |
| 16 MHz crystal oscillator | 400 MHz crystal oscillator |
| USB controller (for uploading your sketches and communicating with a host PC). | USB controller for peripheral devices such as keyboards, gamepads, and audio interfaces. |
| Program with sketches from the Arduino IDE. | Program with Linux executables, Python, shell scripts, or languages that you install. |

The Arduino Yún has a similar layout to other Arduino devices, and it is approximately the same size. The placement of the input/output pins and in-circuit serial programming (ICSP) header are the same across the Arduino range, and so you can use most shields with the Yún. However, the vertically-mounted USB socket can make it difficult to use some shields. You can use an additional set of pin headers to fix this. For an example, see [Project 5 – Making a USB Accelerometer Mouse](#part0011_split_000.html_tp5).

![](images/00002.jpeg) 

Figure 1\. Connectors on the Yún

|  | Description |
| --- | --- |
| 1 | Digital input/output pins. |
| 2 | RJ45 socket for network connections over Ethernet. |
| 3 | micro-USB socket for power and communication with a host PC. |
| 4 | USB socket for peripheral devices. |
| 5 | Power input/output pins. |
| 6 | Analog input pins. |
| 7 | microSD card socket (underside). |
| 8 | ICSP header. |

Seven light-emitting diodes (LEDs) show the status of the board:

| LED Label | Description |
| --- | --- |
| RX | Flashes when the serial port receives data. |
| TX | Flashes when the serial port sends (transmits) data. |
| L13 | Digital output pin 13 links to this LED. When pin 13 is HIGH, the LED lights. When pin 13 is LOW, the LED is off. |
| WAN | Shows the status of the Ethernet connection. |
| ON | Glows green when power is applied and the Yún is on. |
| WLAN | Shows the status of the Wi-Fi connection. |
| USB | Glows white when the Yún connects to a computer over USB. |

And there are three different reset buttons on the Yún:

| Button | Description |
| --- | --- |
| 32U4 RST | Resets the ATmega32u4\. This is the equivalent of the RESET button on other Arduinos. To restart the Arduino sketch, press this button *twice*. |
| WLAN RST | Resets the Wi-Fi configuration. For more information, see [Resetting the Wi-Fi Connection](#part0004_split_002.html_tc1s3s4). |
| YÚN RST | Resets the Atheros A9331 and restarts Linux. |

### Connecting Power

Unlike many of the other Arduinos, the Arduino Yún’s power connector is a micro-USB socket.

To power the Yún from the USB socket of a desktop PC or laptop, you need a USB to micro-USB “data” cable:

1.  Gently, but firmly, push the micro-USB end of the cable into the micro-USB socket on the Arduino Yún.
2.  Push the full-size USB end of the cable into a USB 2.0 or USB 3.0 socket on your PC.

The first time that you connect your Arduino to an Apple Mac, Mac OS X may start the Keyboard Setup Assistant. You can close this window. The Arduino Yún’s USB controller creates a USB keyboard on your system. For more information, see [Project 6 – Making a Translating Keyboard](#part0012_split_000.html_tp6).

Once connected to your internal network, you can upload files and Arduino sketches to the Yún over the Ethernet or Wi-Fi connection. You do not need to cable the Yún to a PC to upload sketches to the board. For more information, see [Uploading Sketches to the Arduino](#part0004_split_005.html_tc1s6).

Many cellphones use a micro-USB socket for data transfer and charging. You can often use the charger from smartphones or tablets to power the Yún, but you should check that the power output of the charger matches the Arduino’s requirements. The Yún requires a 5 V power supply and this should be rated for at least 1 amp (1 A).

To the power the Yún from a cellphone charger:

1.  Gently, but firmly, push the micro-USB end of the cable into the micro-USB socket on the Arduino Yún.
2.  Plug the charger into a wall outlet.

You can also power the Arduino using the *Vin* pin on the lower row of headers. If you do this, you must only use a 5 V regulated supply as there is no on-board regulation or protection when power is applied this way.

Tip: The Linux side of the Yún takes longer to start than other Arduinos. It may take several moments for the operating system to load, connect to a network, and run any scripts that you have setup.

To turn off the Yún, unplug it from its power source. Unlike many other Linux devices, the version of OpenWRT Linux that runs on the Yún does not need to go through a specific shutdown procedure.

### Connecting USB Devices

The micro-USB socket on the Yún should only be used for powering the Arduino or for making a connection with a host PC.

To connect a USB peripheral (such as a mouse, keyboard, Bluetooth dongle, audio device, and so on) to the Linux SoC:

*   Plug the device (or its cable) into the full-size USB socket on the Arduino Yún.

It is usually fine to remove a USB device while the Yún is switched on.

If a USB device does not work properly when connected to the Arduino, test the device on a PC or Mac. If the device works correctly then the problem may be one of the following:

*   The device requires “driver” software that is not installed on the Yún;
*   The Yún’s power supply is not adequate to power the Yún and the device(s) that you are connecting. Either use a better power supply, or try connecting the USB device through a USB hub that has its own power supply.

### Inserting and Removing microSD Cards

The microSD socket on the Arduino Yún is on the underside of the board, behind the LEDs. The Yún supports only microSD and microSDHC cards (in capacities up to 32 GB); you cannot use microSDXC cards.

The socket on the Arduino is not spring-loaded – it will not click when you insert a card. Be aware that the microSD card sticks out from the Yún by roughly 1 cm – do not attempt to force it past this point.

To insert a microSD card:

1.  If possible, turn the Arduino Yún off.
2.  Hold the Yún upside down so that you are looking at the underside of the board.
3.  Hold the microSD facing up so that you are looking at the writing.
4.  Gently, but firmly, push the microSD card into the microSD socket.

![](images/00003.jpeg) 

Figure 2\. Inserting a microSD card (view from above)

The SD card is accessible on the Linux side as */mnt/sda1/* and through the *FileIO* class in the *Bridge* library. For more information, see [Using the Bridge Library](#part0007_split_000.html_tc4).

To remove the microSD card: turn the Arduino Yún off (or make sure that it is not reading or writing to the card) and then pull the microSD card out from the microSD socket.

Tip: Although you can save files to the built-in memory of the AR9331, you should try to use the microSD card to store your information. The AR9331 is limited in the number of times that it can overwrite the contents of its memory. Although this limit is very high, once it is reached then the AR9331 may become unusable.

* * *

## Connecting the Arduino Yún to a Network

On the Arduino Yún, Internet and network connectivity is controlled from the Linux side. The Atheros AR9331 has built-in support for making network connections over Ethernet or Wi-Fi.

Use whichever type of connection is most convenient for you. Ethernet is generally more reliable and easier to setup, but Wi-Fi is often more convenient because you do not need to run a cable from the Arduino to your network router.

### Installing Support for the Yún on PCs

After you connect your Yún to your local network, you can access it from any other device on the same network. To do this, use the host name *arduino.local* or its IP address.

The Yún broadcasts its host name using the multicast domain name system (mDNS), which helps devices on a network find each other without using a name server. Many devices and operating systems have built-in support for mDNS; but Windows does not. If you use Windows then, without additional software, you are unable to access the Arduino Yún using its host name. However, you can always use its IP address.

If you run Apple iTunes on your computer then you already have the necessary software to find your Yún. Apple’s support for mDNS is part of its *Bonjour* package. If you want to install Bonjour without installing iTunes, you can download it from [http://support.apple.com/kb/DL999](http://support.apple.com/kb/DL999).

To use Bonjour, your computer must be able to communicate with other devices on your network over UDP port 5353\. It is rare for network routers to block this port, but you should check this on your system. You should also ensure that the software firewall on your PC allows both incoming and outgoing connections on UDP port 5353.

You only have to install the Arduino IDE on computers that you want to use to create and upload Arduino sketches to the Yún. The Arduino software expects to find the Yún either through a USB cable or using its mDNS host name. If you want to upload sketches to the Arduino Yún, make sure you have enable or installed support for mDNS.

### Connecting to a Network over Wi-Fi

The process for connecting the Arduino Yún to your network is a little different than on many Linux-based devices.

If you have not yet setup a network connection then the Yún creates a new wireless access point when it starts. To tell the Yún how to connect to your network, you need to connect to this access point and enter the Arduino Yún web panel.

![](images/00004.jpeg) 

Figure 3\. Configuring the Yún from the web panel

To do this:

1.  Connect the Yún to a suitable power source and turn it on.
2.  On a PC or Mac, or a smartphone/tablet, open your wireless connection settings.
3.  Scan for wireless access points and connect to the network named *Arduino Yun-XXXXXXXXXXXX*.
4.  Start a web browser and open the webpage *http://arduino.local*
5.  In the **PASSWORD** box, type *arduino*.
6.  Click **LOG IN**.
7.  Click **CONFIGURE**.
8.  Under **WIRELESS PARAMETERS**, if the **CONFIGURE A WIRELESS NETWORK** box is not checked then click it.
9.  In the **DETECTED WIRELESS NETWORKS** list, click the name of your Wi-Fi connection.
10.  In the **SECURITY** list, click the type of security that your router uses.
11.  In the **PASSWORD** box, type the password for your router’s wireless access.
12.  Click **CONFIGURE & RESTART**.

It can take several moments for the Arduino to restart and connect to your Wi-Fi network. When it does, the wireless access point is turned off. Reconnect the device that you used to access the Arduino’s web panel to your Wi-Fi network, and then re-open the web panel.

If you want to use a static IP address for your Arduino Yún, see [Using a Static IP Address](#part0004_split_005.html_tc1s5s1).

### Resetting the Wi-Fi Connection

If you need to change the wireless network that the Arduino connects to, you can change the Wi-Fi configuration using the web panel at *http://arduino.local*

However, if the Yún cannot connect to your network then you will be unable to access the web panel. To fix this, you can reset the Wi-Fi configuration so that the Arduino creates a wireless access point instead of connecting to your router.

To reset the Wi-Fi connection:

1.  Press and hold the **WLAN RST** button for 5–20 seconds.
2.  Wait for the Yún to reboot and then follow the instructions in [Connecting the Arduino Yún to a Network](#part0004_split_001.html_tc1s3).

If you hold the wireless reset button for longer than 30 seconds then this restores the Arduino Yún back to the initial settings that it came with. This wipes any data (including network settings, downloaded files, and installed packages) from your Yún.

### Connecting to a Network over Ethernet

To connect the Yún to a router:

1.  Plug one end of a CAT5 or CAT6 Ethernet cable with RJ45 connectors into the socket on the Yún.
2.  Plug the other end of the cable into an available Ethernet port on your router.
3.  Plug the Arduino into a suitable power supply (if it is not connected already).

When the AR9331 chip powers up, it attempts to connect to the network using dynamic host configuration protocol (DHCP). In this mode, the Yún asks the router for an IP address and uses the gateway and domain name system (DNS) information that the router tells it.

If your router does not support DHCP, you can configure the Yún with a static IP address. You can find more information about using a static IP address in [Using a Static IP Address](#part0004_split_005.html_tc1s5s1).

The LED labelled “WAN” indicates the state of the Ethernet connection.

If you connect your Yún to your network using an Ethernet connection, the Wi-Fi connection remains as a wireless access point. This can allow other people to connect to your Arduino, access the administration panels, and take control of your device.

Caution: If you leave the Wi-Fi unconnected, change the Arduino’s password!

### Connecting to a Network using Both Wi-Fi and Ethernet

The Ethernet and Wi-Fi connections on the Arduino Yún are independent. You can use them to connect the Arduino to two different networks, or to the same network twice.

If you connect to two different networks at the same time, you may have problems specifying the routes that incoming and outgoing traffic takes.

There are two situations where you might want to connect your Arduino to the same network using both Wi-Fi and Ethernet:

*   You connect your Yún to your network using Ethernet, but do not want to leave the Wi-Fi connection open, change the Arduino’s password, or disable the Wi-Fi device;
*   You want to use two different IP addresses on the Yún. For example, two IP addresses are useful when hosting websites. For more information, see [Hosting Websites and Services](#part0008_split_000.html_tc5).

To connect to the same network using both Wi-Fi and Ethernet, follow the instructions for making each type of connection. If either (or both) connections use DHCP, then each connection has its own IP address. However, if you want to use static IP addresses for both connections, make sure that you specify two different IP addresses.

### Changing the Arduino’s Name

Whether you connect to a network using Ethernet or Wi-Fi, the Arduino appears on your network with the host name Arduino. If you have multiple Yúns on the same network then it is useful to change this so that each device appears with a unique host name.

Host names are usually up to 15 characters long, and should start with a letter (A–Z) or a number (0–9). The remaining characters can typically be anything except certain punctuation marks.

Changing the host name also changes the universal resource locator (URL) for the web panel. Instead of *http://arduino.local*, the web panel will be located at http://<newhostname>.local

To change the name:

1.  On a machine on the same network as the Arduino, open a web browser.
2.  In the address bar, type *http://arduino.local*
3.  Type the current password and then click **LOG IN**.
4.  Click **CONFIGURE**.
5.  Under **YÚN BOARD CONFIGURATION**, in the **YÚN NAME** box, type a new name for the Arduino.
6.  Click **CONFIGURE & RESTART**.

* * *

## Updating OpenWRT

OpenWrt-Yun is the Linux distribution that is installed on your Arduino. The makers of the Arduino Yún, Arduino LLC, change this software regularly to fix bugs and make improvements. The version that you have is likely out of date and you should update your Arduino to the latest version.

Updating OpenWrt-Yun wipes all of your settings and removes any additional software that you have installed on the Yún.

Sketches on the Arduino (especially ones that use the *Bridge* library) may interfere with the update process. You should upload the *YunSerialTerminal* example sketch before updating OpenWrt-Yun. For more information, see [Uploading Sketches to the Arduino](#part0004_split_005.html_tc1s6).

To update OpenWrt-Yun, you need to insert a microSD card into your PC or Mac, and then:

1.  Download the OpenWrt-Yun upgrade image from [http://arduino.cc/en/Main/Software](http://arduino.cc/en/Main/Software)
2.  If you are on Windows: find the *.zip* file you downloaded and right-click it. Point to **Open with** and then click **Windows Explorer**.
3.  If you are on Mac OS X: double-click the *.zip* file that you downloaded and it will unzip to a new folder[2](#part0004_split_006.html_fn2). In a **Finder** window, open the newly-unzipped folder.
4.  Copy the *.bin* file to the top-level (root) directory of the microSD card.
5.  Safely eject the microSD card from your PC or Mac.
6.  Insert the microSD card into the Arduino Yún. For more information, see [Inserting and Removing microSD Cards](#part0004_split_001.html_tc1s1s3).
7.  On a machine that connects to the same network as the Arduino, open a web browser. In the address bar, type *http://arduino.local*
8.  In the **PASSWORD** box, type *arduino* and then click **LOG IN**.
9.  Scroll to the bottom of the webpage.
10.  Click **RESET**.

![](images/00005.jpeg) 

Figure 4\. Updating OpenWRT from the web panel

The reset process may take several minutes and the LED labelled “WLAN” will blink. When it is complete, OpenWrt-Yun will be up-to-date and you can reconfigure the Yún’s network connection.

* * *

## Changing the Superuser Password

The default password on Arduino Yúns is *arduino*.

If you connect your Arduino Yún to a network where it can receive incoming traffic from other users (or people across the Internet), then you should change the default password. Changing the password helps to stop unauthorized people from taking control of your Arduino and changing settings or files that you do not want them to.

To change the password:

1.  On a machine on the same network as the Arduino, open a web browser.
2.  In the address bar, type *http://arduino.local*
3.  Type the current password and then click **LOG IN**.
4.  Click **CONFIGURE**.
5.  In the **PASSWORD** box, type a new password.
6.  In the **CONFIRM PASSWORD** box, type the same password again.
7.  Click **CONFIGURE & RESTART**.

* * *

## Opening the Advanced Configuration Panel

The advanced configuration panel is another web-based interface that you can use to change settings on your Arduino Yún. It is more complicated than the Arduino web panel, and has options to control many settings in the Linux operating system that runs on the Atheros AR9331.

To access the advanced configuration panel:

1.  On a machine that connects to the same network as the Arduino, open a web browser.
2.  In the address bar, type *http://arduino.local*
3.  Type the current password and then click **LOG IN**.
4.  Click **CONFIGURE**.
5.  Click **advanced configuration panel (luci)**.

![](images/00006.jpeg) 

Figure 5\. The advanced configuration panel

The advanced configuration panel is divided into three main tabs:

| Tab | Description |
| --- | --- |
| Status | Shows information about the current status of the Yún, and contains options for the administration of running processes. |
| System | Options for configuring OpenWrt-Yun Linux on the Yún. |
| Network | Information and configuration options for the Yún’s network connections. |

Each of the main tabs is then split into several other tabs.

If you are unfamiliar with Linux-based operating systems, you should read [Introducing OpenWRT and Linux](#part0005_split_000.html_tc2) before changing settings in the advanced configuration panel.

### Using a Static IP Address

When the Yún restarts, or reconnects to the network, your network router will give it an IP address. You can use this address to communicate with the Yún, instead of the host name *arduino.local*. However, this IP address can change every time the Yún connects to the network. To prevent the IP address changing, you can use a *static IP*.

The network configuration options in the Arduino web panel are not detailed enough for you to use them to setup a static IP address. However, you can do this from the advanced configuration panel.

1.  Open the **advanced configuration panel**.
2.  Click the **Network** tab.
3.  Under **Interfaces**, next to either the **LAN** (Wi-Fi) or **WAN** (Ethernet) interfaces, click **Edit**.
4.  In the **Protocol** list, click **Static address**.
5.  Click **Switch protocol**.
6.  In the **IPv4 address** box, type the IP address that you want to use.
7.  In the **IPv4 netmask** box, type the subnet mask for your network.
8.  In the **IPv4 gateway** box, type the IP address of your router.
9.  In the **Use custom DNS servers** box, add the IP address of a DNS server that your network uses. If you need to add another, click the **+** button.
10.  Click **Save & Apply**.

If you are unsure what values to type in the IPv4 boxes, look at the network configuration properties of another machine on your network.

### Accessing the System Log

Linux saves important messages and errors into log files. You can view two of these from the advanced configuration panel: the system log, and the kernel log. You can often use these to see whether certain programs or configuration settings are working correctly, and whether scheduled tasks run.

To open the system log in the advanced configuration panel:

*   Click the **Status** tab, and then click the **System Log** tab.

To open the kernel log:

*   Click the **Status** tab, and then click the **Kernel Log** tab.

* * *

## Uploading Sketches to the Arduino

The Arduino integrated development environment (IDE) is a program for your PC or Mac. You can use it to write programs that run on the Arduino side of the Yún (and other Arduinos). Only IDE versions 1.5.8 BETA or later support the Arduino Yún. The current version of the Arduino IDE is 1.6.4.

If the Yún is your first Arduino, you need to install the Arduino IDE. If you are currently using other Arduinos, you should update to the latest version of the IDE.

### Installing Arduino 1.6.4

To install the latest version of the Arduino IDE:

1.  In a web browser, open the webpage [http://arduino.cc/en/Main/Software](http://arduino.cc/en/Main/Software)
2.  In the section **Arduino 1.6.4** download the file that matches the operating system that you are using.
    1.  On Windows: click **Windows Installer**, then click **JUST DOWNLOAD**. Save the file and then double-click it to run the installation process.
    2.  On Mac OS X: click **Mac OS X 10.7 Lion or newer** and then click **JUST DOWNLOAD**. Save the *.zip* file and then double-click to open it. Drag the *.app* file to your *Applications* folder.

### Connecting to the Yún from the Arduino IDE

When the Arduino Yún is on your network, you do not have to use a USB cable to connect it to the same machine that is running the Arduino IDE. Instead, you can upload sketches to the Arduino over Wi-Fi or Ethernet.

1.  Start the Arduino IDE.
2.  On the **Tools** menu, point to **Board**, and then click **Arduino Yún**.

If you connect a USB cable from the Yún to your PC or Mac:

*   On the **Tools** menu, point to **Port**, and then click **COM? (Arduino Yún)**.

Or, to upload sketches over the network connection:

*   On the **Tools** menu, point to **Port**, and then click **Arduino at <IP Address> (Arduino Yún)**.

To compile the current sketch and upload it to the Arduino using the selected port:

*   In the Arduino IDE, on the toolbar, click **Upload**.

Tip: If you cannot make the connection to your Yún, check that your firewall allows UDP connections on port 5353, and that you have installed support for Bonjour. For more information, see [Installing Support for the Yún on PCs](#part0004_split_002.html_tc1s3s3).

If you use the IDE to make a connection to the Arduino Yún over your network, you cannot send messages to the Serial Monitor using the *Serial* class. The routines in this class are designed to send and receive data over the USB serial port only. Instead, you should use the *Console* class in the Bridge library. For more information about the Console, see [Making a Console Connection](#part0007_split_004.html_tc4s5).

To keep the code samples in this book as easy to understand and work with as possible, many of them use the *Serial* class and the Arduino IDE’s Serial Monitor. While you are practicing, you may find it helpful to connect the Yún to your PC using a USB cable.

### Looking at the Example Sketches

The Arduino IDE installs example sketches that show how to use the features of the Arduino Yún. You can also use some of these sketches to help you work with the Yún and perform certain administration functions.

You can open the example sketches from the Files menu:

*   On the **Files** menu, point to **Examples**, and then point to **Bridge**.

For example, to open the *YunSerialTerminal* sketch and upload it to the Arduino:

1.  On the **Files** menu, point to **Examples**, point to **Bridge**, and then click **YunSerialTerminal**.
2.  On the toolbar, click **Upload**.

The table below highlights some of the example sketches and describes what they do.

| Sketch | Description |
| --- | --- |
| Bridge | Demonstrates use of the Bridge library. For more information about Bridge, see [Using the Bridge Library](#part0007_split_000.html_tc4). |
| FileWriteScript | Shows how to write files into the Linux file system from the Arduino side. |
| Process | Demonstrates how to start Linux processes and return the results to the Arduino. |
| ShellCommands | Examples of how to call Linux shell commands from an Arduino sketch. |
| Temboo | A collection of samples that demonstrate how to use the Temboo service to connect to other web-based resources. |
| WiFiStatus | Displays the status of the Wi-Fi connection in the Arduino IDE Serial Monitor. |
| YunSerialTerminal | Provides access to the Linux command shell from the Arduino IDE Serial Monitor. For more information, see [Introducing OpenWRT and Linux](#part0005_split_000.html_tc2). |

* * *

[1](#part0004_split_000.html_nf1)Microprocessor without Interlocked Pipeline Stages (MIPS) is a CPU architecture developed by MIPS Technologies, Inc.[2](#part0004_split_003.html_nf2)If you have installed an archiving tool on your Mac, the OpenWrt-Yun update image might open in this.

# Introducing OpenWRT and Linux

An operating system (OS) is a special type of program that you run on your computer. Its main jobs are to help you run multiple other programs at the same time, share system resources between those programs, and manage the file system (how files and programs are stored).

GNU/Linux (usually referred to as just *Linux*) is an open source OS. This means that the files that you need to build it are freely available, and so anyone can make their own Linux-based OS. A customized OS that is based on Linux is a *distribution*, or *distro*.

OpenWRT is a Linux distribution that is designed to run on devices that do not have the same speed or memory resources as full, desktop machines. It is aimed at standalone devices, such as network routers, to which you do not usually connect a display or keyboard.

The Arduino Yún is much more powerful than other Arduinos and so it is able to do things that other Arduinos cannot. For example, it can play an MP3 file through a USB audio device, while it is downloading files from the Internet and writing them to an SD card. By running an OS, the Yún simplifies how you can use this extra power. Without the OS, using all of the Yún’s features would be difficult – requiring long and detailed sketches that only experienced programmers would be able to write.

The Atheros AR9331 chip inside the Arduino Yún runs a version of OpenWRT Linux called OpenWrt-Yun. Unlike the Arduino side of the Yún (to which you upload sketches using the Arduino IDE), you work with OpenWrt-Yun using a command line. This involves typing commands and editing text files. And unlike operating systems, such as Windows and Mac OS X, OpenWrt-Yun does not have a desktop environment that you control with a mouse.

In This Chapter

[Connecting to the Arduino Yún](#part0005_split_000.html_tc2s1)

[Looking at the Command Prompt](#part0005_split_001.html_tc2s2)

[Editing Text Files with GNU nano](#part0005_split_002.html_tc2s3)

[Working with Environment and Shell Variables](#part0005_split_003.html_tc2s4)

[Writing Shell Scripts](#part0005_split_004.html_tc2s5)

[Expanding the Linux File System onto the microSD Card](#part0005_split_005.html_tc2s6)

[Installing Linux Packages](#part0005_split_006.html_tc2s7)

[Resetting OpenWrt-Yun](#part0005_split_007.html_tc2s8)

[Backing Up the Arduino Yún](#part0005_split_008.html_tc2s9)

* * *

## Connecting to the Arduino Yún

Since you do not usually connect a display and mouse to the Yún, on OpenWrt-Yun you use the command line to make changes to the Linux side, run scripts and programs, and install additional software.

You control the command line using a keyboard, by typing in the names of commands that you want to run. These commands are actually small programs that direct any messages and output to the console – the text-based display. The command line is also called the *shell*, or *terminal*.

![](images/00007.jpeg) 

Figure 6\. Typing a command into the Yún’s command line

Unlike other Linux-based computers, you need to make a connection to the Yún’s terminal from another machine on your network. Although you can do this using the *YunSerialTerminal* sketch and the Serial Monitor in the Arduino IDE, the Serial Monitor is quite basic. It is often better to connect to the Yún using the secure shell (SSH) protocol and a dedicated piece of software.

SSH is an encrypted protocol for executing commands remotely – from another machine on the same network as the Arduino – and accessing the command line. When connected, you can type commands using the keyboard on your computer, and then see the results.

The Yún has built-in support for SSH, but Windows users have to install an SSH client on their machine. These are pieces of software that understand how to work with SSH, and there are many different clients available. One of more popular ones is PuTTY, and you can download this from [http://www.chiark.greenend.org.uk/~sgtatham/putty/](http://www.chiark.greenend.org.uk/~sgtatham/putty/)

To connect to the Arduino’s terminal from Windows, using PuTTY:

1.  Locate the file *putty.exe* that you downloaded, and then double-click it.
2.  In the **Host Name (or IP address)** box, type the host name of the Yún. This is *arduino.local*, unless you have changed it.
3.  Under **Connection Type**, click **SSH**.
4.  Click **Open**.
5.  At the login prompt, type *root*.
6.  At the password prompt, type your password and then press **Enter**. This is *arduino* unless you have changed it.

Mac OS X already has an SSH client; you do not need to download a separate client to connect to your Arduino from a Mac.

To connect to the Arduino’s terminal from Mac OS X:

1.  On the dock, click **Finder**.
2.  On the sidebar, click **Applications**.
3.  Click **Utilities**, and then double-click **Terminal**.
4.  Type the following command, replacing *arduino* with the host name of your Yún, and then press **Enter**:

    ```
    ssh root@arduino.local
    ```

5.  At the password prompt, type your password. This is *arduino* unless you have changed it.

To close the connection, type *exit* and then press the Enter key.

### Transferring Files between the Arduino and a PC/Mac

The secure copy (SCP) protocol is closely-related to SSH. You can use it to download files from the Arduino to your PC or Mac, and to upload files from your computer to the Linux file system (or onto the microSD card) on the Yún.

Tip: If you regularly need to upload or download files from the Yún, use SCP. This way, you do not need to shut down the Yún and remove the microSD card.

On Windows, you need to download and install an SCP client, such as WinSCP ([http://winscp.net/eng/download.php](http://winscp.net/eng/download.php)).

Then to connect to the Arduino:

1.  Start WinSCP.
2.  In the left panel, click **New Site**.
3.  In the **File Protocol** list, click **SCP**.
4.  In the **Host name** box, type the name of your Arduino. This is *arduino.local* unless you have changed it.
5.  In the **User name** box, type *root*.
6.  In the **Password** box, type your Yún’s password. This is *arduino* unless you have changed it.
7.  Click **Save As…**
8.  In the **Site Name** box, type *Arduino Yún*.
9.  Click **OK**.
10.  Click **Login**.

To upload a file to the Arduino, drag it from a Windows Explorer window and drop it over the WinSCP window. To download a file from the Arduino, drag it from the WinSCP window and drop it in a convenient location on your PC.

![](images/00008.jpeg) 

Figure 7\. Connecting to the Arduino using WinSCP

Mac OS X has an *scp* command built-in. There are SCP clients available that have a graphical user interface (GUI) but if you do not want to install one of these then you can use SCP from the Mac OS X terminal.

To upload a file from Mac OS X:

1.  On the dock, click **Finder**.
2.  On the sidebar, click **Applications**.
3.  Click **Utilities**, and then double-click **Terminal**.
4.  Type the following command and then press **Enter**:

    ```
    scp /local/file/to/upload root@arduino.local:/destination/file
    ```

5.  At the password prompt, type your Yún’s password. This is *arduino* unless you have changed it.

To download a file from the Arduino to your Mac:

1.  On the dock, click *Finder*.
2.  On the sidebar, click **Applications**.
3.  Click **Utilities**, and then double-click **Terminal**.
4.  Type the following command and then press **Enter**:

    ```
    scp root@arduino.local:/remote/file/to/download /destination/on/Mac
    ```

5.  At the password prompt, type your Yún’s password. This is *arduino* unless you have changed it.

* * *

## Looking at the Command Prompt

When you connect to your Arduino over SSH and login, you see the command prompt. This is a short sequence of characters that ends with a # symbol. Whenever you see this prompt, you can type a command and then press the Enter key to make Linux run it.

The prompt consists of four parts:

1.  The first part shows the name of the user that you are logged in as (usually *root*).
2.  The second part shows the host name of the Arduino.
3.  The third part is the current working directory (for more information, see [Working with Files and Directories](#part0005_split_002.html_tc2s2s1)).
4.  The # symbol indicates that you are logged in as the root administrator. Non-administrator users see a different symbol.

To run a command, type it at the command prompt and then press the Enter key when you are done.

For example, you can use the *echo* command to display messages.

*   Type the following command and then press **Enter**:

    ```
    echo "Hello from Arduino!"
    ```

Values typed after the command name are called “arguments”. The *echo* command expects one argument, and that is the message to show. In this case, it does not matter if you do not use quotation marks. However, other commands think that spaces indicate gaps between arguments. By using quotation marks, you can ensure that the command treats your text as a single argument.

If you want to run the same command again, press the Up Arrow key and the previous command appears in the console. You can then make changes to the command. Press Enter to run the command or the Down Arrow key to return to a blank prompt.

After you have run several commands, you can use the Up and Down Arrow keys to cycle through your command history.

### Working with Files and Directories

In the Linux file system, it is acceptably true to say that everything is a file. This is because Linux maps things like input/output devices and information about processes that are running into the file system. Even directories are actually files.

Every user on a Linux system has their own home directory. This is an area of the file system where they have permission to create files and directories. On larger Linux systems, a user may not be able to access anything outside of their home directory.

When you login at the command prompt, Linux places you in a directory. On OpenWrt-Yun, you login as the *root* user and so Linux places you in the root user’s home directory – */root*. This is your *current working directory*. If you do not specify a full file path then Linux commands assume that you want to place or work with files in the current working directory.

To change the current working directory and move to the top-level of the file system,

*   Type the following command and then press **Enter**:

    ```
    cd /
    ```

To see a list of all the files and directories that are in the current working directory,

*   Type the following command and then press **Enter**:

    ```
    ls
    ```

In the top-level directory, there are a lot of subdirectories. Many of these have specific functions, and are generally the same across different distributions of Linux. On OpenWrt-Yun, the top-level subdirectories are:

| Directory | Description |
| --- | --- |
| bin | Contains applications that are used by all user accounts, the system, and the system administrator. |
| dev | Linux creates file system entries in this folder for hardware devices that are attached or built-in to the system. |
| etc | Mostly contains configuration files and settings for the OS and installed programs. |
| lib | Contains *libraries* – collections of code and information – that are shared among all applications. |
| lost+found | Files that are saved during failures are placed here. |
| mnt | Storage devices (such as SD cards) are added to the file system in here. |
| overlay | When the file system is expanded to include space on the microSD card, the files in this folder are included in the Linux file system. |
| proc | Contains information about system resources and processes that are currently running. This is a virtual file system entry – the files change depending on the current state of the operating system. |
| rom | When the file system is expanded to include space on the microSD card, this folder refers to the files that are in the Atheros AR9331’s built-in memory. |
| root | This is the home folder for the system administrator. |
| sbin | Contains applications that are only available to the system and the system administrator. |
| sys | This is a virtual directory for accessing information about the current state of the system. |
| tmp | Temporary files used by the system. The contents of this folder are deleted when the Yún starts. |
| usr | Contains files and documentation for all user applications. |
| var | Variables and temporary files that are created by the user or applications. |
| www | Files and scripts for the Arduino’s web panels and web-hosting capabilities. |

Linux creates entries in the */dev* and */mnt* folders for input/output devices, memory cards, and USB peripherals. Because “everything is a file”, you can often access external devices by using commands that are designed to work with files. In those cases, writing to the “file” actually sends the information to the device.

When creating your own files, try to keep them on the microSD card. This is especially important if you do not expand the Linux file system to the memory card (see [Expanding the Linux File System onto the microSD Card](#part0005_split_005.html_tc2s6)) as the Atheros AR9331 can only write to its built-in storage a set number of times.

Tip: If you do expand the file system onto the memory card, the best place to keep your files is in */root*.

To change the current working directory to a subdirectory,

*   Use the *cd* command followed by the name of the directory. For example, type the following command and then press **Enter**:

    ```
    cd etc
    ```

*   Use the *cd* command followed by the full path to the directory. For example, wherever you are in the file system, you can always jump to the SD card by typing the following command and then pressing **Enter**:

    ```
    cd /mnt/sda1/
    ```

When you are in a subdirectory, to move to the parent directory,

*   Type the following command and then press **Enter**:

    ```
    cd ..
    ```

### Managing Files and Directories

On a typical Linux-based operating system, file and directory names are case-sensitive. This means that *file.txt*and *File.txt* are two separate files. This is different from operating systems such as Microsoft Windows, which is case-insensitive.

File names can be up to 255 characters, and usually include a file extension after a dot. The file extension indicates what type of file it is. But you do not have to use the same file extensions as everyone else if you do not want to, and in most cases you do not have to use a file extension at all.

A file path describes the location of a file. There are two types:

Relative file paths

Describe the location of a file relative to the current working directory. For example *../../test.txt* specifies that the file *test.txt* can be found two directories up (in the parent directory of the parent directory of the current working directory).

Absolute (or root-relative) file paths

Describe the location of a file relative to the top-level directory. These begin with a forward slash. For example, */mnt/sda1/test.txt* specifies that the file test.txt is found by moving to the top-level, then into the *mnt* directory, then into the *sda1* directory.

Whenever you need to type a file name, you can also include either type of file path.

There are lots of commands that you can use to create, edit, and remove files or directories:

| To | Do This |
| --- | --- |
| Move to your home directory | Type the following command and then press **Enter**: 
```
cd ~
```

 |
| List the contents of a specific directory | Type *ls* followed by a space and then the name of the directory. Then press **Enter**. |
| Create a directory | Type *mkdir* followed by a space and then the name of the directory, and then press **Enter**. |
| Delete a directory | Type *rmdir* followed by a space and then the name of the directory, and then press **Enter**. |
| Delete a file | Type *rm* followed by a space and then the name of the file, and then press **Enter**. |
| Copy a file or directory | Type *cp* followed by a space and then the name (or full file path) of the file to be copied. Type another space and then the name (or full file path) to call the copy. Press **Enter**. |
| Rename or move a file or directory | Type *mv* followed by a space and then the name (or full file path) of the file to be copied. Type another space and then the name (or full file path) to specify the destination. Press **Enter**. |
| Show the full path of the current working directory | Type *pwd* and then press **Enter**. |
| View a text file | Type *cat* followed by a space and then the name of the file. Then press **Enter**. |
| Edit a text file | Type *nano* followed by a space and then the name of the file. Then press **Enter**. For more information, see [Editing Text Files with GNU nano](#part0005_split_002.html_tc2s3). |

### Redirecting the Output of a Command

Linux commands usually send their output, messages, or errors, to the standard output device. This is normally the console window.

You can redirect the output of a Linux command to device or file by using *pipes*.

For example, to redirect the output of the *ls* command so that the list of files is placed in a text file instead of appearing in the console,

*   Type the following command and then press **Enter**:

    ```
    ls / >/mnt/sda1/files.txt
    ```

Every time you direct output to a file, the file is wiped first. To append content to the end of an existing file, use *>>*. For example,

1.  Type the following command and then press **Enter**:

    ```
    echo "Files in the top-level directory:" >/mnt/sda1/files.txt
    ```

2.  Type the following command and then press **Enter**:

    ```
    ls / >>/mnt/sda1/files.txt
    ```

### Creating and Removing Symbolic Links

Links are special types of file. They do not contain content, but instead they point to another entry in the file system that does contain content.

Create links with the *ln* command followed by *-s*, then the full path of the item that you want to link to, then the file name and file path where you want to save the link. For example, you can use a link to create an entry in your home directory that points to the SD card.

1.  Type the following command and then press **Enter**:

    ```
    cd ~
    ```

2.  Type the following command and then press **Enter**:

    ```
    ln -s /mnt/sda1/ sd
    ```

3.  Type the following command and then press **Enter**:

    ```
    ls
    ```

In the */root* directory (your home directory) you can see an entry named *sd*. If you list the contents of this (*ls ~/sd*) then you actually get a list of the files on the microSD card.

You can also create links to files in the same way.

Deleting a symbolic link does not remove the original file. So, to remove the symbolic link that you just created,

*   Type the following command and then press **Enter**:

    ```
    rm ~/sd
    ```

One of the uses for symbolic links on Linux is in the */lib* directory. If you list the contents of this directory then you will see that some files have their version numbers (or build numbers) in the file name. For those that do, there is usually a matching file that does not have a version number. This is often a link.

By having a link with name that never changes, it means that the actual file can be updated to a new version without affecting any program that wants to use the file.

### Setting the Access Permissions of Files and Directories

As the root user you will rarely be concerned with the access permissions of files and directories – you always have access to the full system. However, if you create a project where multiple users access Linux then this information can help you to keep the system secure.

Access permissions tell Linux which users can access specific files and directories, and what they can do with them. But because of the way OpenWrt-Yun builds the file system, there are lots of restrictions on the file access permissions that you can change.

For example, if you need to create a directory that everyone can access then the best place to do this is in */root*or */www*. You have full control of the file permissions in those directories.

Each file and directory in a Linux system has three sets of permissions:

| Set | Description |
| --- | --- |
| Owner | Permissions that apply only to the owner of the file – usually the person who created it. You can change the owner of a file using the *chown* command. |
| Group | Permissions that apply to a defined group of users. You can change the group of a file or directory with the *chgrp* command. |
| All | Permissions that apply to everyone who has a login for the system. |

In each set, there are three different types of permission that you can give to users:

| Permission | Description |
| --- | --- |
| Read | The user can read or open a file or directory. |
| Write | The user can write or change information in a file or directory. |
| Execute | The user can execute scripts or binary programs. |

You can view the permissions that are set for a file or directory by using the *ls* command with the *-l* flag. For example,

*   Type the following command and then press **Enter**:

    ```
    ls -l
    ```

The sequence of characters on the left of the console describes the access permissions. This is in a special format. For example, drwxr-xr-x.

The first character is a special permissions flag:

| Flag | Description |
| --- | --- |
| _ | No special permissions. |
| d | The entry is a directory. |
| l | The entry is a symbolic link. |
| s | The entry has permissions set by *setuid* or *setgid*. These permissions are for advanced users and are not covered in this book. |
| t | The entry has sticky permissions. These permissions are for advanced users. |

The next three characters show the permissions for the owner of the file or directory. An *r* indicates that the owner can read from the file, a *w* indicates that they can write to it, and an *x* indicates that they can execute the file. If a permission type is not set, a *-* is used instead.

Following the owner permissions, there are three characters that show the permissions for groups. And then three characters that show the permissions for all other users.

After the sequence of characters representing the permissions, in the output of *ls -l* there is a number[1](#part0005_split_009.html_fn1) and then two words. These two words show the owner of the file and then the group that it belongs to. For a user to obtain the group access permissions, you must first assign a user to that group.

Tip: OpenWrt-Yun lacks many of the commands used to deal with users and groups. You can work around this, but these kinds of security measures are less important on the Arduino than on other Linux-based operating systems.

To give permissions to the owner, use the *chmod* command followed by *u+*, and then: an *r* to give read permission, *w* to give write permission, and *x* to give execute permission.

For example:

```
chmod u+rwx test.txt
chmod u+rw- test.txt
chmod u+r-w test.txt
```

To remove permissions, use the *chmod* command followed by *u-*, and then: an *r* to remove the read permission, *w* to remove write permission, or *x* to remove execute permission.

For example:

```
chmod u-rwx test.txt
chmod u--wx test.txt
chmod u-r-x test.txt
```

To change the permissions for the group, replace *u+* or *u-* with *g+* or *g-*.

To change permissions for all other users, replace *u+* or *u-* with *a+* or *a-*.

You can also change all three sets of permissions with one command. In this case, you do not use the permission format explained above. Instead, you use a three-digit number.

The first digit sets the permission for the owner. A zero means no access. *r* has the value 4, *w* has the value 2, and *x* has the value 1\. So to give the owner all three permission types, add all three values together. The digit you use in the *chmod* command is 7 (4+2+1). To only give read and execute permissions, use the digit 5 (4+1).

The second digit sets the permissions for the group. And the third is for all other users.

For example, to change the permissions of *test.sh* so that only the owner can modify it (but everyone else can read and execute it),

*   Type the following command and then press **Enter**:

    ```
    chmod 755 test.sh
    ```

* * *

## Editing Text Files with GNU nano

When you need to write a shell script, Python program, or edit a configuration file, you will work with text files. In most cases, you could transfer the file to your PC or Mac and use the editing tools that you have on your main machine. However, there is also a built-in text editor available from the Linux command line.

GNU nano is a small, but useful, text editor for Linux. It is very popular and is included in many Linux distributions, including OpenWrt-Yun.

To start a new text file in nano,

*   At the command line, type the following command and then press **Enter**:

    ```
    nano
    ```

To edit an existing file, specify the file path and file name after the *nano* command,

*   At the command line, type the following command and then press **Enter**:

    ```
    nano /www/index.html
    ```

To exit nano:

*   Press **Ctrl + X**.

If you have made changes to the file, nano asks you whether you want to save the file. Press the N key if you do not. If you do, press the Y key and then type (or change) the file name. Press the Enter key when you are done.

### Using nano

To move the text cursor, press one of the arrow keys on your keyboard.

Hold the Ctrl key while pressing another key to activate a special function. Some of these are shown with a ^ symbol at the bottom of the nano editor. For example, ^K is the same as Ctrl + K. You can also activate these functions by pressing the Esc key twice and then typing the letter. For example: Esc, Esc, K.

In nano, the Alt key is also known as the “meta” key. The meta key is another way of activating certain functions. For example, to move to the first line in a text file:

*   Press **Alt + |**

However, if you connect to the Yún over SSH, you may find that the Alt key does not work. Instead, you can use the Esc key. Press the Esc key once (release it), and then type the | symbol.

| To | Do This |
| --- | --- |
| Move to the first line in a file | Press **Alt + &#124;** or press **Esc** and then press **&#124;**. |
| Move to the last line in a file | Press **Alt + ?** or press **Esc** and then press **?**. |
| Move to a specific line number | Press **Ctrl + _** (underscore), type the line number and then press **Enter**. |
| Move to a specific character position on a specific line | Press **Ctrl + _** (underscore), type the line number, followed by a comma, then the character position number. Then press **Enter**. |
| Move to the end of the current line | Press **Ctrl + E**. |
| Delete a line | Press **Ctrl + K**. |
| Delete multiple lines | Press **Ctrl + K** repeatedly without making any other edits to the document. |
| Undelete the last line (or multiple lines) that you deleted | Press **Ctrl + U**. |
| Move a line | Press **Ctrl + K**. Move the text cursor and then press **Ctrl + U**. |
| Copy and paste a line | Press **Alt + 6**, or press **Esc** and then press **6**. Move the text cursor and then press **Ctrl + U**. |
| Search the file for a specific word | Press **Ctrl + W**, type the term that you want to search for, and then press **Enter**. |
| Replace all instances of a specific word with another | Press **Ctrl + W**, and then press **Ctrl + R**. Type the term that you want replace and then press **Enter**. Type the term that you want insert, and then press **Enter**. |
| Insert the contents of another file into the current text file | Press **Ctrl + R**, type the file path and file name of the text file that you want to insert, and then press **Enter**. |
| Save the file | Press **Ctrl + O**. Then type (or change) the file name and press **Enter**. |
| Exit nano | Press **Ctrl + X**. |

* * *

## Working with Environment and Shell Variables

On Linux, variables are one way of passing information between programs. Many Linux programs expect key pieces of information to be contained in predefined variable names.

There are two types of variable on Linux:

Environment variables

Created by various scripts and configuration files that run when Linux starts up. Environment variables are accessible from the command line that creates them, and any other scripts or programs that you start from this command line.

Shell variables

Only accessible from the current command line; not to any scripts or programs that you start from this command line.

One of the most important environment variables on Linux is *PATH*. When you type a command on the command line and press the Enter key, the system searches all of the directories that are named in the *PATH* variable and tries to find the command or program.

To display a variable, use the *echo* command and prefix the variable name with a $,

*   Type the following command and then press **Enter**:

    ```
    echo $PATH
    ```

To set an environment variable,

*   Type the following command and then press **Enter**:

    ```
    export VARIABLENAME=value
    ```

To set a shell variable,

*   Type the following command and then press **Enter**:

    ```
    VARIABLENAME=value
    ```

You do not have to use capital letters for variable names, but it is common to do so when setting environment variables. To change a variable of either type, use the same syntax as when setting a shell variable.

When you connect to the Yún using SSH, Linux starts a new command line (*shell*) that sends its output and receives its input over the Yún’s network connection. The shell itself is a program, and so you can run multiple copies of it at the same time.

On the Arduino Yún, running multiple shells usually only happens when you make multiple SSH connections to the Arduino. However, you can start a new shell process using the *sh* command. The newly-created shell sends its output back to the shell that creates it, and usually accepts its input from the information that you specify when you type the *sh* command.

The difference between an environment variable and a shell variable is most-easily demonstrated by looking at what happens when you start a new shell.

1.  At the command prompt, create an environment variable: type the following command and then press **Enter**:

    ```
    export ME=Bob
    ```

2.  Type the following command and then press **Enter**:

    ```
    echo $ME
    ```

3.  Type the following command and then press **Enter**:

    ```
    sh -c "echo \$ME"
    ```

4.  Now create a shell variable: type the following command and then press **Enter**:

    ```
    YOU=Alice
    ```

5.  Type the following command and then press **Enter**:

    ```
    echo $YOU
    ```

6.  Type the following command and then press **Enter**:

    ```
    sh -c "echo \$YOU"
    ```

Steps 3 and 6 both start a new shell and tell it to run the echo command. In the first example, steps 1–3, both *echo* commands display “Bob”. In the second example, steps 4–6, the first *echo* command displays “Alice” but the second does not. This is because the shell variable *YOU* is not accessible to the second shell.

In [Writing Shell Scripts](#part0005_split_004.html_tc2s5), you can see how to store sequences of Linux commands in a text file, and how to run the file and execute the commands. Linux starts these files in a similar way to how the sh command creates a shell, so you should use environment variables when you want to access the value from your script.

If a second shell creates its own shell variables, then it deletes them when it closes.

### Defining Environment Variables on Startup

OpenWrt-Yun does not define as many environment and shell variables as other versions of Linux. The key ones are created in the text file */etc/profile*, and if you want to define your own then this a good place to do so.

To add a new variable definition to */etc/profile*,

1.  On the command line, type the following command and then press **Enter**:

    ```
    nano /etc/profile
    ```

2.  Press the **Down Arrow** key until the text cursor is on the line that reads “export PS1='\u@\h:w\$ '”, and then press **Ctrl + E**.
3.  Press **Enter**.
4.  Type a new variable declaration, for example:

    ```
    export ARDUINO=Yun
    ```

5.  Press **Ctrl + X**.
6.  Press **Y**.
7.  Press **Enter**.
8.  Reboot the Arduino

* * *

## Writing Shell Scripts

A *shell script* is a text file that contains sequences of Linux commands. This can be useful in situations where you need to repeatedly run long commands, or perform exactly the same operation again at a later date.

Once created, there are five ways of running a shell script:

1.  From the command line. See [Running a Shell Script](#part0005_split_005.html_tc2s5s2).
2.  From an Arduino sketch. To learn how to run a shell script from an Arduino sketch, see [Using the Bridge Library](#part0007_split_000.html_tc4).
3.  At a scheduled time. See [Running a Shell Script at Predefined Intervals or on Specific Days](#part0005_split_005.html_tc2s5s13).
4.  When you login to the terminal. See [Configuring OpenWrt-Yun to Run a Script when You Login](#part0005_split_005.html_tc2s5s11).
5.  When the Arduino restarts. See [Configuring OpenWrt-Yun to Run a Script when It Starts](#part0005_split_005.html_tc2s5s12).

Scripts are very useful for administrative tasks and file management. But on Linux, a shell script can also perform complicated procedures, make decisions, and work with hardware devices. So they are one of the ways that you can use the power of the Linux side of the Yún in your projects.

### Creating Shell Scripts

Because shell scripts are text files, you can create them in any text editor. The file extension is usually *.sh* and, while this is not essential, it is a good idea to use the *.sh* extension so that you can easily tell which files are shell scripts.

To start a new script and save it to the microSD card on the Arduino Yún,

1.  At the command line, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/shell1.sh
    ```

2.  On the first line, type the following text and then press **Enter**:

    ```
    #!/bin/sh
    ```

3.  Add the following text and then press **Enter**:

    ```
    echo "Contents of microSD card:"
    ```

4.  Add the following text and then press **Enter**:

    ```
    ls /mnt/sda1/
    ```

5.  Press **Ctrl + X**.
6.  Press **Y**, and then press **Enter**.

The first line, *#!/bin/sh*, tells the system how to run the script. It is not always necessary to include this line, but it is a good practice. The remaining lines in this script are a sequence of commands that are executed when the script is run. Each command is on its own line.

*   The second line uses the *echo* command to send a text string to the console.
*   The third line uses the command *ls* to display the contents of the microSD card.

If you create your script files on your PC or Mac and then transfer them to the Arduino using SCP, you may need to adjust the file permissions before you can run the script. For more information about file access permissions, see [Setting the Access Permissions of Files and Directories](#part0005_split_002.html_tc2s2s5).

To change the permissions of *shell1.sh* so that all users can run it,

*   Type the following command and then press **Enter**:

    ```
    chmod 755 /mnt/sda1/shell1.sh
    ```

### Running a Shell Script

To run this script from the command line, type the following command and then press the Enter key:

```
/mnt/sda1/shell1.sh
```

If you are in the same directory as the script, you can run it without typing the full file path. Type the following command and then press the Enter key:

```
./shell1.sh
```

You can use the same syntax to run one shell script from another. To create a second script that runs the first,

1.  At the command line, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/shell0.sh
    ```

2.  On the first line, type the following text and then press **Enter**:

    ```
    #!/bin/sh
    ```

3.  Add the following text and then press **Enter**:

    ```
    /mnt/sda1/shell1.sh
    ```

4.  Press **Ctrl + X**.
5.  Press **Y**, and then press **Enter**.

Leave *shell1.sh* and *shell0.sh* on your SD card. You need them in the next section.

### Using Variables and Substitution

By using variables, you can make your shell scripts perform different actions every time you run the script. For more information about variables on Linux, see [Working with Environment and Shell Variables](#part0005_split_003.html_tc2s4).

*Substitution* occurs when you reference a variable in your shell script. For example, when you run the command *echo "The home directory is $HOME"*, the shell replaces the text *$HOME* with the value contained in the variable *HOME*.

To see substitution in action, and create a third script file,

1.  At the command line, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/shell2.sh
    ```

2.  On the first line, type the following text and then press **Enter**:

    ```
    #!/bin/sh
    ```

3.  Add the following text and then press **Enter**:

    ```
    echo "Contents of /"
    ```

4.  Add the following text and then press **Enter**:

    ```
    ls /
    ```

5.  Press **Ctrl + X**.
6.  Press **Y**, and then press **Enter**.

Run this script to test it. You should see the list of directories that are in the top level of the Linux file system.

Now edit *shell0.sh*.

1.  At the command line, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/shell0.sh
    ```

2.  Replace the line */mnt/sda1/shell1.sh* with

    ```
    /mnt/sda1/shell$SCRIPTNUM.sh
    ```

3.  Press **Ctrl + X**.
4.  Press **Y**, and then press **Enter**.

If you run the *shell0.sh* script now, it displays an error. The variable *SCRIPTNUM* is not defined (it is treated as blank) and so *script0.sh* tries to execute a file called *script.sh*.

At the command prompt, type the following command and then press the Enter key:

```
export SCRIPTNUM=1
```

Then run *shell0.sh* again. This time, *shell0.sh* runs *shell1.sh*.

Change *SCRIPTNUM* to 2 using the following command:

```
SCRIPTNUM=2
```

Then run shell0.sh again. Now *shell0.sh* runs *shell2.sh*.

In this example, *SCRIPTNUM* is an environment variable so that all scripts can access it. If you try to create a shell variable before calling your script, the script is not able to access that variable.

However, if you declare the shell variable at the same time as you run the script then the shell creates the variable in the same process as the script file. Then the script can access it. To do this, specify shell variables before the call to your script, but on the same line.

*   Type the following command and then press the **Enter** key:

    ```
    SCRIPTNUM=1 /mnt/sda1/script0.sh
    ```

To specify multiple variables, separate each with a space. For example:

```
SCRIPTNUM=1 V2=2 /mnt/sda1/script0.sh
```

You can now delete the three script files from the microSD card[2](#part0005_split_009.html_fn2).

### Defining Environment Variables from Scripts

When you define an environment variable from a shell script using *export*, it is accessible to any script that the current shell process runs. However, it is not always accessible to the rest of the system.

To fix this, you need to run your script on the primary shell process. You can do this using the *source* command. For example:

```
source ./script_file.sh
```

Or simply:

```
. ./script_file.sh
```

### Passing Arguments to Shell Scripts

Another way of changing how scripts run is to pass information into the script from the command line after specifying the name of the script. To do this, you use the same form that you use when passing information to a Linux command. For example:

```
./shell1.sh parameter1 parameter2 parameter3 ...
```

Inside the shell script, you can refer to these parameters using a dollar sign and then the parameter number. *$1* is the first parameter, *$2* is the second, and so on. When the shell encounters a parameter number in your script, it replaces it with the information from the command line.

For example,

1.  At the command line, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/shell1.sh
    ```

2.  On the first line, type the following text and then press **Enter**:

    ```
    #!/bin/sh
    ```

3.  Add the following text and then press **Enter**:

    ```
    echo "Contents of $1"
    ```

4.  Add the following text and then press **Enter**:

    ```
    ls $1
    ```

5.  Press **Ctrl + X**.
6.  Press **Y**, and then press **Enter**.

Call this script in the usual way, but add on a space and then the file path of a directory:

```
./shell1.sh /etc
```

You should see the *ls* command displays the files from the directory that you specify, and the preceding text “Contents of $1” is replaced by “Contents of /etc”.

The shell variable always *$#* shows the number of parameters that you passed into the script, and the variable *$0* always contains the text that is typed on the command line to start the script. In most cases, this is the file name of the script.

### Making Decisions

In shell scripts, you can use the *if* command to make decisions. With this, you can execute different commands depending on the values in variables, parameters, and even the output of other Linux commands.

The basic form of the *if* statement is

```
if [ <things to check> ]; then
     ...
fi
```

The shell *if* statement is similar to the C equivalent. However, you place conditions in square brackets (followed by a semi-colon) instead of parenthesis. And the block of code that runs if the conditions are *true* is placed between *then* and *fi*, not curly braces.

Tip: When writing *if* statements, pay attention to the spaces after a ‘[‘ character and before a ‘]’ character. These spaces are important in a shell script, and it is an error to miss them out.

For example, to test whether a variable contains a specific value:

```
if [ "$SCRIPTNUM" = "v1" ]; then
     ...
fi
```

If the variable *SCRIPTNUM* contains the characters “v1” then the script runs the commands between *then* and *fi*.

In many situations, it does not matter whether or not you place variable names and values in quotes. This is usually the case if you compare numbers, but it also applies to text. For example:

```
if [ $SCRIPTNUM = v1 ]; then
    ...
fi
```

However, you should be aware that the shell uses substitution to handle variables, and if the variable *SCRIPTNUM* is empty then the shell tries to run the following command:

```
if [ = v1 ]; then
```

This generates an error. If you surround variables and values in quotes then the script is more robust. Using quotes, if the variable *SCRIPTNUM* is empty then the shell runs:

```
if [ “” = “v1” ]; then
```

This does not cause an error.

If you need to treat multiple words (or character sequences that include punctuation symbols) as one item, you should wrap them in quotation marks. For example:

```
if [ “$MSG” = “Hello World!” ]; then
```

Without the quotes around *Hello World!*, the shell script compares the variable *MSG* against the value *Hello*, and cannot understand how to process *World!*

The examples so far use = (equals) to test whether one item is the same as another. != (not equal to) tests whether the items are different.

You can run a different set of commands when the variable does not contain the correct value. In the example below, the commands between *then* and *else* run if the value is *v1*; the commands between *else* and *fi* run if the value is not *v1*.

```
if [ "$SCRIPTNUM" = "v1" ]; then
     ...
else
     ...
fi
```

You can combine *if* statements using the *elif* command:

```
if [ "$SCRIPTNUM" = "v1" ]; then
     ...
elif [ "$SCRIPTNUM" = "v2" ]; then
     ...
else
     ...
fi
```

With *elif*, you can make sophisticated decisions based on multiple potential values, and then use *else* to state what happens if none of those conditions are met.In addition to checking whether a variable or parameter contains a specific value, there are a number of other conditions that you can test for. These conditions are placed inside square brackets, and include:

| Condition | Description |
| --- | --- |
| -z variable | Tests whether a variable, parameter, or string is empty or undefined. |
| -n variable | Tests whether a variable, parameter, or string is not empty. |
| -d name | Tests whether the specified location is a directory, not a file. |
| -e filename | Tests whether the specified file exists. |
| -f filename | Tests whether the specified file exists and is a regular file. |
| -r filename | Tests whether the specified file is readable by the current user. |
| -w filename | Tests whether the specified file can be written to by the current user. |
| -x filename | Tests whether the specified filename can be executed by the current user. |
| file1 -nt file2 | Tests whether the first file is newer (was modified more recently) than the second file. |
| file1 -ot file2 | Tests whether the second file is newer (was modified more recently) than the first file. |
| string -lt number | Converts the string to a number and then checks whether it is less than the specified number. |
| string -gt number | Converts the string to a number and then checks whether it is greater than the specified number. |

In [Using Variables and Substitution](#part0005_split_005.html_tc2s5s3), you write a script that calls other scripts depending on the value of the environment variable *SCRIPTNUM*. That script causes an error if *SCRIPTNUM* is not defined. You can extend the script to avoid this by testing whether the environment variable is set:

```
if [ -n "$SCRIPTNUM" ]; then
     /mnt/sda1/shell$SCRIPTNUM.sh
else
     echo "No script to run."
fi
```

In the table above, you can see several other conditions that you can use to similar effect. This includes using *[ -e "/mnt/sda1/shell$SCRIPTNUM.sh" ]* to check whether a suitable file can be found, and *[ -x "/mnt/sda1/shell$SCRIPTNUM.sh" ]* to test whether a suitable file can be found and make sure it is an executable script.

The final example of decision making in this section also involves an aspect of substitution that is not referenced in the previous section on that subject: you can capture the output of a Linux command and use this information in your *if* statements.

The Linux command *id* displays information about the user that is currently logged in. On the Yún, this is usually the root user. At the command prompt, type the following command and then press the Enter key:

```
id -u -n
```

The *-u* and *-n* parameters tell *id* to display only the user name.

In a shell script, you can test whether the current user is named “root” by using the following *if* statement:

```
if [ $(id -u -n) = "root" ]; then
fi
```

This runs the *id* command and captures the output. The result is substituted into the test condition and compared with the string “root”.

If you prefer, you can capture the output of *id* in a variable and then test that instead.

```
ME=$(id -u -n)
if [ "$ME" = "root" ]; then
fi
```

### Repeating Commands

There are three basic loops in shell scripting. With these you can repeat a sequence of commands a predefined number of times, or until a certain condition is met.

The first form of loop is the *while* loop.

```
COUNT=1
while [ "$COUNT" -lt 11 ]; do
     echo $COUNT
     COUNT=$((COUNT+1))
done
```

In the example above, the *while* loop runs until *COUNT* is equal to or greater than 11\. This has the effect of sending the numbers 1–10 to the console. The *while* loop does not automatically increase the *COUNT* variable, you must do this yourself. At the start of each phase of the loop, the shell evaluates the test condition. If it is true, the loop runs again. If it is false, the loop ends and the script continues to run any commands below the *done* statement.

Any of the test conditions mentioned so far can be used in a *while* loop. For example, to force a script to wait until a certain file no longer exists:

```
while [ -e "/mnt/sda1/lock.txt" ]; do
     sleep 1
done
```

The *sleep* command tells the shell to do nothing for the specified number of seconds. Without it, the code above would check for the file *lock.txt* as fast as it can. That is a waste, and working the processor that hard can drain a lot more power than is necessary.

Tip: It is very easy to accidently write a loop that never ends. If this happens, press Ctrl + C to terminate the current script.

The second form of loop in shell scripting is the *until* loop.

```
until [ -e "/mnt/sda1/lock.txt" ]; do
     sleep 1
done
```

The *until* loop works very similarly to the *while* loop. The difference is that *until* loops only run while the test condition is false. So the example above waits until the *lock.txt* file exists before exiting the loop and running any commands below the *done* statement.

The third type of loop is *for*. You can use the *for* loop to run a sequence of commands on each item in a list, or each file in a directory. The example below is a basic version of the Linux command *ls*.

```
for fn in /mnt/sda1/*; do
     echo $fn
done
```

The code above uses a wildcard (asterisk) to match all files in the */mnt/sda1* directory. During each phase of the loop, the shell copies a file name into the variable *fn*, and then the *echo* command prints this value to the console.

The *for* loop expects that each item in the sequence is separated by a space, not a line break. This means that the following example displays the output slightly differently than you might expect.

```
for wrd in $(cat $0); do
     echo $wrd
done
```

In [Passing Arguments to Shell Scripts](#part0005_split_005.html_tc2s5s5), you can see that *$0* refers to the name of the shell script that is running. The *cat* command sends a text file to the console, but by using substitution you are able to capture that output and include it in the *for* loop.

Finally, there are two commands that are only used in the middle of loops: *break* and *continue*.

| Command | Description |
| --- | --- |
| break | Exits the loop without checking the test condition. |
| continue | Jumps to the start of a loop, ignoring any other commands that are underneath the *continue* command. |

You can use *break* to terminate a loop early. For example, if you use a loop to search through a text file for the first instance of a particular word then you can use *break* to stop when the word is found, rather than needlessly process the rest of the document.

The following examples demonstrates the use of the *continue* command.

```
for fn in /mnt/sda1/*; do
     if [ "$fn" != "/mnt/sda1/arduino" ]; then
          echo $fn
     fi
done
```

The code above echoes the file name of every file or directory in the */mnt/sda1* directory, except for the one named “arduino”. The code below is an alternative way of doing this.

```
for fn in /mnt/sda1/*; do
     if [ "$fn" = "/mnt/sda1/arduino" ]; then
          continue
     fi
     echo $fn
done
```

When *fn* equals “arduino”, the *continue* command tells the shell to skip the remainder of the code and start again with the next file name. Because of this, the *echo* command does not run on that occasion and the */mnt/sda1/arduino* directory does not appear in the output.

### Getting Input from the User

Sometimes a shell script needs to ask the user for information. You might want the user to confirm actions that permanently makes changes to their system, or ask them to type in passwords and file names.

The shell command *read* takes keyboard input from the user and puts it into a shell variable. This process continues until the user presses the Enter key.

The next example implements a short confirmation sequence.

```
echo "Are you sure you want to continue? (yes/no):"
read response
if [ "$response" = "yes" ]; then
     echo "OK. I will continue."
else
     echo "OK. I will stop here."
fi
```

By default, the *read* command echoes key presses back to the console so that the user can see what they are typing. If you ask for sensitive information then you can disable this feature by attaching the flag *-s*.

```
echo "Type your password and then press Enter:"
read -s pwd
```

The flag *-t* specifies how long the *read* command waits for input. You can use this in combination with other flags. For example:

```
echo "Type your password and then press Enter within 5 seconds:"
read -s -t 5 pwd
```

All of the examples so far use the *echo* command to prompt the user for the information. Because *echo* also sends a line break, this causes the input to appear on the next line in the console. By using the *read* flag *-p*, you can prompt the user without sending a line break.

```
read -p "What is your name?: " nm
echo "Hello $nm"
```

### Stopping a Shell Script

If your script decides that it must stop (for example, in response to the user typing “no” in a confirmation) then you can use the *exit* command. This stops the script immediately and makes no further changes to the system. It does not undo any changes that have already been made.

To use *exit*, you should also include a number that represents why the script is stopping. This allows other scripts to decide what action to take.

The exit code zero indicates that the script terminated normally, and that no further action is needed. For example:

```
exit 0
```

### Defining Functions

Shell scripts can be quite large and complicated. And you may have long sequences of commands that are repeated in other places in the same script.

One way of organizing a script and avoiding too much repetition, is to define a function. Functions are blocks of code that only execute when another part of the script calls them.

The example below defines a function named “confirm”. This prompts the user to confirm an action, and exits the script if they type anything other than “yes”.

```
#!/bin/sh
confirm() {
     read -p "Are you sure you want to do this? (yes/no): " rsp
     if [ "$rsp" != "yes” ]; then
          echo "OK. Aborting script."
          exit 0
     fi
}

echo "This operation will make changes to your Arduino."
confirm
echo "Operation complete."
```

Note that when defining functions, the function name is followed by parenthesis, and the body of the function (the commands that it runs) is placed between two braces. You can run the function at any time by using its name.

You can also pass information into functions. For example, to modify the *confirm* function so that you can change the prompt:

```
confirm() {
     read -p "$1" rsp
     if [ "$rsp" != "yes" ]; then
          echo "OK. Aborting script."
          exit 0
     fi
}
```

The token *$1* refers to the first piece of information that you pass into the function. *$2* refers to the second, and so on.

To call this function now:

```
confirm "Are you sure you want to do this? (yes/no): "
```

When declaring variables inside the body of a function, they are still accessible to the rest of the script. If you want to declare a variable that only your function can use, include the keyword *local*. For example:

```
confirm() {
     local pt=$1
     read -p "$pt" rsp
     if [ "$rsp" != "yes" ]; then
          echo "OK. Aborting script."
          exit 0
     fi
}
```

When the function ends, the variable *pt* is destroyed.

Finally, you can make functions return actual values to the piece of the script that calls them. To do this, use the *return* command. For example, to modify the *confirm* function so that it returns 1 if the user types “yes”, and 0 if they type anything else (rather than ending the script):

```
confirm() {
     local pt=$1
     read -p "$pt" rsp
     if [ "$rsp" != "yes" ]; then
          return 0
     else
          return 1
     fi
}
```

The return value is available using the special variable *$?* immediately after the function finishes. You can copy its value to another variable, or use it in an *if* statement:

```
echo "This operation will make changes to your Arduino."
confirm "Are you sure you want to do this? (yes/no): "
if [ "$?" = 1 ]; then
     echo "OK. Making changes..."
else
     echo "OK. I will stop here."
     exit 0
fi
```

### Configuring OpenWrt-Yun to Run a Script when You Login

At this point, you have seen the key techniques and commands that enable you to write sophisticated and useful shell scripts. You have also seen how to run your scripts from the command line and from other scripts.

It is also possible to configure OpenWrt-Yun so that it runs one your scripts every time you login to the Yún.

In this short example, you will create a script that defines a new environment variable and then run this script every time you login.

To begin, create a new script file on the microSD card.

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/config.sh
    ```

2.  Add the following code to the script:

    ```
    #!/bin/sh
    export ME="Bob"
    ```

3.  Press **Ctrl + X**.
4.  Press **Y**, and then press **Enter**.

Now add a command to the */etc/profile* script so that your *config.sh* scripts runs every time you login.

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/profile
    ```

2.  On a new line underneath the final *export* command, add the following command:

    ```
    source /mnt/sda1/config.sh
    ```

3.  Press **Ctrl + X**.
4.  Press **Y**, and then press **Enter**.
5.  To log out of the terminal, type the following command and then press **Enter**:

    ```
    exit
    ```

Reconnect to the Arduino Yún using SSH, type the following command, and then press the Enter key:

```
echo $ME
```

Because this is only an example, you should remove the reference to the script from */etc/profile* before continuing. It is no longer needed. You can also delete the *config.sh* file.

### Configuring OpenWrt-Yun to Run a Script when It Starts

If you want to run a script every time OpenWrt-Yun reboots, but not every time you login, you can run your script file from */etc/rc.local* instead.

For example, to create a new script file on the microSD card,

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/config.sh
    ```

2.  Add the following code to the script:

    ```
    #!/bin/sh
    ls / > /mnt/sda1/list.txt
    ```

3.  Press **Ctrl + X**.
4.  Press **Y**, and then press **Enter**.

Now add a command to the */etc/rc.local* script so that your *config.sh* scripts runs every time the Arduino starts up.

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/rc.local
    ```

2.  On a new line before the *exit 0* command, add the following command:

    ```
    source /mnt/sda1/config.sh
    ```

3.  Press **Ctrl + X**.
4.  Press **Y**, and then press **Enter**.
5.  To restart the Arduino, press the **YÚN RST** button.

Log back into the Arduino using SSH, type the following command, and then press the Enter key:

```
cat /mnt/sda1/list.txt
```

The difference between running a script from */etc/rc.local* and */etc/profile* becomes more obvious if you delete the *list.txt* file. For example,

1.  Type the following command and then press **Enter**:

    ```
    rm /mnt/sda1/list.txt
    ```

2.  Type the following command and then press **Enter**:

    ```
    exit
    ```

3.  Log back into the Arduino over SSH.
4.  Type the following command and then press **Enter**:

    ```
    cat /mnt/sda1/list.txt
    ```

When you log back in, the *list.txt* file does not exist because *rc.local* only runs your script when the Arduino is reset.

You can now remove the *source /mnt/sda1/config.sh* line from your */etc/rc.local* file and delete the script.

Tip: You can also edit the */etc/rc.local* file from the Arduino’s advanced configuration panel. In the System tab, click Startup.

### Running a Shell Script at Predefined Intervals or on Specific Days

Linux operating systems usually include a task scheduler called *cron*. You can use this to run programs and scripts at predefined intervals (such as every hour, every day) or at a set date and time. You can configure *cron* from the command line, however, you can also do this from the Arduino Yún’s advanced configuration panel.

To access the advanced panel, and modify the settings for *cron*:

1.  On a machine that connects to the same network as the Arduino, open a web browser.
2.  In the address bar, type *http://arduino.local*
3.  Type the current password[3](#part0005_split_009.html_fn3) and then click **LOG IN**.
4.  Click **CONFIGURE**.
5.  Click **advanced configuration panel (luci)**.
6.  Click the **System** tab, and then click **Scheduled Tasks**.

To schedule a task, you need to add a line to the Scheduled Tasks box. Each task should appear on its own line and follow a set format that is made up of six parts:

```
minute hour day month day_of_week command
```

| Part | Description |
| --- | --- |
| minute | The number of minutes past the hour (0–59) that this task runs at. |
| hour | The hour (0–23) that the task runs at. |
| day | The day of the month (1–31) that this task runs on. |
| month | The month (1–12) that this task runs on. |
| day_of_week | The day of week name (0–6 or Sun–Sat) that this task runs on. |
| command | The Linux command that runs. |

Each part (with the exception of *command*) can also be an asterisk. This indicates that you don’t care what the value is.

| To | Do This |
| --- | --- |
| Run a task every hour | Define the task with 0 * * * * |
| Run a task at 30 minutes past the hour, every hour | Define the task with 30 * * * * |
| Run a task daily at midnight | Define the task with 0 0 * * * |
| Run a task on the first day of every month at midnight | Define the task with 0 0 1 * * |
| Run a task every Wednesday at 02:00 | Define the task with 0 2 * * 3 |
| Run a task on Saturday 29th November at 18:30 | Define the task with 30 18 29 11 * |

For example, to schedule the *config.sh* file from [Configuring OpenWrt-Yun to Run a Script when It Starts](#part0005_split_005.html_tc2s5s12), type the following line into the Scheduled Task box:

```
0 * * * * source /mnt/sda1/config.sh
```

Click the Submit button, and then reboot the Yún for these changes to take effect.

* * *

## Expanding the Linux File System onto the microSD Card

OpenWrt-Yun takes up most of the storage space on the Atheros AR9331 SoC. This leaves very little room for any additional files and programs that you may want to install.

To increase the amount of space available to Linux, you can configure the Yún to use the microSD card for the file system. This divides the microSD card into two partitions – a FAT32 “data” partition which you can use to transfer files from your PC or Mac to the Arduino, and a Linux partition that is used by OpenWrt-Yun. Microsoft Windows and Apple Mac OS X cannot read the Linux part, and so if you put your microSD card back into a PC or Mac then it appears to have shrunk in capacity.

Tip: This partitioning is not permanent. If you want to make the whole SD card accessible to Windows or Mac OS X, you need only delete the two partitions and create a new primary partition that is set to use all of the space on the card. There are many applications that you can use to do this, including diskpart (already installed on Windows) and GParted.

To help you expand the file system, Arduino LLC have a sketch that you can download from their web site. This runs on the Arduino Yún and does most of the work for you. This process deletes everything on the microSD card, so check that the card does not contain any files that you want to keep.

To run the *YunDiskSpaceExpander* sketch, connect your Yún to your computer with a USB cable. The sketch uses the Serial Monitor from the Arduino IDE, which you can only use over USB.

To configure OpenWrt-Yun to use space on the microSD card:

1.  If you have any files open on the microSD card, close them. Then close any remote connections to the Yún.
2.  In a web browser, type the following URL into the address bar: [http://arduino.cc/en/uploads/Tutorial/YunDiskSpaceExpander.zip](http://arduino.cc/en/uploads/Tutorial/YunDiskSpaceExpander.zip)
3.  If you are on Windows: find the *.zip* file you downloaded and right-click it. Point to **Open with** and then click **Windows Explorer**.
4.  If you are on Mac OS X: double-click the *.zip* file that you downloaded and it will unzip to a new folder[4](#part0005_split_009.html_fn4). In a **Finder** window, open the newly-unzipped folder.
5.  Double-click the *.ino* file to open it in the Arduino IDE.
6.  On the toolbar, click **Upload**.
7.  On the **Tools** menu, click **Serial Monitor**.
8.  In the **No line ending** list, click **Newline**.
9.  In the textbox at the top of the **Serial Monitor**, type *yes* and then press **Enter**.
10.  Type *yes* and then press **Enter**.
11.  Type *yes* and then press **Enter**.
12.  Type a number (in megabytes) for the size of the FAT32 “data” partition. Then press **Enter**.
13.  On the Yún, press the **YÚN RST** button.
14.  Unplug the power supply from the Yún, then reinsert it and wait for OpenWrt-Yun to load.

You can access the microSD card from the Linux file system using the path */mnt/sda1/*. This applies whether you expand the Linux file system or not.

When you expand the Linux file system onto the microSD card, the *YunDiskSpaceExpander* sketch creates an *arduino* directory (and a *www* subdirectory) on the card. It also creates a symbolic link between */www/sd* and the */mnt/sda1/arduino/www* directory. This link is useful when you want to run webpages from the Yún. For more information about hosting websites, see [Hosting Websites and Services](#part0008_split_000.html_tc5).

After expanding the file system, the Yún needs the microSD card to load correctly. If you remove or change the card then you have to reconfigure the Yún.

* * *

## Installing Linux Packages

When installing new software on Linux, there are several steps that must be taken:

1.  Check whether the software is compatible with the operating system.
2.  Check whether all of the software that the new program depends on is already installed. If it is not, these dependencies have to be installed too.
3.  Download the new software from the Internet.
4.  Install the new software.

To assist in this process, Linux distributions use tools called “package managers”. These tools try to perform all of the steps above for you. On OpenWRT and OpenWrt-Yun, the package manager is OPKG.

A *repository* is an online collection of software that you can download and install by using a package manager. Each item is called a “package” and, in most cases, software in a Linux repository is free. Initially, it can be helpful to think of a repository as a simplified version of the Apple App Store or Google Play.

OpenWrt-Yun is configured to use a repository created by Arduino LLC, and this contains many useful packages for Yún users. These packages are made especially for the Yún, and so not all of the software that runs on desktop versions of Linux is currently available.

### Using OPKG and Finding Packages

To save space in the AR9331’s memory, OPKG does not keep an up to date list of all of the packages that are available in the Arduino Yún repository. You must download the list before using the package manager. Every time you restart the Arduino, this list of packages is deleted.

*   On the command line, type the following command then press **Enter**:

    ```
    opkg update
    ```

You can use the command *list* to display all of the software that is available in the repository, or to search for packages by their name.

To view all packages,

*   Type the following command and then press **Enter**:

    ```
    opkg list
    ```

To view only the GCC compiler package, which is named “yun-gcc”,

*   Type the following command and then press **Enter**:

    ```
    opkg list yun-gcc
    ```

If a package with that name cannot be found, OPKG displays no information. If the package is there, OPKG displays a short summary (usually a version number and brief description) of the software. You can see more information by using the *info* command,

*   Type the following command and then press **Enter**:

    ```
    opkg info yun-gcc
    ```

You can also use wildcards (typed as an asterisk) to search file names. To view only packages that have a name beginning with the three characters “yun”,

*   Type the following command and then press **Enter**:

    ```
    opkg list yun*
    ```

Or to view a list of packages that contain the characters “gcc” anywhere in their name,

*   Type the following command and then press **Enter**:

    ```
    opkg list *gcc*
    ```

### Installing a Package

Before installing additional software on your Yún, you should expand the Linux file system so that it can use the microSD card for storage space. Packages, and all of the software that they depend on, can be quite large and the AR9331 SoC only has a few megabytes of free space. For more information, see [Expanding the Linux File System onto the microSD Card](#part0005_split_005.html_tc2s6).

When you have found a package in the repository that you want to install, you can download and install it with one command: *install*.

For example, to download the *libxml2* package (a library for manipulating XML files),

*   Type the following command and then press **Enter**:

    ```
    opkg install libxml2
    ```

This process also downloads and installs any of the dependency software that the new package needs. In this example *libc*, *libpthread*, and *zlib* are also downloaded if they are not already on the system.

Tip: When software installs, it is copied to the correct file system folders. However, each package is different and it may not be obvious how to use the software. You may have to search the web and find the developer’s website in order to learn how to use the package.

### Updating and Uninstalling Packages

To view a list of all of the packages that are installed on your Arduino,

*   Type the following command and then press **Enter**:

    ```
    opkg list-installed
    ```

As with the *list* command, you can also use package names and wildcards with *list-installed*.

It is not uncommon for the developers of packages to update them. They usually do this to fix a bug or problem in the software, or to add new features.

You can use the package manager to update the software on your Yún. To view a list of any packages that are out of date,

*   Type the following command and then press **Enter**:

    ```
    opkg list-upgradable
    ```

Then to update a single package, you can use the *upgrade* command. For example,

*   Type the following command and then press **Enter**:

    ```
    opkg upgrade libxml2
    ```

To uninstall a package and free up space on your Arduino Yún, you can use the *remove* command. This does not uninstall any packages that the software depends on. For example,

*   Type the following command and then press **Enter**:

    ```
    opkg remove libxml2
    ```

### Installing and Removing Packages with the Advanced Configuration Panel

In addition to installing and removing packages from the command line, you can use the web-based advanced configuration panel.

To access this:

1.  On a machine that connects to the same network as the Arduino, open a web browser.
2.  In the address bar, type *http://arduino.local*
3.  Type the current password and then click **LOG IN**.
4.  Click **CONFIGURE**.
5.  Click **advanced configuration panel (luci)**.
6.  Click the **System** tab, and then click **Software**.

To download the up to date list of packages that are available in the repository:

*   Under **Actions**, click **Update lists**.

To find a package that is either installed on your Arduino or available from the repository:

1.  In the **Filter** box, type any part of the name of the package.
2.  Click **Find Package**.

To remove a package that is already installed:

1.  Under **Status**, click **Installed packages**.
2.  Next to the item you want to remove, click **Remove**.

To install a package:

1.  Under **Status**, click **Available packages**.
2.  Next to the item that you want to install, click **Install**.

* * *

## Resetting OpenWrt-Yun

If the operating system becomes unstable or corrupted, or you just want to wipe everything from the Yún and start again with a clean system, you can either:

*   Download and install the latest upgrade image from [http://arduino.cc/en/Main/Software#toc8](http://arduino.cc/en/Main/Software#toc8). This process wipes your Arduino. For more information, see [Updating OpenWRT](#part0004_split_002.html_tc1s2); or
*   Reset the Arduino by pressing the **WLAN RST** button for longer than 30 seconds.

In either case, you may then have to reconfigure the Yún’s network connection, install any additional Linux packages that you need, and expand the Linux file system to the microSD card.

When you install an upgrade image on the Yún, it overwrites the backup data that the reset process uses. So resetting OpenWrt-Yun using the WLAN RST button puts the Linux side of the Yún back into the same state that it was in when you first installed the upgrade image. It does not return the Yún to the same state that it was in when you first received the board.

* * *

## Backing Up the Arduino Yún

As with any computer, there can be times when hardware fails or when you need to reinstall the operating system. To avoid losing work, you should ensure that you have a backup of all of your important files and configuration settings.

There are several ways you can make a backup:

*   You can backup network configuration, password settings, and other OpenWrt-Yun configuration files from the advanced configuration panel;
*   You can download important files to another computer, using secure copy protocol (SCP);
*   If you expand the Linux file system onto the microSD card, you can make a copy of the entire card.

### Backing Up Configuration Settings using the Advanced Configuration Panel

The advanced configuration panel has an option that you can use to create a backup copy of the most important configuration files and settings. If you need to reset your Yún and reinstall OpenWrt-Yun, you can use the “restore backup” option to transfer the previous settings back onto your Yún.

To create a backup of your configuration files and download them to another computer:

1.  On a machine that connects to the same network as the Arduino, open a web browser.
2.  In the address bar, type *http://arduino.local*
3.  Type the current password and then click **LOG IN**.
4.  Click **CONFIGURE**.
5.  Click **advanced configuration panel (luci)**.
6.  Click the **System** tab, and then click **Backup / Flash Firmware**.
7.  Under **Backup / Restore**, click **Generate archive**.

The backup file is a *.tar.gz* archive that contains the contents of the OpenWrt-Yun */etc* directory.

To transfer previous settings to the Yún:

1.  On a machine that connects to the same network as the Arduino, open a web browser.
2.  In the address bar, type *http://arduino.local*
3.  Type the current password and then click **LOG IN**.
4.  Click **CONFIGURE**.
5.  Click **advanced configuration panel (luci)**.
6.  Click the **System** tab, and then click **Backup / Flash Firmware**.
7.  Next to **Restore backup:**, click **Browse**.
8.  Click the *.tar.gz* file that contains your configuration files, and then click **Open**.
9.  Click **Upload archive...**

### Downloading Files using SCP

You can transfer files from the Arduino Yún to another computer by using SCP. For more information, see [Transferring Files between the Arduino and a PC/Mac](#part0005_split_001.html_tc2s1s1).

After a reinstall of OpenWrt-Yun, you can restore files by uploading them from your computer to the Arduino. However, this is not always suitable when transferring Linux executables and other software that you install on the Yún.

### Copying the microSD Card

If you install additional software on the Yún, you should expand the Linux file system to the microSD card. Then, to back up the Linux system, copy the entire microSD card (not just the files on it).

When you expand the Linux file system onto the microSD card, the process divides the card into two partitions. One of these is a FAT32 data partition that you can use to store your files. The other contains a copy of the Linux system and any additional software that you install.

On Mac OS X and Linux, you can use the command *dd* to create a file that contains an exact copy of the microSD card. On Microsoft Windows, you need to install additional software.

These copies are often called “disk images”. Disk images that you make from hard drives and disks contain all of the extra information about the partitions and the permissions of files.

#### Copying the microSD Card on a Linux Computer

To create a disk image of the Yún’s microSD card on a Linux computer:

1.  Unplug the Arduino Yún from its power supply.
2.  Remove the microSD card.
3.  Insert the microSD card into a suitable slot on your computer.
4.  Open a terminal or command line.
5.  Type the following command and then press **Enter**:

    ```
    sudo fdisk -l
    ```

6.  Find the **Device** in the list. You should see two devices (one for each partition on the microSD card) with similar names. For example: */dev/sdb1* and */dev/sdb2*. One has the type “W95 FAT32 (LBA)” (or similar description) and the other has the type “Linux”. The parent device of these two devices is */dev/sdb*.
7.  Type the following command and then press **Enter**:

    ```
    sudo dd if=/dev/sdb of=./yun-backup.bin
    ```

To restore a backup,

*   Type the following command and then press **Enter**:

    ```
    sudo dd if=./yun-backup.bin of=/dev/sdb
    ```

#### Copying the microSD Card on an Apple Mac

To create a disk image of the Yún’s microSD card on Mac OS X:

1.  Unplug the Arduino Yún from its power source.
2.  Remove the microSD card.
3.  Insert the microSD card into a suitable slot on your Mac.
4.  Open a Terminal.
5.  Type the following command and then press **Enter**:

    ```
    diskutil list
    ```

6.  Find the device label for the microSD card – it contains two partitions. For example, */dev/disk2*.
7.  Type the following command and then press **Enter**:

    ```
    dd if=/dev/disk2 of=yun-backup.bin
    ```

To restore a backup,

1.  Type the following command and then press **Enter**:

    ```
    diskutil unmountDisk /dev/disk2
    ```

2.  Type the following command and then press **Enter**:

    ```
    dd if=yun-backup.bin of=/dev/disk2
    ```

#### Copying the microSD Card on Microsoft Windows

Mac OS X and most Linux distributions already have the *dd* command. On Microsoft Windows, you need to install a suitable program. One option is to use Win32DiskImager. To install it, download and run the setup program from [http://sourceforge.net/projects/win32diskimager/files/latest/download](http://sourceforge.net/projects/win32diskimager/files/latest/download)

Then, to create a disk image of the Yún’s microSD card:

1.  Unplug the Arduino Yún from its power source.
2.  Remove the microSD card.
3.  Insert the microSD card into a suitable slot on your PC.
4.  Start Win32DiskImager.
5.  Windows recognizes the FAT32 partition on the microSD and assigns a drive letter to it. In the **Device** list, click the drive letter for your microSD card.
6.  Under **Image File**, click the folder button.
7.  Browse to where you want to save the image file and click **Open**.
8.  Click **Read**.

Even though Windows cannot recognize the Linux partition and you can only select the FAT32 partition in Win32DiskImager, the tool reads the entire contents of the card.

To restore a backup:

1.  Insert a microSD card into a suitable slot on your PC.
2.  Start Win32DiskImager.
3.  Under **Image File**, click the folder button.
4.  Browse to your image file, click it, and then click **Open**.
5.  In the **Device** list, click the drive letter for your microSD card.
6.  Click **Write**.

* * *

[1](#part0005_split_002.html_nf1)This number shows the number of links to the file. It is not important at this stage.[2](#part0005_split_005.html_nf2)rm /mnt/sda1/*.sh[3](#part0005_split_005.html_nf3)If you have not changed it, the password is arduino.[4](#part0005_split_006.html_nf4)If you have installed an archiving tool on your Mac, the OpenWrt-Yun update image might open with this instead. If you need help, consult the documentation for your archiving tool.

# Programming in Python

Python is a programming language that you can use to control the Atheros AR9331 SoC on the Arduino Yún. It is similar to the variety of C/C++ that you use to write sketches on the Arduino, and many of the commands and structures that are in Arduino C are also in Python.

Unlike C, Python is an interpreted language. This means that you do not compile your programs as you do with an Arduino sketch. Instead, a piece of software (an interpreter) runs on OpenWrt-Yun Linux. This software reads your source code and performs the instructions for you. Version 2.7.3 of the Python interpreter is already installed on your Arduino Yún.

Python users often encourage programmers to use a specific style of coding, called “Pythonic”. Pythonic is a set of style guidelines that promotes writing programs in a way that highlights the unique features of the language.

This chapter is an introduction to the Python language, and there are certain elements that are not covered here. It is primarily aimed at readers who are used to Arduino C, and sometimes uses code samples that are not Pythonic so that they are easier to understand. When you are more familiar with programming in Python, you should read the Pythonic style guidelines at [http://www.python.org/dev/peps/pep-0008/](http://www.python.org/dev/peps/pep-0008/), and there are a large number of online resources that can help you learn even more about the language.

In This Chapter

[Running Python on the Yún](#part0006_split_000.html_tc3s1)

[Performing Basic Arithmetic](#part0006_split_001.html_tc3s2)

[Working with Strings and Variables](#part0006_split_002.html_tc3s3)

[Making Decisions](#part0006_split_003.html_tc3s4)

[Looping your Code](#part0006_split_004.html_tc3s5)

[Writing your Own Functions](#part0006_split_005.html_tc3s6)

[Working with Classes and Objects](#part0006_split_006.html_tc3s7)

[Using Packages and Modules](#part0006_split_007.html_tc3s8)

[Reading and Writing to Files](#part0006_split_008.html_tc3s9)

[Handling the Errors in Scripts](#part0006_split_009.html_tc3s10)

[Compiling your Python Programs](#part0006_split_010.html_tc3s11)

* * *

## Running Python on the Yún

There are two ways of using Python on the Yún: in interactive mode, or by running Python scripts.

In interactive mode, the Python interpreter is a command-line interface (CLI) that you can use to type Python commands one by one.

To start the Python CLI:

1.  Login to the OpenWrt-Yun command line. For more information, see [Connecting to the Arduino Yún](#part0005_split_000.html_tc2s1).
2.  Type the following command and then press **Enter**:

    ```
    python
    ```

The Python command prompt is different to the Linux command prompt. You can tell that you are in the Python environment when the command prompt is >>>.

To run a command, type it on the keyboard and then press the Enter key. For example, to display a message in the console,

*   At the Python command prompt, type the following command and then press **Enter**:

    ```
    print "Hello from Python."
    ```

To close the Python CLI and return to the Linux command line, either

*   Type the following command and then press **Enter**:

    ```
    exit()
    ```

*   Or press **Ctrl + D**.

### Running a Python Script

A Python script is a text file that contains a sequence of Python commands. Instead of typing each command and running them one by one, you can run the entire script in one go. You can create these scripts in any text editor – including GNU nano, as described in [Editing Text Files with GNU nano](#part0005_split_002.html_tc2s3).

Type each command in a Python script on its own line. And, unlike C, you do not end the command with a semi-colon.

In the following sections of this chapter, you will learn how to use the Python language to write programs. For now, create and run a short sample script.

1.  At the Linux command prompt, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/test.py
    ```

2.  Add the following text to the file:

    ```
    # A test script to display the user’s name repeatedly
    name = raw_input("What is your name? ")
    for i in range(1, 10):
        print name
    ```

3.  Press **Ctrl + X**.
4.  Press **Y** and then press **Enter**.

Take care to type in the script accurately, and remember to place four spaces before the text “print name”.

Tip: The line beginning with the symbol # is a comment. The Python interpreter ignores these lines and so you can use them to add extra information to your program.

To run this Python script,

*   At the Linux command prompt, type the following command and then press **Enter**:

    ```
    python test.py
    ```

In the same way as a shell script can specify the binary program that Linux should use to interpret it, the first line of a Python script can also include a reference to the Python interpreter.

1.  Type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/test.py
    ```

2.  Add the following text on its own line at the top of the file:

    ```
    #!/usr/bin/python
    ```

3.  Press **Ctrl + X**.
4.  Press **Y** and then press **Enter**.

With this reference on the first line, you can run the Python script without calling the Python interpreter yourself. For example, type the following command and then press the Enter key:

```
/mnt/sda1/test.py
```

* * *

## Performing Basic Arithmetic

There are several different types of number in Python. The two most common are *integers* and floating-point numbers (*floats*).

An integer is a whole number – it does not have a decimal point or a fraction. It can be negative (less than zero) or positive (greater than zero). The numbers 1, -3, and 0 are examples of integers.

A float is a number that can use a decimal point. The numbers 88.8, -0.0123, and 1.0 are examples of floats.

You can use *mathematical operators* to combine numbers in different ways and calculate the result.

For example,

1.  At the Linux command prompt, type the following command and then press **Enter**:

    ```
    python
    ```

2.  At the Python prompt, type the following command and then press **Enter**:

    ```
    print 5 + 18.3
    ```

The *print()* function displays a message or value in the console. You can also enclose the message in parenthesis: *print(5 + 18.3)*

| To | Do This |
| --- | --- |
| Add two numbers together | Type one number, followed by + and then another number. |
| Subtract the second number from the first | Type the first number, followed by - and then the second number. |
| Multiply two numbers together | Type one number, followed by * and then another number. |
| Divide the first number by the second | Type the first number, followed by / and then the second number. |
| Divide the first number by the second and return an integer | Type the first number, followed by // and then the second number. |
| Perform modulo arithmetic | Type one number, followed by % and then another number. |

* * *

## Working with Strings and Variables

As in Arduino C, a *string* is a sequence of characters that you surround with quotation marks. The sample script in [Running a Python Script](#part0006_split_001.html_tc3s1s1), includes the string “What is your name? “

Strings can contain any letter or number, and most punctuation marks. For special characters such as line breaks, quotation marks, or tabs, you can use *escape characters* to add them to a string. Escape characters begin with a single backslash, and the Python interpreter replaces them with the chosen character automatically. For example, you can include *\t*to insert a tab, *\"* to insert a quotation mark, and *\n* to include a line break. But in Python, you can also declare triple-quoted strings that include any line breaks and white space that you type into the script file.

```
print "Twas the Night Before Christmas"
print "by Clement Moore"
print """
      Twas the night before Christmas,
      When all through the house,
      Not a creature was stirring,
      Not even a mouse.
"""
```

To join two strings together, use the *+* operator. For example:

```
print "Hello " + "World"
```

And you can use the *** operator to repeat strings a set number of times. In the following example, the parenthesis ensure that Python only repeats the string “!”, not the whole phrase.

```
print "Hello World" + ("!" * 5)
```

Tip: In [Working with Classes and Objects](#part0006_split_006.html_tc3s7), you can see other ways of using and manipulating strings in Python.

### Creating Variables

A *variable* is an area of the computer’s memory that you give a name to. You can use variables to hold information until the Python script ends.

To declare a variable in Python: specify a name, followed by the equals sign and then a value. For example,

```
result = 1
```

The name can begin with a letter (a–z or A–Z) or an underscore. Any following characters can be a letter, an underscore, or a number.

Variables work slightly differently in Python than in Arduino C because Python is a *weakly-typed* language. This means that you do not have to state what type of information a variable can hold, and the type of information can change at any point in the program. So you can create a string variable and then change it to hold a number:

```
message = "This is a test."
print message
message = 5
print message + 1
```

When you use the variable in your program, the Python interpreter tries to decide the best way of working with the information in the variable. This can sometimes cause errors.

The following command is valid, and Python converts the number into a string before appending it to the message.

```
message = "This is a test (" + 5 + ")."
```

However, this next command causes an error. Since the number comes first, Python attempts to convert anything that follows into a number.

```
message = 5 + "This is a test."
```

### Converting Strings to Numbers

In the previous example, you can see how trying to append a string to a number causes an error. This also happens if you try a command like:

```
v = "6"
message = 5 + v
```

There are two Python functions that you can use to convert a string to a number, and doing so avoids the error.

| Function | Description |
| --- | --- |
| int(string) | Tries to convert the specified string to an integer. |
| float(string) | Tries to convert the specified string to a float. |

For example:

```
v = "6"
message = 5 + int(v)
```

If the string cannot be converted to a number (for example “6 mm“) then the Python interpreter displays an error. When asking the user to type numbers into your scripts on the keyboard, there can be a problem if they type letters instead. You can catch these types of error – for more information see [Handling the Errors in Scripts](#part0006_split_009.html_tc3s10).

### Introducing Lists, Tuples, and Dictionaries

There are three common types of collection in Python: lists, tuples, and dictionaries. They appear to be similar to the arrays that you use in Arduino C, but each one has a slightly different purpose.

Lists package multiple pieces of information together into a single variable. To create a list, use square brackets. For example, to create an empty list:

```
mylist = []
```

Or to specify the values that you want in the list, separate each item with a comma. For example:

```
greek = ["Alpha", "Beta", "Gamma", "Delta", "Epsilon", "Eta"]
```

Each item in the list is accessible by its position number, with the first item being at position zero. In the example above, position five is “Eta”. You can change an item (and fix the deliberate mistake) by using this position number, for example:

```
greek[5] = "Zeta"
```

To find the length of a list, use the function *len()*. The following command outputs the value *6* because there are six items in the *greek* list.

```
print len(greek)
```

You can also delete items from a list. To do this, use the function *del()*.

```
del greek[2]
```

When an item is deleted, all of the items that follow it in the list move up one position. So deleting *Gamma* from position two puts *Delta* into position two, *Epsilon* into position three, and *Zeta* into position four.

In Python, lists are a special type of object, and so they contain several methods that you can use to manipulate the contents of the list. For more information about objects, see [Working with Classes and Objects](#part0006_split_006.html_tc3s7).

| Method | Description |
| --- | --- |
| append(object) | Adds the specified item to the end of the list. |
| count(object) | Counts how many times the specified item appears in the list and returns the result as an integer. |
| index(object) | Searches the list for the specified item and returns its position in the list. |
| insert(position, object) | Adds an item to the list in the specified position. |
| remove(object) | Removes the specified item from the list. |
| reverse() | Reverses the order of items in the list. |

To use a method, add a dot after the list name and then specify the method (and any arguments). For example, to remove the *Gamma* item:

```
greek.remove("Gamma")
```

A tuple is very similar to a list. However, once a tuple is created, you cannot change the items in it. You cannot add and remove items from a tuple.

Because they are a simpler than a list, the Python interpreter can handle them significantly faster. This makes them useful when you need to pass a predefined number of items between different parts of your code. For example, when returning multiple values from a function.

To create a tuple, use parenthesis.

```
mytuple = (1, 2, 3)
```

Like in a list, each item in a tuple is ordered. You can access an individual item by using square brackets and its position. For example:

```
print mytuple[0]
```

And you can find the number of items in a tuple with the *len()* function:

```
var1 = len(mytuple)
```

The third type of collection is a dictionary. Again, these are very similar to Python’s lists. However, you can give each slot in a dictionary a name (or *key*). Instead of referring to items by their position, you can use this key.To create a dictionary, use curly braces. For example:

```
character = { "Name":"Legolas", "Class":"Archer", "Race":"Wood Elf", "Age":2931 }
```

Each item consists of two parts: the name of the key, and a value. Use a colon to separate these two parts, and a comma to separate each item in the dictionary. The key is always a string, but the value can be any type of data.

To access the value of an item, use the key.

```
character["Age"] = character["Age"] + 1
```

The *len()* and *del()* functions work the same way on dictionaries as they do on lists. But there are also several other methods that you can use.

| Method | Description |
| --- | --- |
| clear() | Removes all items from the dictionary. |
| copy() | Gets a copy of the dictionary. |
| has_key(key) | Returns *True* if the specified key is in the dictionary, or *False* if it is not. |
| keys() | Gets a list of the keys in the dictionary. |
| update(dic) | Adds the items from the specified dictionary to the current dictionary. |
| values() | Gets a list of the values in the dictionary. |

* * *

## Making Decisions

In both Python and Arduino C, making a decision involves deciding whether a particular condition is *True*, or whether it is *False*. Depending on the result of the condition, you can run different blocks of commands.

To check a condition, use the *if* statement. For example:

```
if raw_input("Quit? (y/n): ") == "y":
    print "Quitting..."
    exit
print "This line does not run if the user types y."
```

This example uses the *raw_input()* function to prompt the user for text input on the keyboard.

The *==* operator compares two values (the user’s input and the string “y”) and returns *True* if they are equal, or *False* if they are different.

There are a few important differences between the *if* statement in Python and its equivalent in Arduino C:

*   You do not surround the code that runs if the statement is *True* with curly braces;
*   Put a colon at the end of the first line;
*   Indent the code that runs if the statement is *True*. Four spaces is recommended.

Indenting the code is not only to make reading the source code easier. The Python *if* statement expects you to indent all of the code that the interpreter should run if the condition is True. When the interpreter finds code that it is not indented, it treats this as the end of the *if* statement.

You can extend the *if* statement with a block of code that runs if the condition is *False*. To do this, use the keyword *else*.

```
inp = raw_input("Continue? (y/n): ")
if inp == "y":
    print "OK."
    print "I shall continue."
else:
    print "OK."
    print "I shall stop here."
    exit
print "This line only runs if the user types y."
```

And you can also use the *if* statement to check for several possible values. To do this, add another condition using the keyword *elif*.

```
inp = raw_input("Abort, Retry, Fail?")
if inp == "a":
    print "Abort."
elif inp == "r":
    print "Retry."
elif inp == "f":
    print "Fail."
else:
    print "Invalid input."
```

There are several other operators that you can use in Python. All of these compare two values and return either *True* or *False*.

| Operator | Description |
| --- | --- |
| != | Returns *True* if two values are not equal, and *False* if they are. This is the opposite of *==*. |
| > | Returns *True* if the first number is greater than the second, and *False* if it is not. |
| < | Returns *True* if the first number is less than the second, and *False* if it is not. |
| >= | Returns *True* if the first number is greater than or equal to the second, and *False* if it is not. |
| <= | Returns *True* if the first number is less than or equal to the second, and *False* if it is not. |

To combine two (or more) conditions into one *if* statement: place each condition in parenthesis and then use one of the *logical* operators below:

| Operator | Description |
| --- | --- |
| and | Returns *True* if both conditions are *True*, and *False* if either one is *False*. |
| or | Returns *True* if either of the expressions is *True*. Returns *False* if they are both *False*. |

For example:

```
inp = raw_input("Abort, Retry, Fail?")
if (inp == "a") or (inp == "r") or (inp == "f"):
    print "Valid input."
else:
    print "Invalid input."
```

The *not()* function inverts the value of a condition. If the condition is *True*, then *not()* makes it *False*. If the condition is *False* then *not()* makes it *True*.

To use it, type *not* and then place your conditions inside parenthesis. In the following example, if the user’s input is not *a*, *r*, or *f* then the script prints the message “Invalid input.”

```
inp = raw_input("Abort, Retry, Fail?")
if not( (inp == "a") or (inp == "r") or (inp == "f") ):
    print "Invalid input."
else:
    print "Valid input."
```

Tip: If you want to put another *if* statement inside an *if* statement, you can. Just remember to indent the second *if* statement with four spaces. This means that the code that runs if the second *if* statement is *True* is indented with eight spaces.

* * *

## Looping your Code

You can use loops to repeat sequences of Python commands a set number of times, or until something changes.

In Python, the *while* loop looks quite similar to an *if* statement. It repeats the indented code while the condition is *True*, and stops when the condition becomes *False*.

```
while raw_input("Abort, Retry, Fail?") == "r":
    pass
exit
```

Like the *if* statement, indenting the code is important. When the interpreter reaches code that is not indented, it treats this as the end of the loop.

The Python code above simulates the infamous “Abort, Retry, Fail?” error message from early versions of Microsoft DOS. Selecting *abort* or *fail* causes the program to end, but selecting *retry* only repeats the message.

Loops and *if* statements in Python cannot be empty. However, you can use the *pass* command to create loops that do nothing.

Tip: It is quite easy to accidently write an infinite loop in Python – a loop that never ends. To break an infinite loop, press Ctrl + C.

The *for* loop in Python is a little different from the one in C. It is primarily used for working with lists, tuples, and dictionaries, and is more similar to the *foreach* loop in languages such as PHP and C#.

```
f4 = ["Reed", "Ben", "Sue", "Johnny"]
for fantastic in f4:
    print fantastic
```

Each time the loop runs, Python copies the next item in the list into the variable *fantastic*. When there are no more items, the loop ends.

You can replicate the typical C-style *for* loop that counts from one number to another. In C, you create this loop using the code:

```
for (int count=0; count < 5; count++) {
    Serial.println(count);
}
```

The equivalent in Python is:

```
count = 0
while count < 5:
    print count
    count = count + 1
```

However, replicating the C-style loop is not recommended in the Pythonic style guidelines. Instead, you can use the *range()* function to create a special type of list and then use the *for* loop.

```
for count in range(0, 5):
    print count
```

In this example, *range(0, 5)* creates a list that contains the numbers 0, 1, 2, 3, and 4.

Finally, there are two commands that you can use inside a loop. These are ways to change how the loop runs.

| Command | Description |
| --- | --- |
| break | Immediately exits the loop. |
| continue | Jumps to the top of the loop, ignoring any other commands that are below the *continue* command. |

* * *

## Writing your Own Functions

In the examples so far, you have seen several functions that are built-in to Python. These include *len()*, *range()*, *print()*, and *raw_input()*.

You can also write your own functions.

Breaking your code up into smaller functions helps to make your scripts more readable and easier to work with. And when you begin working on a new project, you may find that some functions that you wrote in another script are useful in this one. It is easier to copy and paste a function from one script to another than it is to copy commands and variables from one long, continuous sequence of Python commands.

To define a new function, use the *def* keyword followed by a name, then empty parenthesis and a colon.

```
def myfunction():
```

The name of your function should follow the same rules as variable names – they should begin with a letter or underscore, and then may also include numbers in the characters that follow.

After the declaration, indent all of the code that you want to run in the function. For example:

```
def myfunction():
    print "This is my function."
    print "There are many like it,"
    print "But this one is mine."
```

When the Python interpreter reaches code that is not indented, it treats this as the end of the function.

The code in a function does not run until you call it. To call a function, specify its name followed by empty parenthesis.

```
myfunction()
```

When you use functions like *len()*, *range()*, and *raw_input()*, you pass in *arguments* to those functions to provide data for them to work on. You can give your own functions this same ability. To do this, you must define the parameters that your function accepts, in the function’s declaration.The example below defines a function that accepts one argument:

```
def inc(val1):
    val1 = val1 + 1
```

The next example accepts two arguments:

```
def add(val1, val2):
    val1 = val1 + val2
```

To call these functions, you need to include the extra information in parenthesis:

```
inc(x)
add(y, z)
```

These examples highlight one important difference between Python and other languages. When you pass a variable into a function, the Python interpreter actually sends a reference to that variable. It does not send a copy of the data. This means that functions like *inc()* and *add()* can permanently change the variables that you pass into them.

Doing this can be confusing; you should avoid changing arguments in your functions. Instead, you can copy the data to new variables, make the changes, and then *return* the new value.

```
def add(val1, val2):
    v1 = val1
    v2 = val2
    v1 = v1 + v2
    return v1
```

Or, to do this without specifically creating and setting any variables:

```
def add(val1, val2):
    return val1 + val2
```

With functions that return values, you can capture the result into a variable:

```
result = add(5, 7)
```

Tip: If you write a function that needs to return multiple values, you can return a tuple. For more information, see [Introducing Lists, Tuples, and Dictionaries](#part0006_split_003.html_tc3s3s3).

### Making Parameters Optional

Sometimes, you might want to write a function that has optional parameters. For example, you can combine the *inc()* and *add()* functions from the previous examples into a single function that adds *1* if you do not specify the second argument.

To do this: define both parameters in the function, but then specify a default value for the second.

```
def inc(val1, val2 = 1):
    return val1 + val2
```

You can call this function like this:

```
result = inc(5)
```

Or like this:

```
result = inc(5, 7)
```

If you only send one argument, then the Python interpreter uses the default value (*1*) for *val2*.

Whether you define a function with one, two, three, or more parameters, you can make parameters optional.

* * *

## Working with Classes and Objects

*Object-oriented programming* is a technique where variables and pieces of data are treated as standalone *objects*. Simple objects contain the values that you give to them, but also information about what type of object they are and even functions that only operate on that object.

When a function is declared inside an object, it is called a “method”.

The C compiler that translates Arduino sketches into executables that run on the Arduino, is actually a C++ compiler. C++ is a variant of C that includes features for working with objects. And so, as an Arduino user you are already using object-oriented programming.

In an Arduino sketch, this code tells the *Serial* object to run its *println()* method:

```
Serial.println("Hello Serial Monitor");
```

Python is also an object-oriented programming language.

In Python, string variables are instances of the string *class*. A class is a blueprint that specifies what information an object can hold, and what methods it implements. When you create an *instance* of a class, you create an object in memory that follows the structure that is set by that class.The string class contains several methods that you can use to create new strings by modifying existing ones, and several other methods that you may find useful.

| Method | Description |
| --- | --- |
| capitalize() | Returns a copy of the string, with the first letter in uppercase. |
| center(width) | Returns a copy of the string, padded with space characters so that the text appears centered. |
| count(seq) | Counts the number of times that the specified sequence of characters occurs in the string. |
| find(seq) | Finds the location (starting at zero for the first character) of the specified sequence of characters in the string. Returns *-1* if the sequence is not in the string. |
| lower() | Returns a copy of the string, with all characters in lowercase. |
| replace(seq1, seq2) | Returns a copy of the string with all instances of the first sequence of characters replaced by the second sequence of characters. |
| split() | Returns a list of strings – each word in the string. The default setting splits strings whenever there is a space. You can change this action by calling the *split()* method and passing another string. For example, to split a string into separate pieces every time there is a comma, call *mystring.split(",")* |
| strip() | Returns a copy of the string, without any spaces at the start or end. |
| upper() | Returns a copy of the string, with all characters in uppercase. |

You can tell an object to run a method by typing the name of the object, followed by a dot, and then the name of the method. For example:

```
mystring = "hello world!"
print mystring.capitalize() 
```

### Creating New Classes

When you work with numbers, lists, tuples, and so on, you create instances of classes that Python already knows. To create your own custom object, you must first define your own class and tell Python what an instance of this class can contain.

In the following examples, you will create and work with a new class called *Movie*. Objects of this type represent an individual movie, and contain multiple pieces of information about it.

1.  Login to the OpenWrt-Yun command line.
2.  To start a new script, type the following command then press **Enter**:

    ```
    nano /mnt/sda1/movietest.py
    ```

To define a new class, use the keyword *class* and then a name. Indent the contents of the class with four spaces. When the Python interpreter finds code that is not indented, it treats this as the end of the class.

Add the following code to the top of the Python script:

```
class Movie:
    title = None
    director = None
    year = None
```

Objects can contain multiple values, and this class definition specifies that objects based on the *Movie* class contain three variables. Variables that you create inside an object are called “fields”. The keyword *None* indicates that the field does not have a default value.

To create an instance of the *Movie* class and get a usable object, add the following line underneath the class definition (do not indent it):

```
house = Movie()
```

To set the information about this film, add the following code underneath the last line:

```
house.title = "House on Haunted Hill"
house.director = "William Castle"
house.year = 1959
```

Now add a *print* command to show the object to the user:

```
print house
```

The script should now look this like:

```
class Movie:
    title = None
    director = None
    year = None

house = Movie()
house.title = "House on Haunted Hill"
house.director = "William Castle"
house.year = 1959
print house
```

To run this script,

*   At the command prompt, type the following command and then press **Enter**:

    ```
    python /mnt/sda1/movietest.py
    ```

Instead of the information you are expecting, you will see an object reference in the terminal:

```
<__main__.Movie instance at 0x776daa58>
```

This is because the *print* command does not know how to work with your custom object – it expects a string. But you can add a method to the *Movie* class that returns a printable string.Underneath the line *year = None*, add the following code. Remember to indent this code because you want the method to be part of the *Movie* class.

```
 def info(self):
        return self.title + " (" + str(self.year) + ")"
```

And then change the line *print house* to:

```
print house.info()
```

Run the script again and the output is now “House on Haunted Hill (1959)”.

When defining methods, the first parameter must always be *self*. The *self* parameter allows the methods to refer to variables that are inside the current object. But notice that when you call the method later, you do not need to pass in anything. The Python interpreter handles all of this for you.

The script should now look like the following code.

```
class Movie:
    title = None
    director = None
    year = None

    def info(self):
        return self.title + " (" + str(self.year) + ")"

house = Movie()
house.title = "House on Haunted Hill"
house.director = "William Castle"
house.year = 1959
print house.info()
```

You can also use lists, tuples, dictionaries, and even other objects as fields in a class.

To extend the *Movie* class with a tuple that holds the names of actors in the movie, add the following line underneath *year = None*

```
 starring = None
```

And then add this line underneath *house.year = 1959*:

```
house.starring = ("Vincent Price", "Carol Ohmart", "Richard Long")
```

One of the reasons object-oriented programming is powerful, is that you now have a single variable *house* that contains all of the information that you want to hold about the movie, and also a method for displaying its title. And because objects can be assigned to variables, they can also be assigned to lists.Remove the line *print house.info()* and add the following code to the bottom of the file:

```
house2 = Movie()
house2.title = "House on Haunted Hill"
house2.director = "William Malone"
house2.year = 1999
house2.starring = ("Geoffrey Rush", "Famke Janssen", "Taye Diggs")
favorites = [house, house2]
```

The code above creates a second instance of the *Movie* class, and then adds the information for the 1999 remake of the first film.

The final line in that code creates a list and adds both objects to it. Because both of the objects in *favorites* are instances of *Movie*, they both contain the method *info()*. So you can display all of the titles in the *favorites* list using a *for* loop:

```
for mv in favorites:
    print mv.info()
```

And that code works regardless of how many different *Movie* objects you add into the list.

Here is the full script so far:

```
class Movie:
    title = None
    director = None
    year = None
    starring = None

    def info(self):
        return self.title + " (" + str(self.year) + ")"

house = Movie()
house.title = "House on Haunted Hill"
house.director = "William Castle"
house.year = 1959
house.starring = ("Vincent Price", "Carol Ohmart", "Richard Long")

house2 = Movie()
house2.title = "House on Haunted Hill"
house2.director = "William Malone"
house2.year = 1999
house2.starring = ("Geoffrey Rush", "Famke Janssen", "Taye Diggs")
favorites = [house, house2]
for mv in favorites:
    print mv.info()
```

### Inheriting Fields and Methods from Other Classes

One of the key concepts in object-oriented programming is that classes can borrow the structure of other classes. So rather than have an entirely new class for a new type of object called “TVShow” (which would duplicate many of the fields from *Movie*), you can create *TVShow*; inherit the structure from *Movie*; and then expand on it.

Underneath the class definition for *Movie*, define *TVShow* using the code below:

```
class TVShow(Movie):
    series = None
    season = None
    episode = None
```

You tell Python which class to inherit fields and methods from, by specifying its name in parenthesis after the name of the new class. In the code above, although you have only declared three fields, all of the fields from the *Movie* class are also available in *TVShow* objects.

In the script, before the line *favorites = [house, house2]*, add the following code:

```
tv = TVShow()
tv.title = "The Competition Begins"
tv.year = 2011
tv.starring = ("Abby Lee Miller", "Brook Hyland", "Maddie Ziegler-Gisoni")
tv.series = "Dance Moms"
tv.season = 1
tv.episode = 1
```

Change the line *favorites = [house, house2]* to read:

```
favorites = [house, house2, tv]
```

Then run the script again. Even though the *tv* object is a different type, the code that prints the contents of the *favorites* list does not know this. *TVShow* objects have the same *info()* method and so everything works.

### Overriding Inherited Methods

Any code that can work with *Movie* objects can also work with *TVShow* objects, because *TVShow* inherits from *Movie*. However, this does not mean that all of the methods in the *TVShow* class have to be exactly the same as the ones in the *Movie* class. You can add extra methods to *TVShow*, and even override the ones that it inherits from *Movie* with slightly different versions.

For example, underneath the line *episode = None*, add the following code:

```
 def info(self):
        return self.title + " (TV - " + str(self.year) + ")"
```

Then run the script again.

All objects in Python have several methods that you do not write or call explicitly, but that are used by the Python interpreter at various times. You can override these. For example, Python uses a built-in method *__str__* to try and convert an object to a string when using the *print* function.

Instead of having the method *info()* return a string, you can override *__str__*.

Change the two *def info(self):* lines to:

```
 def __str__(self):
```

And then change the line *print mv.info()* to:

```
 print mv
```

The table below shows a few of the other built-in methods that you might want to override.

| Method | Description |
| --- | --- |
| __repr__(self) | Should return a string version of the object, when a more formal conversion is required than that expected of *__str__*. |
| __lt__(self, other) | Should return *True* if the current object is less than the other object. Or *False* if it is not. |
| __le__(self, other) | Should return *True* if the current object is less than or equal to the other object. Or *False* if it is not. |
| __eq__(self, other) | Should return *True* if the current object is equal to the other object. Or *False* if it is not. |
| __ne__(self, other) | Should return *True* if the current object is not equal to the other object. Or *False* if it is not. |
| __gt__(self, other) | Should return *True* if the current object is greater than the other object. Or *False* if it is not. |
| __ge__(self, other) | Should return *True* if the current object is greater than or equal to the other object. Or *False* if it is not. |
| __cmp__(self, other) | Should return a negative integer if the current object is less than the other object, or a positive number if the current object is greater than the other object. If the two are objects are equal, the *__cmp__* method should return 0. |

You can override these methods and use them to create complicated objects that you can compare using the standard Python operators. For example, if you have a field *rating*, which holds an integer representing how good the movie or TV show is, you can use this to compare the objects.

Without overriding the built-in methods, you can do this using an *if* statement like:

```
if movie1.rating > movie2.rating:
```

But if you override the standard methods...

```
 def __gt__(self,other):
        return self.rating > other.rating
```

...then you can compare the objects by writing:

```
if movie1 > movie2:
```

By overriding the comparison methods, you can define what makes one object greater than another. This can be based on a combination of fields, not just one.

Tip: If you override one of the comparison methods, it is usually best to override them all.

In the examples so far, you initialize the fields of an object on individual lines after the object is created. But you can also initialize fields at the same time as you create the object. To do this, you need to override the built-in method *__init__*.

For example, to override *__init__* so that you set the *title* and *year* of a movie or TV show at the same time, add the following method override to the *Movie* class:

```
 def __init__(self, title, year):
        self.title = title
        self.year = year
```

Then when you create the object, pass in values for *title* and *year*:

```
house = Movie("House on Haunted Hill", 1999)
```

You can include as many initializers in the override for __init__ as you want to.

* * *

## Using Packages and Modules

A *module* is a collection of classes and functions that you can use in your projects instead of having to code everything yourself. This is the equivalent of using libraries and *#include* statements in Arduino C.

A *package* is a collection of modules.

There is large number of packages and modules available that extend the capabilities of Python on the Yún. Using these can save you many hours of programming time. Some of these modules work with very complicated Linux libraries that perform advanced tasks, such as: playing media files; communicating over a network or the Internet; storing and retrieving data from databases; and many more.

To save space on the Arduino Yún, very few Python packages and modules are installed. However, you can install others.

### Downloading and Installing Python Packages

You can use a program called “pip” to download and install Python packages from the Python Package Index website (PyPI – [https://pypi.python.org/pypi/](https://pypi.python.org/pypi/)), but you first need to install pip on your Arduino.

To use pip, you must install support for secure sockets layer (SSL) and the *easy_install* program. To install all of these programs:

1.  Login to the OpenWrt-Yun command line.
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    opkg update
    ```

3.  Type the following command and then press **Enter**:

    ```
    opkg install distribute
    ```

4.  Type the following command and then press **Enter**:

    ```
    opkg install python-openssl
    ```

5.  Type the following command and then press **Enter**:

    ```
    easy_install pip
    ```

pip works in a very similar way to the command-line package manager OPKG.

To list all of the Python modules that are on your Arduino,

*   Type the following command and then press **Enter**:

    ```
    pip list
    ```

You can also use the *list* command to show whether any of the Python modules on your Arduino need updating.

*   Type the following command and then press **Enter**:

    ```
    pip list --outdated
    ```

To search the Python Package Index, use the *search* command followed by a keyword. This command searches all of the titles and descriptions in the package index, and then shows a list of the ones that contain the keyword you type.

For example, to find all modules that work with MP3 files,

*   Type the following command and then press **Enter**:

    ```
    pip search mp3
    ```

To install a Python module, use the *install* command. For example, to install the *id3reader* module,

*   Type the following command and then press **Enter**:

    ```
    pip install id3reader
    ```

And then to uninstall this module,

*   Type the following command and then press **Enter**:

    ```
    pip uninstall id3reader
    ```

When you install Python modules using pip, the software copies all of the files that are needed into the appropriate Python module directory, and you can use them in your Python scripts immediately.

Tip: Not all of the modules on the Python Package Index can be used on the Arduino Yún. Many of them depend on Linux libraries or programs that are not yet available from the OpenWrt-Yun repository. You can find detailed information about each Python package on the PyPI website.

### Including a Module in a Python Script

In this short example, you use the *id3reader* module to read the song information from an MP3 file. You can find the documentation for *id3reader* at [http://nedbatchelder.com/code/modules/id3reader.html](http://nedbatchelder.com/code/modules/id3reader.html)

Install the *id3reader* module using the instructions in [Downloading and Installing Python Packages](#part0006_split_008.html_tc3s8s1). Then copy an *.mp3* file over to the SD card on the Arduino Yún.

Start a new Python script, and then add the following command to the top of the file:

```
import id3reader
```

The *import* command tells the Python interpreter to load a module because your script uses it.

To actually use the *id3reader* module, you need to create an instance of the *Reader* class and pass in the file name and file path of your MP3 file.

```
id3 = id3reader.Reader("/mnt/sda1/Track 01.mp3")
```

To tell the *Reader* object to return a specific piece of information, use the method *getValue()* and pass in the name of the information that you want.

| Value | Description |
| --- | --- |
| title | The song title. |
| performer | The name of the artist who recorded the song. |
| album | The name of the album that the song appears on. |
| year | The year the song (or album) was released. |
| track | The track number. |

For example, to show a summary of the information about the song:

```
import id3reader
id3 = id3reader.Reader("/mnt/sda1/Track 01.mp3")
print id3.getValue("track") + " - " + id3.getValue("title")
print "Artist: " + id3.getValue("performer")
print "Album: " + id3.getValue("album") + " (" + id3.getValue("year") + ")"
```

You can also import modules and give them a different name by using the keyword *as*. This changes the way you create an instance of the class:

```
import id3reader as ID3
myID = ID3.Reader("/mnt/sda1/Track 01.mp3")
```

And you can be very specific about what you want to import. For example:

```
from id3reader import Reader as ID3
id3 = ID3("/mnt/sda1/Track 01.mp3")
print id3.getValue("track") + " - " + id3.getValue("title")
print "Artist: " + id3.getValue("performer")
print "Album: " + id3.getValue("album") + " (" + id3.getValue("year") + ")"
```

The keyword *from* tells the Python interpreter that you only want to import one specific class from the *id3reader* module.

When modules are grouped into packages, you use the *from* keyword to tell the interpreter which module you want from the package:

```
from packagename import modulename
```

Tip: You will usually need to find the documentation for the package that you install in order to learn what modules are available and how to use them.

* * *

## Reading and Writing to Files

On the Arduino Yún, the ability to create, read, and write files is especially important because it is also how you communicate with many of the Yún’s features.

Python has built-in support for working files of two types: text files, and binary files. The difference between the two is that when you open a file as a text file, Python handles line breaks and character encodings for you. When you open a file as a binary file, you have raw access to the bytes that it comprises of.

### Opening a File

To open a file in Python, use the *open()* function and pass in the file name (and file path unless the file is in the current working directory):

```
myfile = open("/mnt/sda1/test.txt")
```

By default, Python tries to open the file as a read-only text file. If you want to open the file for writing, or as a binary file, you need to pass in an additional argument to the *open()* function. This is the *mode*, and it can be one of several values:

| Mode | Description |
| --- | --- |
| r | Open a text file for reading. |
| rb | Open a binary file for reading. |
| w | Open a text file for writing. This overwrites the existing file or, if it does not exist, creates the file. |
| wb | Open a binary file for writing. This overwrites the existing file or, if it does not exist, creates the file. |
| a | Open a text file for “appending”. Anything you write is added to the end. If the file does not exist, Python creates the file. |
| ab | Open a binary file for “appending”. Anything you write is added to the end. If the file does not exist, Python creates the file. |

The *open()* function returns an object that represents the open file. You need to save this object in a variable so that you can work with the file.

You should always close files. Closing the file ensures that any changes you make are saved, and allows other programs to access the file. To close a file, call the *close()* method of the object:

```
myfile.close()
```

### Reading from Files

To read from a file, you need to open it using one of the modes that support reading (usually *r*, or *rb*).

When working with a text file, Python has several methods that you can use.

| Method | Description |
| --- | --- |
| read() | Reads all of the text from the file and returns the information as a string. |
| readline() | Reads a single line (up to a line break) from the file and returns the information as a string. |
| readlines() | Reads all of the text from the file, and returns a list of strings. Each item in the list is a single line from the text file |

These are methods of the file object that you receive from a call to *open()*. The following Python code displays the text from the file */etc/passwd* in the console:

```
myfile = open("/etc/passwd", "r")
print myfile.read()
myfile.close()
```

The *read()* method also accepts an argument that tells the Python interpreter how many characters you want to read from the file. When the string returned by *read()* is empty (or has a length of zero) then you have reached the end of the file.

Python automatically keeps track of where you are in the file. So you can repeatedly call *read()* with an argument, or *readline()*, to read the file piece by piece.

The example below prints each character from the */etc/passwd* file on its own line.

```
myfile = open("/etc/passwd", "r")
while True:
    tx = myfile.read(1)
    if len(tx) == 0:
        break
    else:
        print tx
myfile.close()
```

When working with binary files, you also use the read() function. But it usually does not make sense to use *readline()* or *readlines()* with binary files.

To read a binary file (or a predefined number of bytes from a binary file) into an array, or “buffer”, you need to create a special type of object – a *bytearray*. You can then use the file method *readinto()*to fill the buffer with the contents of the binary file.

For example, to read the first ten bytes of the */etc/passwd* file into a buffer:

```
myfile = open("/etc/passwd", "rb")
buf = bytearray(10)
myfile.readinto(buf)
myfile.close()
```

The value returned by *readinto()* is a number that tells you how many bytes were read from the file. When this number is zero, you have reached the end of the file. At the end of this script, *buf* contains ten bytes. You can access each byte using square brackets and the number of the byte (starting at zero for the first) that you want to extract:

```
print buf[0]
```

### Writing to Files

To write to a file, you first need to open it with a mode that supports writing (*w*, *wb*, *a*, or *ab*). Then you can call the *write()* method of the open file, and pass in a string that contains the text that you want to write to the file. If you open the file using mode “a”, the text is written to the end of the file, after any existing content. If you open the file using mode “w” then the file is automatically wiped when Python opens it.

Writing strings to binary files can cause unexpected results. The code below does not write the number 65 to a binary file, it actually writes two bytes to the file: the ASCII code for the character that looks a 6 (which is 54), and then the ASCII code for the character that looks like a 5 (which is 53).

```
myfile.write("65")
```

If you do want to use a string, but need to ensure that the script writes the correct number to the file, you can use the escape sequence *\x* and then include the number in hexadecimal notation. For example:

```
myfile.write("\x41")
```

The preceding command writes the number 65 (which is 41 in hexadecimal) to the file as a single byte. But if you are working with numbers in your Python script, it is usually easier and clearer to write to a binary file using a *bytearray* object. The code below demonstrates one way to create a *bytearray* with five values in it and then write it to a file.

```
buf = bytearray(5)
for x in range(0, 5):
    buf[x] = x
myfile = open("/mnt/sda1/test.dat", "wb")
myfile.write(buf)
myfile.close()
```

### Managing Files and Directories in Python

The *os* module contains many functions for working with files and directories from your Python script. To use this module, add the following *import* statement to the top of a script:

```
import os
```

The table below shows some of the functions that you can use. Remember to prefix them with *os* and a dot, to call them from your Python scripts.

| Method | Description |
| --- | --- |
| listdir(path) | Returns a list of the contents of the specified directory. |
| makedirs(path) | Creates a new directory at the specified path, and any directories above it that do not exist yet. |
| mkdir(path) | Creates a new directory at the specified path. |
| remove(path) | Deletes the specified file. |
| removedirs(path) | Deletes the specified directory and everything inside it. |
| rename(path, path) | Changes the name of, or moves, a directory from the first file path, to the second. |
| system(command) | Runs the specified Linux command-line command. |
| urandom(length) | Returns a random string of the length specified. |

* * *

## Handling the Errors in Scripts

If you make a mistake in your script or a Python command causes an error, the Python interpreter stops your program and displays the error message. However, even perfect code can sometimes cause an error that you cannot prevent or predict. This is especially true when communicating with systems that you do not have full control over.

You can stop the interpreter from terminating your program by handling the error yourself. The basic way of doing this, is to use the *try* and *except* statements. Place a *try* statement before any code that might cause an error, and then indent the code. Then use *except* to specify what happens if an error occurs.

For example:

```
try:
    myfile = open("/mnt/sda1/test.txt", "r")
    myfile.close()
except:
    print "File does not exist"
```

If the file */mnt/sda1/test.txt*does not exist then trying to open it in read-only mode causes an error. In the example above, the error is caught and the Python interpreter runs the code indented below *except*. If there is no error, the interpreter does not run the code indented below *except*.

* * *

## Compiling your Python Programs

The Python interpreter is installed on all Arduino Yúns, unless you specifically remove it. On rare occasions, it may be useful to compile your Python programs so that they can run on an Arduino Yún without the Python interpreter.

*cx_Freeze* is a tool that translates Python scripts (and any modules that they rely on) into native executables. It is available from the Python Package Index. However, the installation of Python on the Yún is missing several files that cx_Freeze needs, so you need to add these files to your system before installing the tool.

To install cx_Freeze,

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    opkg install binutils
    ```

2.  Type the following command and then press **Enter**:

    ```
    opkg -t /root install yun-gcc
    ```

3.  Install easy_install and pip, as described in [Downloading and Installing Python Packages](#part0006_split_008.html_tc3s8s1).
4.  Type the following command and then press **Enter**:

    ```
    cd /usr/lib
    ```

5.  Type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/download/libpython2.7.a
    ```

6.  Type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/libz.so.1.2.7
    ```

7.  Type the following command and then press **Enter**:

    ```
    ln -s /usr/lib/libz.so.1.2.7 /usr/lib/libz.s
    ```

8.  Type the following command and then press **Enter**:

    ```
    pip install cx_Freeze
    ```

Because of the way cx_Freeze works, you need to compile your Python script in a directory that you have full control over. You can move it again after compiling the script. If you expand the Linux file system to the SD card, then the best place to put your script is in */root*. If you are not using the SD card this way, put your Python script in */www* or */mnt/sda1/arduino/www*.

To start the build process and compile a script called *hello.py*,

*   At the command prompt, type the following command and then press **Enter**:

    ```
    cxfreeze hello.py
    ```

You can usually ignore any warnings relating to the command *ldd*.

To run the executable,

*   At the command prompt, type the following command and then press **Enter**:

    ```
    dist/hello
    ```

cx_Freeze builds the project into a directory named “dist”. Inside this directory, you can find a file that has no file extension. This is the executable (*hello*). The other files in the *dist* directory are libraries that you need to distribute with the executable.

If you create a symbolic link in */usr/bin/* that links to the executable, then you can run the program from anywhere by typing its name. To learn about creating symbolic links, see [Creating and Removing Symbolic Links](#part0005_split_002.html_tc2s2s4).

Even though cx_Freeze includes the command line tool, you have more control over the conversion to an executable if you use a small Python script. For more information about using cx_Freeze and how to control its output, see the webpage [http://cx-freeze.sourceforge.net/](http://cx-freeze.sourceforge.net/)

# Using the Bridge Library

The two processors on the Arduino Yún can communicate with each other over a hardware serial port. To communicate with the AR9331 from the ATmega32u4, you need to program it with an Arduino sketch that sends the right messages.

In the Arduino integrated development environment (IDE), the Bridge library is a collection of classes and functions that simplifies how to do this. It also contains built-in mechanisms to detect and handle errors that may occur when the two processors attempt to talk to each other.

As the Wi-Fi and Ethernet adaptor, USB hosting, and SD card facilities are all controlled by the AR9331, you can use the Bridge library to access these features from the Arduino side of the Yún.

Using the Bridge library gives control of your project to the ATmega32u4 and your Arduino sketch. Your sketch initiates communication with the Linux side, and tells it what to do. To have the Linux side take more control of the project, you can have the Arduino start the communication but then loop and wait for instructions from the AR9331.

Tip: Many of the examples in this chapter use the *Serial* class to send messages to the Arduino IDE. Connect your Yún to your PC using a USB cable to use these code samples.

In This Chapter

[Creating a Link between the ATmega32u4 and the AR9331](#part0007_split_000.html_tc4s1)

[Storing Data in the AR9331’s Memory](#part0007_split_001.html_tc4s2)

[Running Commands and Scripts](#part0007_split_002.html_tc4s3)

[Working with Files in the Linux File System](#part0007_split_003.html_tc4s4)

[Making a Console Connection](#part0007_split_004.html_tc4s5)

[Using Mailbox and Sending Messages](#part0007_split_005.html_tc4s6)

[Communicating over Local Networks and the Internet](#part0007_split_006.html_tc4s7)

[Choosing a Connection Method](#part0007_split_007.html_tc4s8)

* * *

## Creating a Link between the ATmega32u4 and the AR9331

When OpenWrt-Yun loads, it starts a program that waits for communication from the Arduino side. OpenWrt-Yun is capable of running many programs at the same time – so it can load Linux, run scripts, and accept SSH connections, regardless of whether the ATmega32u4 sends any messages or not.

To start the communication between the ATmega32u4 and the Atheros AR9331, you need to use the Bridge library. And so you need to include it in your Arduino sketch.

*   At the top of your Arduino sketch, add the following line:

    ```
    #include <Bridge.h>
    ```

Then make a connection to the AR9331 by using the *begin()* method of the Bridge class. The most-common place to do this is in your sketch’s *setup()* function.

```
void setup() {
    Bridge.begin()
}
```

You do not need to create an instance of *Bridge* to do this, you can call the *begin()* method directly.

It usually takes several seconds to make the connection. However, when you first apply power to the Arduino, this process takes considerably longer as *begin()* must wait until the Linux side loads OpenWrt-Yun. None of your code underneath the call to *begin()* runs until the connection to the AR9331 completes.

When *begin()* completes, the connection between the ATmega32u4 and the AR9331 is ready to use and will remain usable until the Arduino is turned off.

The *Bridge* class contains several methods.

| Method | Description |
| --- | --- |
| readMessage() | Reads a message from the AR9331. |
| writeMessage() | Sends a message from the ATmega32u4 to the AR9331. |
| MessageAvailable() | If the AR9331 sends a message to the ATmega32u4 then this method returns the length of the message. |
| transfer() | Sends a message from the ATmega32u4 to the AR9331, waits for a response, and then ensures that the response is correct. If there is an error in the transmission, *transfer()* resends the message. |

You rarely need to use these in your sketches – they are for working with Bridge communications at a very low level. Other classes in the Bridge library rely on these methods and simplify the processes for you.

However, there are two methods in the Bridge class that you might want to use: *put()* and *get()*. You can use these to store data in the AR9331’s memory and then retrieve it later.

* * *

## Storing Data in the AR9331’s Memory

The ATmega32u4 on the Arduino side only has 2.5 KB of internal RAM for storing your variables and temporary information. The Atheros AR9331 on the Linux side has 64 MB, although OpenWrt-Yun uses a lot of this.

If you need more memory on the Arduino side then you can use the Bridge library to store information in the AR9331’s memory instead.

Storing and retrieving information from the AR9331’s memory is slower than using the RAM on the ATmega32u4\. And when you turn off the Yún or reboot the AR9331, this information is lost. Resetting the ATmega32u4 or restarting the sketch does not affect the values stored on the AR9331.

If you want to find out how much unused memory the Linux side of your Arduino Yún has, you can do this either from the OpenWrt-Yun command line or from the advanced configuration panel.

To access the information (in kilobytes) from the command line:

1.  Login to the OpenWrt-Yun command line. For more information, see [Connecting to the Arduino Yún](#part0005_split_000.html_tc2s1).
2.  Type the following command and then press **Enter**:

    ```
    free
    ```

To access the information from the advanced configuration panel:

1.  Login to the Arduino web panel and open the advanced configuration panel. For more information, see [Opening the Advanced Configuration Panel](#part0004_split_004.html_tc1s5).
2.  Click the **Status** tab.
3.  Click **Overview**.
4.  Make a note of the values in the **Memory** section.

There are two methods in the Bridge library that you can use for storing your data in the AR9331’s memory:

| Method | Description |
| --- | --- |
| put(name, String) | Sends a *String* to the AR9331 and stores it in memory using the specified name. |
| get(name, buffer, length) | Finds the data with the specified name and copies *length* bytes from the AR9331 to the buffer (an array or area of memory). |

*put()* only stores strings, and so if you want to store other types then you must first convert them to a string. Like variable names, the names that you use with *put()* should be unique for each value that you want to store.

### Storing Strings

To store a string, pass a *String* object or char array into *put()*.

For example:

```
Bridge.put("my_variable", "This is a string!");
```

Or:

```
char[] my_string = "This is a string!";
Bridge.put("my_variable", my_string);
```

To retrieve a string from the AR9331’s memory, you need to create a buffer – an array or area of memory in which the *get()* method can store the data.

The call to *get()* expects three arguments:

```
Bridge.get( key, buffer, length );
```

*   *key* is the name that you gave the value when you added it to the AR9331’s memory using *put()*.
*   *buffer* is the name of an array or area of memory in which to store the string.
*   *length* is the maximum size of the buffer, or the maximum number of bytes that you want to fetch from the AR9331.

If you define the buffer as a char array, you can generally treat it as a string.

For example:

```
#include <Bridge.h>

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    Bridge.put("my_variable", "This is a string!");
}

void loop() {
    char buf[100];
    Bridge.get("my_variable", buf, 100);
    Serial.println(buf);
    delay(5000);
}
```

Upload this sketch to your Arduino, and then open the Serial Monitor in the Arduino IDE.

Tip: Unlike other Arduinos, opening the Serial Monitor does not restart the Arduino Yún. The line *while (!Serial);* forces the Arduino to wait until the Serial Monitor opens before the remainder of the sketch runs.

To re-run the sketch: close the Serial Monitor, press the 32U4 RST button twice, and then reopen the Serial Monitor.

### Storing Numbers

The *char* type holds ASCII characters and numbers from 0 through 255\. A byte is the same and you can convert it to a char by including the keyword *char* in parenthesis before the name of a byte or byte variable.

```
byte x = 10;
char y = (char)x;
```

To store a char type using *put()*, you can use the *String()* function to convert it to a string. For example:

```
void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    char x = 10;
    Bridge.put("my_variable", String(x));
}
```

When retrieving the value using *get()*, you only need the first item (the first byte) in the buffer array:

```
char buf[100];
Bridge.get("my_variable", buf, 1);
char x = buf[0];
```

On the Arduino, other types of number use more than one byte. For example, an integer comprises two bytes. You can use the *String()* function to pass these into *put()*, and then convert the entire contents of the buffer to an integer using the function *atoi()*.

For example:

```
#include <Bridge.h>

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    int x = -10;
    Bridge.put("x", String(x));
}

void loop() {
    char buf[100];
    Bridge.get("x", buf, 100);
    int x = atoi(buf);
    Serial.println(x);
    delay(5000);
}
```

To convert the buffer string to a float, use the function *atof()*. Or to convert the buffer to a long integer, use *atol()*.

### Storing Arrays

Storing arrays is a little more complicated because you cannot use the *String()* function. *put()* expects that the strings that you pass in are null-terminated – that the last entry is zero. This means that if you have any zeroes in an array and you convert it to a string using *String()*, the string ends early.

To handle this, you need to convert the array to a string in which all zeroes are changed to something else. There are many ways of doing this, but in this section you will see how to convert the array to a base16 string.

Base16 encoding divides each byte of the source item into two halves – each half is four bits. The process then adds on a value to each half so that the result is safe for use in strings. Each half is then written out as a new byte.This doubles the size of the array, but it is relatively simple to implement.

In the example below, the code defines a new function called “store”. This function creates a new buffer that is twice the size of the one that you pass into it (plus an additional byte for the final zero).

When you pass arrays into functions, they become more difficult to work with. The *store()*function cannot detect how large the array is and so you have to pass this size as an argument.For each byte in the array, *store()* first extracts the highest four bits and adds the character ‘A’ (65) to that. Then it extracts the lowest four bits and adds ‘A’. Finally it converts the new array to a string and sends it to the AR9331\. This process ensures that all of the values are represented by ASCII letters.

```
void store(String key, char ar[], int sz) {
    char *buf = (char *)malloc((sz * 2)+ 1);
    if (buf != NULL) {
        int count = 0;
        byte b;
        for (int i=0; i<sz; i++) {
            b = ar[i];
            buf[count++] = ((b >> 4) & 0x0F) + 65;
            buf[count++] = (b & 0x0F) + 65;
        }
        buf[count] = 0;
        Bridge.put(key, String(buf));
        free(buf);
    }
}
```

In order to support arrays of different sizes, this example function uses dynamic memory management (*malloc*, and *free*) to work with the new buffer space.

When using the *get()* method to retrieve the value from the AR9331, your buffer needs to be twice as large as the original object that you store. The *retrieve()* function below is an example of how to reverse the process and fetch a value from the AR9331.

```
void retrieve(const char *key, char *dest, int sz) {
    char *buf = (char *)malloc(sz * 2);
    if (buf != NULL) {
        Bridge.get(key, buf, sz * 2);
        int count = 0;
        for (int i=0; i < sz * 2; i=i+2) {
            dest[count++] = ((buf[i] - 65) << 4) | (buf[i+1] - 65);
        }
        free(buf);
    }
}
```

The next example sketch creates a char array with a zero in the middle. This causes problems when using the *String()* function and so the sketch uses *store()* to encode the data into base16, and stores the result on the AR9331 as a string. The *retrieve()* function reverses this – fetching the encoded string from the AR9331 and decoding it back into an array.

```
#include <Bridge.h>

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    Serial.println("Storing array...");
    char myarray[5] = {1, 2, 0, 4, 5};
    store("myarray", myarray, 5);
}

void store(String key, char ar[], int sz) {
    char *buf = (char *)malloc((sz * 2)+ 1);
    if (buf != NULL) {
        int count = 0;
        byte b;
        for (int i=0; i<sz; i++) {
            b = ar[i];
            buf[count++] = ((b >> 4) & 0x0F) + 65;
            buf[count++] = (b & 0x0F) + 65;
        }
        buf[count] = 0;
        Bridge.put(key, String(buf));
        free(buf);
    }
}

void retrieve(const char *key, char *dest, int sz) {
    char *buf = (char *)malloc(sz * 2);
    if (buf != NULL) {
        Bridge.get(key, buf, sz * 2);
        int count = 0;
        for (int i=0; i < sz * 2; i=i+2) {
            dest[count++] = ((buf[i] - 65) << 4) | (buf[i+1] - 65);
        }
        free(buf);
    }
}

void loop() {
    Serial.println("Fetching array...");
    char buf[5];
    Bridge.get("myarray", (char *)buf, 5);
    for (int i=0; i<5; i++) {
        Serial.println(buf[i], DEC);
    }
    delay(15000);
}
```

To store an integer array, you can use exactly the same functions. However, as an integer is a 16-bit number, if there are five items in the array then the size is 10 bytes. You need to keep this in mind when passing in values for the *sz* parameter.

```
int myarray[5] = {1000, 2000, 3000, 4000, 5000};
store("myarray", (char *)myarray, 10);
retrieve("myarray", (char *)buf, 10);
```

### Storing Structs

Storing a struct is similar to the process for storing an array. In fact, you can use the same *store()* and *retrieve()* functions as the previous example.

```
#include <Bridge.h>

struct CMD {
    char reserved[3];
    byte opcode;
    int length;
}

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    CMD myCmd;
    myCmd.reserved[0] = 'C';
    myCmd.reserved[1] = 'M';
    myCmd.reserved[2] = 'D';
    myCmd.opcode = 0;
    myCmd.length = 255;
    store("myCMD", (char *)&myCmd, sizeof(myCmd));
}

void store(String key, char ar[], int sz) {
    char *buf = (char *)malloc((sz * 2)+ 1);
    if (buf != NULL) {
        int count = 0;
        byte b;
        for (int i=0; i<sz; i++) {
            b = ar[i];
            buf[count++] = ((b >> 4) & 0x0F) + 65;
            buf[count++] = (b & 0x0F) + 65;
        }
        buf[count] = 0;
        Bridge.put(key, String(buf));
        free(buf);
    }
}

void retrieve(const char *key, char *dest, int sz) {
    char *buf = (char *)malloc(sz * 2);
    if (buf != NULL) {
        Bridge.get(key, buf, sz * 2);
        int count = 0;
        for (int i=0; i < sz * 2; i=i+2) {
            dest[count++] = ((buf[i] - 65) << 4) | (buf[i+1] - 65);
        }
        free(buf);
    }
}

void loop() {
    CMD bCmd;
    retrieve("myCMD", (char *)&myCmd, sizeof(myCmd));
    Serial.println(bCmd.length);
    delay(5000);
}
```

Both arrays and structs are pointers to areas of memory. And so in the call to *store()* and the call to *retrieve()* you only need to tell the C compiler to treat the struct as a suitable buffer. The *&* prefix on *myCmd* fetches the memory address of the structure, and then *(char *)* tells the compiler that the content at that address is actually comprised of char types.

### Accessing Stored Data from Python Scripts

Python scripts on the Linux side of the Yún can also access this shared-storage area. This can be a useful way of exchanging information between the two processors on the Yún.

OpenWrt-Yun includes several Python scripts that assist in making the Bridge library work. The *BridgeClient* class is able to work with the shared-storage area in much the same way as the Arduino sketch.

To use the *BridgeClient* class, you need to add it to Python’s path so that you can import it:

```
import sys
sys.path.insert(0, "/usr/lib/python2.7/bridge/")
from bridgeclient import BridgeClient
```

Then you can create an instance of *BridgeClient*:

```
client = BridgeClient()
```

There are three methods that you can use to store, retrieve, and delete information the shared-storage area from your Python scripts:

| Method | Description |
| --- | --- |
| get(key) | Gets the value of the specified item. |
| put(key, value) | Adds a value to the storage area and identifies it with the specified key. |
| delete(key) | Deletes the item that has the specified string as its key. |

To call one of these methods, start with the name of an instance of the *BridgeClient* class and then a dot. For example:

```
client = BridgeClient();
cmd = client.get("myCMD")
```

And:

```
client.put("myIDX", 25)
```

Tip: Architecture differences between the ATmega32u4 and the Atheros AR9331 can make it difficult to store complicated structures and arrays on one processor and retrieve them on the other. To use the AR9331’s memory to pass data between the two processors, it is usually best to use String objects.

* * *

## Running Commands and Scripts

The Bridge library’s *Process* class contains methods for starting Linux commands on the AR9331 from an Arduino sketch running on the ATmega32u4\. You can use this to start shell scripts and Python programs.

To run a Linux command from an Arduino sketch, you need to create an instance of the *Process* class:

```
Process p;
p.begin("ls");
```

*begin()* specifies which command to run. However, the command does not run yet.

On the Linux command line, you send parameters to commands by placing them on the same line as the command, and separating each parameter with a space. When using the *Process* class, add each parameter to the instance using the method *addParameter()*.

```
p.addParameter("-l");
p.addParameter("/");
```

The code so far creates a *Process* object to run the command *ls -l /* on the AR9331 and list the contents of the top-level directory.

To run the command, call the method *run()*. This method returns the exit code of the Linux process as an integer. Most Linux programs return zero if they run without an error.

However, in most cases, the exit code is not the information that you want. When you run *ls* from the command prompt, it displays the information in the console. When you run *ls* from a *Process* object, the information is in a buffer that you need to read from. There are two methods to help you do this: *available()* and *read()*.

*available()* returns true if there is data waiting for you, and false if there is not.

*read()* fetches one byte from the buffer and returns it as an integer. It returns -1 when you reach the end.

The example sketch below reads the output of the *ls* command and writes it to the Serial Monitor.

```
#include <Bridge.h>

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    Process p;
    p.begin("ls");
    p.addParameter("-l");
    p.addParameter("/");
    p.run();

    if (p.available()) {
        while (p.available()) 
            Serial.write(p.read());
        }
        Serial.println();
    }
}

void loop() {
}
```

You can run shell scripts and Python programs in a similar way. However, the *run()* method is intended to run binary programs. And so to run a script, you need to run the command that understands those script files:

*   For a shell script, place “sh” in the call to *Process.begin()*, and add the script’s file path and file name as a parameter;
*   For Python programs, place “python” in the call to *Process.begin()*, and add the script’s file path and file name as a parameter.

There are several other occasions when you have to use “sh” in *Process.begin()* so that the system can understand your command:

*   When you want to run multiple commands and redirect the output of one, to another; and
*   When you want to use environment and shell variables in your command or parameters.

The *Process* class has two additional methods to make using shell command lines easier: *runShellCommand()* and *runShellCommandAsynchronously()*. Both of these methods accept a string, and this string is the entire command and its parameters. You do not call *begin()* or *addParameter()* when using these two methods.

### Running Commands and Scripts Asynchronously

When you start a command or script with *Process.run(),* the Arduino waits for the command to finish before it runs any other commands in the sketch.

However, you can use the method *runAsynchronously()*to tell the Arduino sketch not to wait. This is useful when:

*   You want to run multiple Linux commands at the same time; or
*   The ATmega32u4 has other work to do before it needs the result of the Linux command.

After you start a command with *runAsynchronously()*, you can periodically check whether the command is finished. To do this, use the method *running()*, which returns true if the command is still running or false if it is finished. Then you can fetch the exit code using the *exitValue()*method.

The example below tells the Linux package manager to download a list of all of the software that is available on the Arduino Yún repository. This can take several seconds. While it is happening, the sketch flashes the Yún’s built-in LED on digital pin 13.

When the update is complete, the sketch checks the exit code and then fetches the output of the command.

```
#include <Bridge.h>

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    Process p;
    p.begin("opkg");
    p.addParameter("-l");
    p.addParameter("/");
    p.runAsynchronously();

    while (p.running()) {
        digitalWrite(13, HIGH);
        delay(100);
        digitalWrite(13, LOW);
        delay(100);
    }
    if (p.exitValue() == 0) {
        if (p.available()) {
            while (p.available()) {
                Serial.write(p.read());
            }
            Serial.println();
        }
    }
}

void loop() {
}
```

Many commands (such as this one) send messages to the console while they are in progress. You do not need to wait until the command is finished before you read the output.

You can modify the example above so that the sketch picks up messages as quickly as it can:

```
void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    Process p;
    p.begin("opkg");
    p.addParameter("-l");
    p.addParameter("/");
    p.runAsynchronously();

    while (p.running()) {
        digitalWrite(13, HIGH);
        delay(100);
        digitalWrite(13, LOW);
        delay(100);
        while (p.available()) {
            Serial.write(p.read());
        }
    }
    if (p.exitValue() == 0) {
        Serial.println();
    }
}
```

Tip: After starting a command using *runAsynchronously()*, you can wait as long as you like before checking whether the command is finished.

### Sending Information to Running Commands

When you start a command or script using *runAsynchronously()*, you can also write information to it. For example, in [Getting Input from the User](#part0005_split_005.html_tc2s5s8), you can see the following shell script:

```
echo "Are you sure you want to continue? (yes/no):"
read response
if [ "$response" = "yes" ]; then
     echo "OK. I will continue."
else
     echo "OK. I will stop here."
fi
```

When the script runs the *read* command, it waits for keyboard input from the user. When you start this script from a *Process* object in an Arduino sketch, the command waits for input from the *Process* object instead. You can send this using the *write()* method.

1.  Login to the OpenWrt-Yun command line.
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/test.sh
    ```

3.  Type in the shell script code above.
4.  Press **Ctrl + X**.
5.  Press **Y**.
6.  To test the script, type the following command and then press **Enter**:

    ```
    /mnt/sda1/test.sh
    ```

To build an Arduino sketch that automates this shell script, start a new sketch in the Arduino IDE and type in the following code:

```
#include <Bridge.h>

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    Process p;
    p.runShellCommandAsynchronously("/mnt/sda1/test.sh");

    while (p.running()) {
        if (p.available()) {
            int x = p.read();
            Serial.write(x);
            if (x == ':') {
                p.write('n');
                p.write('o');
                p.write((byte)10);
            }
        }
    }
    while (p.available()) {
        Serial.write(p.read());
    }
    Serial.println("END.");
}

void loop() {
}
```

This code reads the output of the shell script and writes it to the Serial Monitor. When it receives the character ‘:’, it answers the question by sending the string “no”. Because the Linux *read* command waits for the Enter key, the script sends a line feed character (10).

You should note that it is possible for the script to finish before the Arduino has been able to read all of the script’s output. This is why there is a final *while* loop in the example above that reads from the buffer.

Tip: At the time of writing, there are a few bugs in the *write()* method. It is currently better to send bytes to the command individually, rather than try to send strings.

### Stopping a Command or Script

If you start a command or script that either never ends, or that seems to be broken, you can stop it using the *close()* method of the *Process* object.

For example:

```
Process p;
p.runShellCommandAsynchronously("/mnt/sda1/test.sh");
p.close();
```

* * *

## Working with Files in the Linux File System

The *File* and *FileSystem* classes in the Bridge library are very similar to the ones that you use to read and write files on an SD card using shields such as the Arduino Ethernet shield. On the Arduino Yún, you can use these classes to make changes to the OpenWrt-Yun Linux file system, or to store information on the microSD card.

The *File* and *FileSystem* classes are almost the same as the classes that you use with the Arduino SD library. However, there are a few small inconsistencies. Do not assume that code that works for the SD library will always compile when using Bridge.

For more information about the structure of the Linux file system on the Arduino Yún, see .

Before you can open or create files from an Arduino sketch, you need to initialize the connection to the Linux file system.

1.  At the top of your sketch, include the *Bridge* and *FileIO* header files:

    ```
    #include <Bridge.h>
    #include <FileIO.h>
    ```

2.  In your sketch’s *setup()* function, connect to the Linux file system using the command:

    ```
    FileSystem.begin();
    ```

The connection to the Linux file system remains open for as long as the sketch runs. You do not need to close this connection when you finish using it.

There are five methods of the *FileSystem* class that you can use to work with the file system:

| Method | Description |
| --- | --- |
| exists(filename) | Returns true if the specified file or directory exists, or false if it does not. |
| mkdir(directory) | Creates a directory at the specified path. If any directories in the path do not exist, *mkdir()* creates them too. |
| rmdir(directory) | Deletes the specified directory – if it is empty. |
| remove(filename) | Deletes the specified file. |
| open(filename, mode) | Opens a file for reading or writing. For more information, see [Opening or Creating a File](#part0007_split_004.html_tc4s4s1). |

You do not need to create an instance of the *FileSystem* class to work with these methods – you can call them directly.

For example, to create a directory named “TestDir” (and its parent, *Test*) on the microSD card:

```
#include <Bridge.h>
#include <FileIO.h>

void setup() {
    Bridge.begin();
    FileSystem.begin();
    FileSystem.mkdir("/mnt/sda1/Test/TestDir");
}

void loop() {
}
```

You can delete these directories by logging in to the OpenWrt-Yun command line over SSH, or by creating an Arduino sketch that calls the *rmdir()* method twice:

```
FileSystem.rmdir("/mnt/sda1/Test/TestDir");
FileSystem.rmdir("/mnt/sda1/Test");
```

### Opening or Creating a File

To open an existing file so that your Arduino sketch can read or write to it, use the *open()* method of the *FileSystem* class.

This method accepts one or two arguments:

```
FileSystem.open( filename, mode )
```

filename

The full path to the file that you want to open or create. To read from a file, you should make sure that it exists before calling *open()*.

mode

Can be either *FILE_READ* or *FILE_WRITE*. If *mode* is not specified then *open()* opens the file for reading.

The *open()* method returns an instance of the *File* class. If the Arduino cannot find, open, or create the file, this instance evaluates to *false* in an *if* statement. To check only whether a file exists, use the method *FileSystem.exists()*, which returns *true* if the file is there or *false* if the file cannot be found.

```
void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();
    FileSystem.begin();

    Serial.println("Checking for /etc/passwd file…");
    if (FileSystem.exists("/etc/passwd")) {
        File pwd = FileSystem.open("/etc/passwd");
        pwd.close();
    } else {
        Serial.println("NOT FOUND!");
    }
}
```

You should close files as soon as you are finished with them. Closing a file ensures that any changes that you have made are saved, and allows other programs to open the file. To close a file, call the *close()* method of the *File* object that you receive from *FileSystem.open()*.

If you try to open a file with mode set to *FILE_WRITE* and the file does not exist, the *open()* method creates it. If the file does exist, *open()* opens the file so that the next piece of information that you write is added to the end of the file.

### Reading from a File

Once you have opened a file with *FileSystem.open()*, there are two methods of the *File* class that you can use to read bytes from the file: *read()* and *peek()*.

If you do not pass any arguments, a call to *read()* returns the next byte from the file. The library keeps track of your position in the file, so that the next call to *read()* does not return the same value. The method *available()* returns the number of bytes left in the file that you have not yet read, and you can use this to detect the end of the file. When your position is at the end of the file, there are no bytes available.

To read the entire file, you can loop until *available()* returns zero, reading and printing bytes one-by-one:

```
#include <Bridge.h>
#include <FileIO.h>

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();
    FileSystem.begin();

    Serial.println("Checking for /etc/passwd file…");
    if (FileSystem.exists("/etc/passwd")) {
        Serial.println("OK");
        Serial.println();

        File pwd = FileSystem.open("/etc/passwd");
        while (pwd.available() > 0) {
            Serial.write(pwd.read());
        }
        pwd.close();

        Serial.println();
    } else {
        Serial.println("NOT FOUND!");
    }
}

void loop() {
}
```

*peek()* can be useful occasionally, but it is not used by the examples in this book. It reads the next byte from the file in the same way as *read()*, but it does not advance your position in the file.

An alternate form of *read()* reads multiple bytes into an area of memory – often called a buffer – including the memory occupied by an array or a struct, or dynamically-allocated with *malloc()*. When used in this way, *read()* accepts two arguments and returns an integer value indicating how many bytes were read from the file:

```
int read( void *buf, uint16_t nbyte );
```

*buf* is a pointer to an area of memory. The name of an array is also a pointer to an area of memory and can be used as this argument.

*nbyte* specifies the number of bytes that should be read from the file.

When working with arrays, keep the size of the data types in mind. An array of integer types defined as *int buf[100]* allocates memory that is 200 bytes long, because integer types on the Arduino are 16-bit values. You can calculate the actual size in bytes of any type (including arrays and structs) with the *sizeof()* operator.

### Writing to a File

When a file is opened with *FILE_WRITE* and it already exists, it opens at the end so that any data that you write is added after the existing content. If you want to overwrite a file then the easiest way is usually to delete the existing file before the call to *FileSystem.open()*.

You use the instance of the *File* class that is returned by a successful call to *FileSystem.open()* to write to the file, calling the method *write()*. Like *read()*, *write()* also has two forms – the first accepts a single byte and writes it to the file. The second form accepts a pointer to the area of memory that contains the data to be written to the file, and an integer number specifying how many bytes to write. The name of an array is actually a pointer and so this can be used when calling *write()*.

Tip: There is no guarantee that the data will be written to the file immediately – it may only be saved when the file is closed. To ensure that the data is written, you can call the method *flush()*.

The following code sample creates a new file on the SD card, and then writes the number 65 to it. When the file is opened with a text editor, such as nano, this number appears as ‘A’.

The code then writes an array of numbers, which appears in a text editor as “BCDEF”. Finally, this sample demonstrates how you can use calls to *write()* to store entire structures with one command.

To run this sketch, upload it to your Arduino and then open the Serial Monitor.

```
#include <Bridge.h>
#include <FileIO.h>

struct TS {
    byte G;
    byte H;
    byte I;
};

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();
    FileSystem.begin();

    if (FileSystem.exists("/mnt/sda1/test.txt")) {
        FileSystem.remove("/mnt/sda1/test.txt");
    }

    Serial.println("Opening file for writing... ");
    File test = FileSystem.open("/mnt/sda1/test.txt");
    if (!test) {
        Serial.println("FAILED!");
        return;
    }
    Serial.println("OK!");

    //Write a byte
    test.write(65);

    //Declare an array and then write it to the file
    byte buf[] = {66, 67, 68, 69, 70};
    test.write(buf, 5);

    //Create a struct and then write it to the file
    TS mytest = {71, 72, 73};
    test.write((uint8_t*)&mytest, sizeof(TS));

    //Close the file
    test.close();

    Serial.println("Finished!");
}

void loop() {
}
```

To open the text file and look at the data that this sketch writes:

1.  Login to the OpenWrt-Yun command line.
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/test.txt
    ```

3.  Press **Ctrl + X**.
4.  To delete the file, type the following command and then press **Enter**:

    ```
    rm /mnt/sda1/test.txt
    ```

### Opening Directories

You can use the methods in the *FileSystem* class to create and remove directories. To open a directory, use the *FileSystem.open()* method in the same way as you open a file for reading.

When you open a directory, the File object for it has three useful methods for working with the contents of the directory.

| Method | Description |
| --- | --- |
| isDirectory() | Returns true if the current File object points to a directory, or false if it does not. |
| openNextFile() | Opens the first (or next) file or directory inside the current directory, without specifying a file name. It then returns a new File object. The library remembers the last item that you open, and so the next call to openNextFile() opens the next file in the directory. |
| rewindDirectory() | Resets the current directory so that openNextFile() opens the first file in a directory. |

For an example of opening directories and listing their contents, see the functions *countMP3s()* and *getMP3Filename()*in [Project 3 – Making an MP3 Jukebox](#part0009_split_000.html_tp3).

* * *

## Making a Console Connection

If you upload sketches from the Arduino IDE to the Yún over Wi-Fi or Ethernet, you cannot use the *Serial* class to send messages to the Serial Monitor. For debugging purposes, you can use the *Console* class in the Bridge library instead.

The Console is also one of the simpler ways of giving the Linux side of the Yún control over the Arduino side. And you can still use the Console even if you connect your Yún to your PC using the USB cable.

Using the *Console* class is similar to working with the Arduino’s serial port or connecting to the Yún over SSH. However, there are two important notes:

*   As when receiving data that you send from the Serial Monitor, you need to create an Arduino sketch that listens and responds to messages. There is no built-in functionality;
*   The connection is made from software running on the AR9331, not from another computer.

### Enabling the Console from an Arduino Sketch

To use the *Console* class in your sketch, add the following include statement to the top of your sketch:

```
#include <Console.h>
```

And then call the Console’s *begin()* method from your sketch’s *setup()* function:

```
Console.begin();
```

It can take a few moments to make the connection. So it is usually a good idea to wait until the connection is setup before continuing. To do this, add the following code underneath the call to *Console.begin()*:

```
while (!Console);
```

This creates an empty loop that runs until the Console is ready.

To send information from an Arduino sketch to the Console, you can use the methods *print()*, *println()*, and *write()*. These work the same as the versions in the *Serial* class.

*print()* sends information to the Console as ASCII text. It accepts numbers, characters, and strings. If you pass a number (for example, an integer, byte, or float) then the method converts the number to a series of ASCII characters that show the value in a human-readable form.

For example:

```
Console.print(65);
```

This call to *print()* converts the number 65 into two ASCII characters – ‘6’ and ‘5’.

You can use an optional second parameter, *format*, to convert the number in different ways. The second parameter can be:

| Format | Description |
| --- | --- |
| BIN | Converts the number to a string that shows its binary representation. |
| DEC | Converts the number to a decimal (base 10) form. This is the default if you do not specify the format. |
| HEX | Converts the number to a string that shows its hexadecimal representation. |
| OCT | Converts the number to an octal (base 8) form. |

With numbers of the *float* type – those that include decimal points – you can specify a number as the second parameter. This number tells the method how many decimal places you want to show.

The *println()* method acts the same as *print()* and accepts the same inputs. However, it also adds a line break to the end of the string.Because these two methods translate numbers into human-readable text strings, if you send messages to other programs in this way then they have to convert the string back into a number. For precise control of how you send data through the *Console* class, you can use the method *write()*. *write()* does not translate numbers into human-readable text. For example:

```
Console.write(65);
```

This call does not send the characters ‘6’, and ‘5’. Instead, it sends the number as a single byte – which appears in text editors and the Linux console as the character ‘A’ because 65 is the ASCII code for the character ‘A’.

*write()* also accepts strings, and arrays of bytes or characters. When using arrays, you have to specify a second parameter that states how many bytes you want to send. For example:

```
byte buf[] = {66, 67, 68, 69, 70};
Console.write(buf, 5);
```

### Using the Console as a Replacement for the Serial Class

When debugging or testing code, it is a common practice to send messages to the Arduino IDE’s Serial Monitor using the *Serial* class. If you upload sketches to your Yún over a network connection then you cannot use the *Serial* class to do this. Instead, you can use the *Console* class to send messages to the Linux command shell.

In Running Commands and Scripts on page 113, you can see how to start the *ls* command from an Arduino sketch and send the results to the Serial Monitor. The code for this is below.

```
#include <Bridge.h>

void setup() {
    Serial.begin(9600);
    while (!Serial);
    Bridge.begin();

    Process p;
    p.begin("ls");
    p.addParameter("-l");
    p.addParameter("/");
    p.run();

    if (p.available()) {
        while (p.available()) 
            Serial.write(p.read());
        }
        Serial.println();
    }
}

void loop() {
}
```

To rewrite this sketch so that it sends the result of the *ls* command to the Console, you need to remove the references to the *Serial* class and replace them with calls to the *Console* class.

```
#include <Bridge.h>
#include <Console.h>

void setup() {
    Bridge.begin();
    Console.begin();
    while (!Console);

    Process p;
    p.begin("ls");
    p.addParameter("-l");
    p.addParameter("/");
    p.run();

    if (p.available()) {
        while (p.available()) 
            Console.write(p.read());
        }
        Console.println();
    }
}

void loop() {
}
```

Upload this sketch to your Arduino, and then to test it:

1.  Login to the OpenWrt-Yun command line. For more information, see [Connecting to the Arduino Yún](#part0005_split_000.html_tc2s1).
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    telnet localhost 6571
    ```

To test this sketch, you can use the Linux command *telnet*. The two arguments that you pass into telnet tell the program which machine on the network to connect to, and which port to use. In this example, you tell the Arduino to connect to itself on port 6571\. This port is for use with the *Console* class.

To disconnect from the Console, and return to the Linux command prompt:

1.  Press **Ctrl + C**.
2.  Press **E**.

To restart the ATmega32u4 and rerun the sketch, press the 32u4 RST button twice.

The *Console* class only accepts connections from the Linux side of the Yún. You cannot make a telnet connection directly to it from another PC, you must use SSH.

### Writing a Sketch to Control Pins from Linux

To receive commands or data from a Console connection, you need to write an Arduino sketch that: listens for messages; interprets them; performs the relevant actions; and then sends back a response (if needed).

The *Console* class has seven methods that you can use, and it also inherits the *print()* and *println()* methods from the *Stream* class.

| Method | Description |
| --- | --- |
| end() | Closes the current connection. |
| connected() | Returns true if the connection is currently open and working, or false if it is not.[1](#part0007_split_008.html_fn1) |
| available() | Returns an integer that specifies how many bytes the AR9331 has sent, but that the Arduino sketch has not yet read. |
| peek() | Reads the next byte from the connection, but does not increment your position in the buffer. The next call to *peek()* or *read()* fetches the same byte. |
| read() | Read a byte or multiple bytes from the Console connection. |
| write() | Write a byte or multiple bytes to the Console connection. |
| flush() | Ensures that any bytes that you have written with calls to *write()*, *print()*, or *println()* are sent to the AR9331 immediately. |
| print() | Prints data to the Console connection as human-readable text. Works the same way as *Serial.print()*. |
| println() | Prints data to the Console connection as human-readable text and adds on a line break character. Works the same way as *Serial.println()*. |
| readBytes() | Reads from the Console connection until the connection ends or the method receives no data. Then the method returns all of the data as an array of bytes. |
| readBytesUntil() | Reads from the Console connection until the method receives the specified character, the connection ends, or the method receives no data. Then the method returns all of the data as an array of bytes. |
| readString() | Reads from the Console connection until the connection ends or the method receives no data. Then the method returns all of the data as a string. |
| readStringUntil() | Reads from the Console connection until the method receives the specified character, the connection ends, or the method receives no data. Then the method returns all of the data as a string. |

The following example code is an Arduino sketch that gives control of the Arduino’s digital pins to Linux. It opens the Console connection and waits for information from the Linux side of the Yún.

When the sketch receives data, it looks for a three-character message. The first character is either *H*, *L*, *O*, or *I*. A two digit number follows and this specifies the number of a digital pin on the Arduino.

| Character | Description |
| --- | --- |
| H | Writes a *HIGH* to the specified digital pin. |
| L | Writes a *LOW* to the specified digital pin. |
| O | Sets the specified pin as an output. |
| I | Sets the specified pin as an input. |

Start a new Arduino sketch and type in the following code:

```
#include <Bridge.h>
#include <Console.h>

char buf[3];
int pin;

void setup() {
    Bridge.begin();
    Console.begin();
    while (!Console);
}

void loop() {
    int count = 0;
    while (count <= 3) {
        if (Console.available() > 0) {
           if ((Console.peek() != '\n') && (count == 3)) {
               Console.read();
           }
           else {
               buf[count++] = Console.read();
           }
        }
    }

    buf[3] = 0;
    pin = atoi((char *)&buf[1]);
    switch (buf[0]) {
        case 'H':
            digitalWrite(pin, HIGH);
            break;
        case 'L':
            digitalWrite(pin, LOW);
            break;
        case 'O':
            pinMode(pin, OUTPUT);
            break;
        case 'I':
            pinMode(pin, INPUT);
            break;
    }
}
```

In many cases, you can simply read until you have the number of characters that you need. However, because of the way you are going to test this sketch, the code has to wait until it receives a line break.

The *while* loop in the sketch’s *loop()* function ensures that the sketch waits until it has the three bytes for the command. At that point, the loop ignores any other characters until it reads a line break.

Tip: If the AR9331 drops the connection, this code loops because there is no data available. When the AR9331 reestablishes the connection, the *Console* class automatically handles this and *Console.available()* is again able to detect data.

This code uses a small array, *buf*, to hold the characters that it reads from the Console connection. The sketch reads bytes in groups of three (since all commands are expected to be three characters long) but *buf* contains space for four bytes. It sets the final byte to zero.

The sketch does this so that it can convert the two ASCII characters that represent the pin number to an actual integer. To do this, it uses the function *atoi()* which accepts a null-terminated string. However, the data read from the Console connection starts with *H*, *L*, *O*, or *I*. To exclude this character from the conversion, the sketch passes in the memory address of the second character in the buffer as the start of the string.

Telnet is not a raw connection and it only sends information when you press the Enter key. This is why the example in this section must wait for the line break character.

To test the sketch and control the L13 LED on the Yún:

1.  Login to the OpenWrt-Yun command line.
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    telnet localhost 6571
    ```

3.  Type the following text and then press **Enter**:

    ```
    O13
    ```

4.  To light the LED, type the following text and then press **Enter**:

    ```
    H13
    ```

5.  To turn off the LED, type the following text and then press **Enter**:

    ```
    L13
    ```

6.  Press **Ctrl + C**.
7.  Press **E**.

### Communicating through the Console from a Shell Script

The telnet command has a lot of features and options. But it is a little more limited on OpenWrt-Yun than on other Linux distributions because a few of the tools that you can use with it are not available.

If you want to write a shell script to programmatically send and receive data to the Arduino sketch, you can use *Netcat*. Netcat is a very similar program to telnet, but it is easier to use from scripts. It creates a connection to an IP address and port, and then allows other commands to redirect their input and output to this connection.

For example, to send the data “H13” to the Arduino, you can use the command:

```
echo "H13" | nc 127.0.0.1 6571
```

Netcat only accepts IP addresses. In the example above, *127.0.0.1* is the IP address for the host name “localhost”, which always points to the same machine that opens the connection. After the *echo* command is done, netcat closes the connection to the Console.

You can run multiple commands, one after the other, by placing them in parenthesis and separating each with a semi-colon:

```
(echo "H13"; sleep 2; echo "L13") | nc 127.0.0.1 6571
```

To write a shell script, you can redirect the input and output of every command in the script by executing the entire script with one call to netcat.

For example, to write a shell script on the microSD card that works with the Arduino sketch in the previous example and blinks the L13 LED:

1.  At the Linux command prompt, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/blink.sh
    ```

2.  Type the following code into the file:

    ```
    #!/bin/sh
    echo "O13"
    while true; do
        echo "H13"
        sleep 2
        echo "L13"
        sleep 2
    done
    ```

3.  Press **Ctrl + X**.
4.  Press **Y**.

To run this script from the command prompt and direct its output to the ATmega32u4, type the following command and then press the Enter key:

```
/mnt/sda1/blink.sh | nc 127.0.0.1 6571
```

### Communicating through the Console from Python

In the previous section, you can see how to use the Arduino sketch to give control over the Arduino’s digital pins to a shell script running on the AR9331\. In this section, you can see how to do the same thing from a Python script.

One of the ways to do this is to open a raw socket to the *localhost* on port 6571\. A socket is a type of connection to another machine on your network or the Internet, and a raw socket specifies that you are not using any predefined protocols (such as FTP or HTTP). Instead, you send and receive characters through a socket in a similar way to how you work with a serial port.

To use raw sockets in a Python script, you must include the *socket* module in your script.

Start a new Python script file and save it to the microSD card of your Arduino Yún.

At the top of the file, add

```
import socket, time
```

This imports the *socket* module and the *time* module. This example script uses the *sleep()* function in the *time* module to wait for a few seconds before changing the state of the Arduino’s LED.

Next, create an instance of a socket using the code:

```
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```

And specify a time-out value in seconds. The ATmega32u4 needs sufficient time to acknowledge the connection, so a good value for this is 5.

```
s.settimeout(5)
```

To open the socket, add the following code to the script:

```
try:
    s.connect(("localhost", 6571))
except:
    print "Unable to connect to the Arduino Console."
    exit()
print "Connected."
```

The *connect()* method accepts a tuple that specifies the host name or IP address of a computer to connect to, and the port number. If the script cannot connect to the Arduino, the *try* and *except* statements catch the error and the script displays a message. If the script successfully makes the connection, it displays the message “Connected.”

Make sure that digital pin 13 is set to an output by sending the command “O13”:

```
s.send("O13\n")
```

The *send()* method writes values to the socket. Because the Arduino sketch requires that commands end with a line break, the string you pass into the method also includes *\n*, which the Python interpreter replaces with a new line character. This marks the end of the command in the same way as pressing the Enter key when you test the Arduino sketch from the Linux command prompt.

To create the infinite loop that blinks the LED, add the following code to the file:

```
while 1:
    s.send("H13\n")
    time.sleep(2)
    s.send("L13\n")
    time.sleep(2)
```

Because this loop is infinite, the Python interpreter does not run any statements that are not inside the loop. Even so, the full example script includes a line at the end to demonstrate how to call the *close()* method.

```
s.close()
```

The *close()* method ends the current connection. You should close sockets when you do not need them anymore. However, if you forget, Python will usually close the connection for you when the script ends or when it decides that the object *s* is not needed.

The full Python script should look like this:

```
import socket, time

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.settimeout(5)

try:
    s.connect(("localhost", 6571))
except:
    print "Unable to connect to the Arduino Console."
    exit()
print "Connected."

s.send("O13\n")
while 1:
    s.send("H13\n")
    time.sleep(2)
    s.send("L13\n")
    time.sleep(2)
s.close()
```

* * *

## Using Mailbox and Sending Messages

The *Mailbox* class is another way of sending information from the AR9331 to the ATmega32u4\. You can also use it to send information from other machines on your network, and have the AR9331 receive and store them until the Arduino sketch reads them.

At the time of writing, sending messages from the ATmega32u4 to the AR9331 is not fully supported by the Mailbox.

Mailbox uses short text strings as messages. You can send these to the Arduino using a universal resource locator (URL) and the hypertext transfer protocol (HTTP). The built-in web server in OpenWrt-Yun Linux does the work of processing the HTTP request for you.

In the Arduino IDE, the example sketch *MailboxReadMessage* demonstrates how to read messages from an Arduino sketch. To upload this example to your Arduino from the Arduino IDE:

1.  On the **File** menu, point to **Examples**, then point to **Bridge**, and then click **MailboxReadMessage**.
2.  On the toolbar, click **Upload**.
3.  On the **Tools** menu, click **Serial Monitor**.

To send a message from another machine on your network to the Arduino,

1.  Open a web browser and type the following URL into the address bar: *http://arduino.local/mailbox/Test*
2.  Press **Enter**:
3.  In the username box, type *root*.
4.  In the password box, type *arduino*.[2](#part0007_split_008.html_fn2)
5.  Click **OK**.

Everything that you type after *http://arduino.local/mailbox/* is a message. When you send a message from the web browser, the response that you receive is a blank page.

If you want to disable the password protection and allow any machines on your network to send messages to the Arduino without specifying the username and password:

1.  On a machine that connects to the same network as the Arduino, open a web browser.
2.  In the address bar, type *http://arduino.local*
3.  Press **Enter**.
4.  In the username box, type *root*.
5.  In the password box, type *arduino*.[3](#part0007_split_008.html_fn3)
6.  Click **LOG IN**.
7.  Click **CONFIGURE**.
8.  Scroll to the bottom of the page and, under **REST API ACCESS**, click the **Open** box.

You do not need to restart the Yún to protect or unprotect the Mailbox interface.

### Receiving Messages in an Arduino Sketch

The example sketch from the IDE is shown below:

```
#include <Mailbox.h>

void setup() {
   pinMode(13, OUTPUT);
   digitalWrite(13, LOW);
   // Initialize Bridge and Mailbox
   Bridge.begin();
   Mailbox.begin();
   digitalWrite(13, HIGH);

   // Initialize Serial
   Serial.begin(9600);

   // Wait until a Serial Monitor is connected.
   while (!Serial);

   Serial.println("Mailbox Read Message\n");
   Serial.println("The Mailbox is checked every 10 seconds\n");
}

void loop() {
   String message;
   // if there is a message in the Mailbox
   if (Mailbox.messageAvailable()) {
     // read all the messages present in the queue
     while (Mailbox.messageAvailable()) {
       Mailbox.readMessage(message);
       Serial.println(message);
     }
     Serial.println("Waiting 10 seconds before checking the Mailbox again");
   }
   // wait 10 seconds
   delay(10000);
}
```

In the sketch’s *loop()* function, you call the *begin()* method of the *Mailbox* class to initialize the connection to the Mailbox on the Atheros AR9331.

The method *messageAvailable()* returns true if there are any messages stored on the AR9331 that you have not yet read.

To read a message, you use the method *readMessage()*. readMessage() accepts two arguments:

| Argument | Description |
| --- | --- |
| buffer | A *String* object in which to store the message. |
| size | An optional number of bytes. If included, *readMessage()* only reads the specified number of bytes from the message. |

### Sending Messages from the Linux Shell

To send a message from the Linux shell to an Arduino sketch, you can use the same process of making a web request to a URL with the message on the end.

The Linux command *curl* makes an HTTP request to a specified URL. So to send a simple message to the *MailboxReadMessage* example sketch:

1.  Login to the OpenWrt-Yun command line.
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    curl http://127.0.0.1/mailbox/Hello
    ```

The IP address 127.0.0.1 is a special address that always points to the same machine that the request is made from.

You can use curl in a shell script in exactly the same way. Remember, even if you use a variable to store the message, you need to URL encode special characters (such as spaces) so that curl sends them to the Mailbox.

For example:

```
#!/bin/sh
MSG="This%20is%20a%20test!"
curl -u root:arduino http://127.0.0.1/mailbox/$MSG
```

Or if you turn off the password protection for the REST API in the Arduino web panel:

```
#!/bin/sh
MSG="This%20is%20a%20test!"
curl http://127.0.0.1/mailbox/$MSG
```

### Sending Messages from a Python Script

There are two ways that you can send a message to the ATmega32u4 from a Python script running on the Atheros AR9331\. You can use the same method of calling a URL as the previous examples, or you can use the Python *BridgeClient* class.

To make a URL request from a Python script, you can use the *urllib* module. To do this, first import the module at the top of your script and then open the URL using the function *urllib.urlopen()*. For example:

```
import urllib
urllib.urlopen("http://root:arduino@127.0.0.1/mailbox/Hello from Python!")
```

You can automatically send the username and password to access the REST API by including those pieces of information before an @ symbol. If you turn off password protection for the REST API in the Arduino web panel, you can simply call:

```
urllib.urlopen("http://127.0.0.1/mailbox/Hello from Python!")
```

Unlike curl, *urlopen()* automatically URL encodes special characters (such as spaces and punctuation marks) so that the Mailbox can receive them.

There is also a special Python module, *BridgeClient*, which you can use to work with the Mailbox from scripts on the AR9331\. This avoids passing the information in a URL. To use this module, you need to add it to Python’s path so that you can import it:

```
import sys
sys.path.insert(0, "/usr/lib/python2.7/bridge/")
from bridgeclient import BridgeClient
```

Then you can create an instance of *BridgeClient* and use the method *mailbox()* to send a string to the Mailbox for the Arduino sketch to pick up.

```
client = BridgeClient()
client.mailbox("Hello from Python!")
```

* * *

## Communicating over Local Networks and the Internet

On the Yún, the Atheros AR9331 provides network connectivity to the ATmega32u4 in a similar way to how an Ethernet Shield or Wi-Fi Shield provides network connectivity to other Arduinos.

There are three classes in the Bridge library for working with network and Internet connections.

| Class | Description |
| --- | --- |
| HttpClient | Makes a connection to a web server over hypertext transfer protocol (HTTP) on transmission control protocol (TCP) ports. This class uses the Linux command *curl* to fetch information from web servers. |
| YunClient | Makes a connection to a server and provides methods for sending and receiving data. This class is not specific to any particular protocol. |
| YunServer | Allows other machines to make a connection over Internet protocols. This class is not specific to any particular protocol. |

You can use the two client classes (*HttpClient* and *YunClient*) to make connections with servers on your local network, the Internet, and the AR9331\. And you can use the *YunServer* class to receive connections from external machines, and from the Linux side of the Yún.

In , you can see how these classes work and how to use them to create devices that communicate over Internet protocols.

* * *

## Choosing a Connection Method

In this chapter, you can see six ways of exchanging information between the ATmega32u4 on the Arduino side of the Yún and the Atheros AR9331 on the Linux side:

*   Passing data through the shared-memory area;
*   Starting Linux commands and scripts, and passing information into them from the command line or by writing to the running process;
*   Reading and writing to files on the Linux file system;
*   Using the Console;
*   Using the Mailbox;
*   Communicating over Internet protocols.

There are no fixed rules as to when you should use each. However, the summary notes below may help you.

*   Using the shared-memory area works when passing values between an Arduino sketch and a Python script. It relies on both the sketch and the Python program knowing the key names of each item of data, and understanding who can change this information and when. It is most useful when you have a long-running program on one processor that needs up to date information from the other (for example, a temperature reading), but that itself never needs to change the information. The shared-memory area works best with simple numbers and strings. For other types, you may find it more useful to work with files, the *Console* class, or network connections.
*   Running Linux commands is helpful when the Arduino needs to modify the Linux system, run programs that do not take long to complete, or start long-running programs that communicate with the ATmega32u4 through a different method. You can easily pass information into the program at the start, but it is more difficult to pass information to programs that are already running.
*   You can use the file system to exchange very large pieces information between the two processors. However, you first need to work out how each processor knows that data is ready, how it knows when all of the relevant data has been transferred, and how it knows that it is safe to open that information without blocking the other processor. This works best in combination with another method – for example, sending a Mailbox message to the ATmega32u4 with a file name to tell the Arduino sketch that it can open the file.
*   The Mailbox is a simple and convenient way of sending short strings from the Linux side of the Yún to the Arduino side. However, it does not work well when trying to send messages in the other direction, or when trying to exchange non-text-based information.
*   You can use the *Console* class when you want to make a continuous connection between the ATmega32u4 and the AR9331\. Once the connection is made, either side of the Yún can send and receive data when it wants.
*   The three networking classes of the Bridge library (*HttpClient*, *YunClient*, and *YunServer*) are a good choice when: you are already using network protocols for some other aspect of your project; when you want to accept or make connections to and from other devices; and when you want to pass information to Linux programs that normally communicate with web-based systems.

* * *

[1](#part0007_split_005.html_nf1)It is possible for a connection to be closed after data is sent, but before you read it from the buffer.[2](#part0007_split_006.html_nf2)If you change the password on your Yún, type the new password here.[3](#part0007_split_006.html_nf3)If you have not changed it, the password is arduino.

# Hosting Websites and Services

Web servers wait for incoming connections from clients, usually web browsers. They process requests for information, and then send the information or an error message indicating why the server could not complete the request. When hosting websites, the information that a web browser requests is usually a page. After examining the page, the browser then makes requests for all the images, JavaScript files, stylesheets, and other files that the page needs.

A web service – often called an application programming interface (API) – is a special type of website. Rather than sending back pages and images, the server processes requests and usually performs some kind of action (for example, lighting an LED) and sends back information in a format that is intended for other computer programs to interpret.

If you work with shields, such as the Arduino Ethernet or Wi-Fi shields, then you may be familiar with how to accept an incoming connection in an Arduino sketch, and how to send back pages and information to web browsers. On the Arduino Yún, you can use the same techniques that you use with those shields. In [Project 2 – Controlling an LED Matrix through a Web API](#part0008_split_004.html_tc5s5) you can see how to accept connections using the *YunServer* and *YunClient* classes in the Bridge library.

However, the Atheros AR9331 is much faster and has more memory than the ATmega32u4\. And so the Linux side of the Yún is a much more capable web server than the Arduino side. OpenWrt-Yun has a built-in software package called “uHTTPd”. This is the software that runs the Yún’s two web-based administration panels, and you can use it to host your own websites and web services.

In This Chapter

[Setting Up a Website on the Arduino Yún](#part0008_split_000.html_tc5s1)

[Server-Side Scripting with CGI and Python](#part0008_split_001.html_tc5s2)

[Project 1 – Building a Web-Based Temperature Monitor](#part0008_split_002.html_tc5s3)

[Making Web Services and APIs](#part0008_split_003.html_tc5s4)

[Project 2 – Controlling an LED Matrix through a Web API](#part0008_split_004.html_tc5s5)

[Installing and Using PHP](#part0008_split_005.html_tc5s6)

* * *

## Setting Up a Website on the Arduino Yún

In OpenWrt-Yun, the top-level directory */www* contains all of the files that uHTTPd uses to make the Yún’s web-based administration panels accessible to web browsers.

When a web browser requests a file from the Arduino Yún, uHTTPd looks in this directory for it. If the browser specifies a sub-directory as part of the web address then uHTTPd looks for the directory inside */www*. If the browser does not specify which page it is looking for, uHTTPd sends back the default webpage. This default is usually one of the following file names: *index.html*, *index.htm*, *default.html*, or *default.htm*.

OpenWrt-Yun takes up most of the available space on the Atheros AR9331\. To host your own files, you need to store them on the microSD card.

If you expand the Linux file system onto the microSD card then inside */www* there is a symbolic link, */www/sd*. This links to the */mnt/sda1/arduino/www* directory on the microSD card. For example, if you place a hypertext markup language (HTML) file called “index.html” inside the */mnt/sda1/arduino/www* directory then you can access this file using the universal resource locators (URLs):

*   *http://arduino.local/sd*; or
*   *http://arduino.local/sd/index.html*

If you do not expand the Linux file system onto the microSD card, but want to add files to the Yún’s default website in the way described, you have to create this link yourself. For example, to link */www/sd* to a directory called “www” in the top-level of the microSD card, type the following command at the OpenWrt-Yun command prompt and then press the Enter key:

```
ln -s /mnt/sda/www /www/sd
```

Placing your files in the Yún’s default website is often convenient. But any configuration changes that you make to this site also apply to the two administration panels.

You can run more than one website on the Yún. However, uHTTPd has a few limitations that affect how you do this. Web clients make connections to web servers over transmission control protocol (TCP), and they usually do this over port 80\. uHTTPd can only run one website for each TCP port.[1](#part0008_split_006.html_fn1)

To change how uHTTPd runs, you can make changes to the file */etc/config/uhttpd*. Open this file in nano to see how to structure information in this file:

1.  Login to the OpenWrt-Yun command line.
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/config/uhttpd
    ```

The file comprises several sections, each one starting with a *config* declaration. At the top of the file, you can see the section beginning with “config uhttpd main”. This configuration section controls the default website on the Yún – including the two administration panels. To create a new website, you need to add a new configuration section.

To create a new website, first create a directory on the microSD card to contain all of your files. For example:

1.  If you still have nano open, press **Ctrl + X**.
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    cd /mnt/sda1
    ```

3.  Type the following command and then press **Enter**:

    ```
    mkdir www2
    ```

To configure uHTTPd with a new website that runs on TCP port 81,

1.  Type the following command and then press **Enter**:

    ```
    nano /etc/config/uhttpd
    ```

2.  Press the **Down Arrow** key until you reach the lines:

    ```
    # Certificate defaults for px5g key generator
    config cert px5g
    ```

3.  Above those lines, type in the following text:

    ```
    # Configuration for the second website
    config uhttpd site2
            list listen_http          0.0.0.0:81
            option home               /mnt/sda1/www2
            option rfc1918_filter     0
            option max_requests       2
            option network_timeout    30
            option tcp_keepalive      1
    ```

4.  Press **Ctrl + X**.
5.  Press **Y** and then press **Enter**.

Use the Tab key to indent the lines. The spacing in this file is very important to uHTTPd.

Lines that begin with *#* are comments, and uHTTPd ignores these. Place as many comments in the file as you need to help you remember why you made certain settings.

*site2* is the name of the new website; you can set this to anything you want. The configuration section in this example is very minimal, and there are only two important lines to be aware of:

*   The line *list listen_http 0.0.0.0:81* tells uHTTPd to listen on TCP port 81 on all IP addresses. You can specify an IP address by replacing 0.0.0.0 with the IP address that you want uHTTPd to listen on.
*   The line *option home /mnt/sda1/www2* specifies where uHTTPd looks for the files for this website.

Before these changes take effect, you have to restart uHTTPd. To do this,

*   At the command prompt, type the following command and then press **Enter**:

    ```
    /etc/init.d/uhttpd restart
    ```

Next, place a simple *index.html* in the */mnt/sda1/www2* directory, or

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /mnt/sda1/www2/index.html
    ```

2.  Type in the following text:

    ```
    <html>
    <head><title>OK</title></head>
    <body><p>OK</p></body>
    </html>
    ```

3.  Press **Ctrl + X**.
4.  Press **Y** and then press **Enter**.

To test this website, you need to open a web browser on a machine that is on the same network as your Arduino. To specify the TCP port that the browser should use, you add a colon and then the port number to the end of the host name or domain name.

For example: *http://arduino.local:81/*

Tip: The TCP port numbers for your websites can be a number from 0 through 65535\. However, many of these ports are already in use by other programs. Numbers 80–90 are usually a safe choice.

### Setting the Default Page

If a web browser makes a request to uHTTPd but does not specify the file that it wants, uHTTPd looks in the website’s directory for any of the following files: *index.html*, *index.htm*, *default.html*, or *default.htm*.

You can change this by specifying the *index_page* option in the */etc/config/uhttpd* configuration section for your site. For example:

```
option index_page         home.html
```

### Introducing Port Forwarding and Dynamic DNS

On a network, computers make connections to other computers using IP addresses. These addresses tell one machine where it can find the other.

However, when your computers connect to the Internet through a router, your Internet service provider (ISP) assigns an additional IP address to the router. To the outside world, all devices on your local network appear to have the same IP address – the one set by the ISP. The local network addresses are not used by clients connecting through the Internet.

This creates two problems: how can your router know which machine on your network is supposed to respond to web requests, and how do clients on the Internet find your router?

Port forwarding is a configuration setting that you can use to tell your router which device on your local area network (LAN) should receive the connection from the outside world. The exact method of setting this up is different for each router.

As a general guide:

1.  Login to your router’s administration panel. For many home routers, this is done by visiting the URL http://192.168.0.1 in a web browser on your PC.
2.  Look for an option or page that allows you to control inbound connections. This may be named *Port Forwarding*, *Firewall Rules*, *Services*, or something similar.
3.  Create rules that says the HTTP service is allowed on a specific port (for example, 80 and 81), and that requests should be sent to IP address of the Arduino Yún.

Because the IP address of the Yún changes every time it connects to the router, you should connect the Yún to your network using a static IP address. For more information, see [Using a Static IP Address](#part0004_split_005.html_tc1s5s1).

When you visit a website, you use its domain name (for example, *google.com*) as part of the web address. Your web browser looks up the domain name to find the associated IP address, using the domain name system (DNS). But unless you ask them to, your ISP does not allocate a fixed (or static) IP address to your router. Instead, the IP address will change every time your router connects to the Internet. If the connection drops or the router restarts, this address changes.

Dynamic DNS (DDNS) is a method of automatically updating DNS records when the router receives a new IP address from an ISP. This means that any web clients trying to find your server using a domain name will always receive the up-to-date IP address.

Although there are many DDNS services out there, they all tend to work the same way: when your router connects to the Internet then it (or a machine on your network) contacts the DDNS servers and tells them the new IP address. You can usually choose whether to use a domain name given to you by the DDNS service, or buy your own domain name and use that.

When hosting multiple websites on the Yún, there are additional problems.Unless you use multiple IP addresses for the Yún, only one of your websites can use TCP port 80\. If the user (or a link that they click on) does not specify the port number, then the browser uses TCP port 80\. With the default configuration, this opens up the Arduino Yún’s administration panel to the world. If you allow incoming connections from across the Internet, you should change the password for your Arduino Yún.If you want to run your second website on TCP port 80, so that it is the default site, then you have to change the website configuration for the administration panels in */etc/config/uhttpd* so that they use a different port. You can then configure your router to only allow access on TCP port 80, and the administration panels become inaccessible outside of your local network.

### Changing the TCP Port Number of the Administration Panels

To change the uHTTPd configuration so that your new website is the default (on TCP port 80), and the administration panels use a different port:

1.  Login to the OpenWrt-Yun command line.
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/config/uhttpd
    ```

3.  In the configuration section labelled “main”, change the line that reads *list listen_http 0.0.0.0:80* to

    ```
    list listen_http          0.0.0.0:81
    ```

4.  In the configuration section for your new website, change the line that starts *list listen_http* to

    ```
    list listen_http          0.0.0.0:80
    ```

5.  Press **Ctrl + X**.
6.  Press **Y** and then press **Enter**.
7.  Type the following command and then press **Enter**:

    ```
    /etc/init.d/uhttpd restart
    ```

### Protecting Websites with Basic Authentication

Basic authentication is a way of protecting your website by telling visitors to enter a username and password when they try to access the site. This method of user authentication is not secure – when the user submits their details to the server, anyone listening to the request can see the password – but it can be useful as a temporary method of preventing people from accidently accessing your projects.

You need to create an *httpd.conf*configuration file for this. *httpd.conf* is a file name, but it also describes a type of file. The file names that you use for your configuration files can be different. You use this file to set additional configuration properties for the site. */etc* is a good place to keep these files. In this example, you will password-protect the website that is created in [Setting Up a Website on the Arduino Yún](#part0008_split_000.html_tc5s1). The configuration file is called */etc/site2.conf*.

1.  Login to the OpenWrt-Yun command line.
2.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/site2.conf
    ```

3.  Type the following line into the file:

    ```
    /:test:01234
    ```

4.  Press **Ctrl + X**.
5.  Press **Y** and then press **Enter**.

The line that you add to the file contains three pieces of information separated by colons: the path[2](#part0008_split_006.html_fn2); the username that visitors must use; and the password.

To add multiple users, add multiple lines of this type.To enable basic authentication on the website in uHTTPd,

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/config/uhttpd
    ```

2.  Find the configuration section for the website that you want to protect.
3.  The realm name is usually displayed to the user. It can be anything that you want (but only one word). To add a realm name to the configuration, add the line:

    ```
    option realm              Site2
    ```

4.  To specify the location of the *httpd.conf* file that you created earlier, add the line:

    ```
    option config             /etc/site2.conf
    ```

5.  Press **Ctrl + X**.
6.  Press **Y** and then press **Enter**.
7.  Type the following command and then press **Enter**:

    ```
    /etc/init.d/uhttpd restart
    ```

### Creating Virtual Files and Directories

One of the ways to link content into your website from directories outside of a website’s directory, is to create symbolic links. For more information, see .

However, because of the way that OpenWrt-Yun mounts the Linux file system, you cannot create symbolic links in the */mnt/sda1/* directory, or any of its sub-directories except for *arduino/www/*.

Using an additional website configuration file is another way that you can create links between files and directories. Unlike symbolic links, these links only work when you access the files through the web server. You need to create an *httpd.conf* configuration file for this. This file allows you set additional configuration properties for the site. */etc* is a good place to keep these files.For example, you can have all of your images stored in the directory *data/images/* and create a virtual directory that allows you to access these files from the URL *http://arduino.local/images/*.

To create this link in an *httpd.conf* file, */etc/site2.conf*,

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/site2.conf
    ```

2.  Type the following line into the file:

    ```
    A:/images:/data/images
    ```

3.  Press **Ctrl + X**.
4.  Press **Y** and then press **Enter**.

The line beginning “A:” contains three pieces of information separated by colons: a command (*A*) to tell uHTTPd to create an alias; the name of the virtual directory that website visitors can use; and the actual directory in the file system. In an *httpd.conf* file, file and directory paths beginning with */* do not start from the top-level directory in the Linux system, they start from the top-level directory of the website.

You can also create virtual files, using an entry like:

```
A:/favicon.ico:/data/images/myicon.ico
```

To enable these extra configuration options, you need to change uHTTPd’s configuration for the website so that it uses the *.conf*file.[3](#part0008_split_006.html_fn3)

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/config/uhttpd
    ```

2.  Find the configuration section for the website that you want to apply these extra options to.
3.  To specify the location of the *httpd.conf* file that you created earlier, add the line:

    ```
    option config             /etc/site2.conf
    ```

4.  Press **Ctrl + X**.
5.  Press **Y** and then press **Enter**.
6.  Type the following command and then press **Enter**:

    ```
    /etc/init.d/uhttpd restart
    ```

In the next section of this chapter, you can see how to write programs that dynamically create content for your website. You may choose to put these programs in a special folder named “cgi-bin”. However, by using virtual files and directories, you can make these programs appear anywhere in your website.

* * *

## Server-Side Scripting with CGI and Python

When you host HTML pages and files on the Arduino and send them to web browsers, this is called “static content”. The files that uHTTPd sends to the clients, and what the web browsers display, only change when you update the files on the Yún.

Dynamic content is different. Dynamic content means using a programming or scripting language to change the information that is displayed in the web browser. Fetching content from a database and then including it on a web page is an example of dynamic content.

This can be done with client-side scripting, or server-side scripting. Client-side scripting uses languages, such as JavaScript, that run in the web browser. The server sends the same information every time, but the browser runs a script to change how it uses that information.

With server-side scripting, a program changes the information *before* the web server sends it to the web browser.

On web servers, you can use languages such as active server pages (ASP), java server pages (JSP), and PHP: hypertext processor (PHP) for server-side scripting. OpenWrt-Yun does not have built-in support for these languages, but it is sometimes possible to install them.

On the Yún, you can use the common gateway interface (CGI) to write dynamic content. CGI programs and scripts send their output to the standard output device – this is the command-line shell when you run a program from the command prompt, but when you run the same program from uHTTPd then it sends the output to the web browser.

Because the Arduino Yún has built-in support for the Python language, this chapter focusses on writing Python scripts for server-side scripting. In [Programming in Python](#part0006_split_000.html_tc3), you can learn more about writing Python scripts.Before you can run Python scripts that send information to web browsers, you need to change the configuration of uHTTPd to allow this. If you do not already have an additional web site on your Yún, follow the instructions in [Setting Up a Website on the Arduino Yún](#part0008_split_000.html_tc5s1) to create one.There are two ways of running Python scripts from a website: using a cgi-bin directory; and using a script interpreter.

### Using Python Scripts in cgi-bin

If you use a cgi-bin directory then uHTTPd only runs files that are in that directory. If the web browser requests a Python file outside of the cgi-bin directory then the web server sends the script as a text file.

To add a cgi-bin to a website,

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/config/uhttpd
    ```

2.  Find the configuration section for the website that you want to apply these extra options to.
3.  Add the following lines to the site’s configuration:

    ```
    option cgi_prefix         /cgi-bin
    option script_timeout     60
    ```

4.  Press **Ctrl + X**.
5.  Press **Y** and then press **Enter**.
6.  Create a directory inside the website’s home directory, and call it *cgi-bin*.
7.  Type the following command and then press **Enter**:

    ```
    /etc/init.d/uhttpd restart
    ```

To create a test script and run it:

1.  Create a file, for example *test.py*, inside the cgi-bin directory.
2.  Add the following text to the file:

    ```
    #!/usr/bin/python
    print "Content-type: text/plain"
    print
    print "Hello from Python"
    ```

3.  Open a web browser on a machine that is connected to the same network as your Arduino.
4.  In the address bar, type the URL of the website followed by */cgi-bin/test.py* and then press **Enter**.

### Adding a Script Interpreter to a Website

By adding a script interpreter to the website’s configuration in */etc/config/uhttpd*, you can run Python scripts outside of a cgi-bin directory.

To set this up,

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    nano /etc/config/uhttpd
    ```

2.  Find the configuration section for the website that you want to apply these extra options to.
3.  Add the following lines to the site’s configuration:

    ```
    list interpreter          ".py=/usr/bin/python"
    option script_timeout     60
    ```

4.  Press **Ctrl + X**.
5.  Press **Y** and then press **Enter**.
6.  Type the following command and then press **Enter**:

    ```
    /etc/init.d/uhttpd restart
    ```

To create a test script and run it:

1.  Create a file, for example *test.py*, inside the website’s home directory.
2.  Add the following text to the file:

    ```
    #!/usr/bin/python
    print "Content-type: text/plain"
    print
    print "Hello from Python"
    ```

3.  Open a web browser on a machine that is connected to the same network as your Arduino.
4.  In the address bar, type the URL of the website followed by */test.py*, and then press **Enter**.

If you are working on a project that allows users to upload files then you should be careful using an interpreter declaration. If you allow Python scripts to run anywhere on the site, not just in a cgi-bin, you need to ensure that users cannot upload their own script and then run it.

### Sending HTTP Responses from Python Scripts

In the test script in the previous section, you can see how a Python script sends information to the web browser: uHTTPd redirects the program’s standard output to the web browser, and so the script can use the *print()* function to send content.

The first line of the test script tells the web server which command to use to run the script.

When a server sends a file to a web browser, it also sends additional information that describes the file and the server from which it came. These pieces of information are HTTP response headers. On the Yún, uHTTPd does most of the work of generating and sending the HTTP headers. The only one that you must send yourself is *Content-Type*.

Web browsers use the *Content-Type* field in an HTTP response header to decide what to do with the file – this serves the same purpose as the file extension on Microsoft Windows.

The values of the *Content-Type* field are called “MIME types” because they are derived from the multipurpose Internet mail extensions (MIME) standard, which is used to allow email messages to contain attachments and different types of text.

Some of the most common MIME types used on the web are:

| File Extension | Media Type | Description |
| --- | --- | --- |
| .HTM | text/html | Specifies that the file is an HTML document. |
| .GIF | image/gif | Specifies that the file is an image in the graphics interchange format (GIF). |
| .PNG | image/png | Specifies that the file is an image in the portable network graphics (PNG) format. |
| .JPG | image/jpeg | Specifies that the file is an image in the format created by the Joint Photographic Experts Group. |
| .CSS | text/css | Specifies that the file is a cascading style sheet (CSS). |
| .TXT | text/plain | Specifies that the file is a plain text document. |

To send an HTTP header, you print its name followed by a semi-colon, and then a value. For example:

```
print "Content-type: text/plain"
```

If you want to send other HTTP header fields in your scripts, you can do it in exactly the same way.

After sending all of the HTTP headers, there is an empty line between them and the actual web page information.

### Accessing CGI Environment Variables

When a web browser requests a file from a web server, it sends an HTTP request message. This information contains the name of the file that the browser wants, and additional HTTP request headers that contain things like: query string parameters (values that come after a question mark in the URL); form fields; and strings that state the name of the web browser and the operating system that it runs on.

uHTTPd places this information in environment variables, and you can access it from a Python script by using the *os* module.

The example below shows how to write a server-side Python script that shows the name (and similar information) of the web browser.

```
#!/usr/bin/python
import os

print "Content-type: text/plain"
print
print os.environ["HTTP_USER_AGENT"]
```

The most-common CGI environment variables that you can access using the *os.environ* collection are:

| Variable | Description |
| --- | --- |
| CONTENT_TYPE | When the web browser performs a file upload, this field specifies the MIME type of the attached file. |
| CONTENT_LENGTH | The length (in bytes) of form-submitted data. This is only used when the browser makes a form submission using the *POST* method. |
| DOCUMENT_ROOT | The file path of the website’s top-level directory on the server. |
| HTTP_COOKIE | Contains the cookies that the web browser sends. This is a string of key-value pairs, with each pair separated by a semi-colon. |
| HTTP_REFERER | Contains the URL of a web page if the user clicked a link to access the current page. |
| HTTP_USER_AGENT | Describes the web browser and the operating system that it runs on. |
| QUERY_STRING | See below. |
| REMOTE_ADDR | The IP address of the machine that makes the HTTP request. |
| REMOTE_HOST | If it is possible to resolve the *REMOTE_ADDR* IP address into a host name, then *REMOTE_HOST* contains this information. |
| REQUEST_METHOD | Usually *GET* for standard web requests, or *POST* for form submissions. |
| REQUEST_URI | A string that contains all of the information in the web browser’s request URL, except for the protocol and domain name. |
| SCRIPT_FILENAME | The file name and full file path of the current script. |
| SERVER_NAME | The host name or IP address of the web server. |
| SERVER_PROTOCOL | The HTTP protocol used for this request. This is usually *HTTP/1.1*. |
| SERVER_SOFTWARE | The name of the web-server software. If you use uHTTPd on the Arduino Yún, this value is *uHTTPd*. |

Some of this information comes from the web browser, and some of it is extra information from uHTTPd.

### Accessing Query String and Form Data using the Python CGI Module

Web browsers can send information to the web server in several ways: through a query string; with a form submission; or in cookie variables.

The query string is a collection of key and value pairs that the browser sends as part of the request URL. Each pair comprises a key (like a variable name) and a value, and these are separated by an equals sign. Each pair is separated from the others using an ampersand. A question mark in the URL indicates the start of the query string.

For example:

```
http://arduino.local/cgi-bin/file.py?key1=value1&key2=value2&key3=value3
```

When uHTTPd receives this request, it puts everything after the question mark into the CGI environment variable *QUERY_STRING*. You can process the query string using Python’s string functions. However, there is a simpler way.

Tip: When the browser makes a form submission using the request method POST, it creates a very similar key-value string. However, it sends the string after the HTTP request header, not as part of the request URL.

The Python CGI module simplifies how you can access query string and form data. You can use it from scripts in a cgi-bin directory, or from Python scripts that run through a script interpreter.To use the module, you need to import it into your Python script. For example:

```
#!/usr/bin/python
import cgi
```

The CGI module interprets the CGI environment variables and makes it easier for you to extract the information that you want. Whether the browser passes values into a script using a query string or it sends them with a form submission, you can use the *FieldStorage* class to access the values.

To create an instance of *FieldStorage*, add the following line to your script:

```
form = cgi.FieldStorage()
```

Then you can access a query string value using the *getvalue()* method and the key name. For example, to send back the value of the query string parameter *key1*, place this script into your cgi-bin directory:

```
#!/usr/bin/python
import cgi
form = cgi.FieldStorage()

print "Content-type: text/plain"
print
print form.getvalue("key1")
```

If the web browser does not send a key-value pair with the name that you request, *getvalue()* returns an empty string.

You can also access values using the syntax:

```
form["key1"].value
```

Each entry in a form is a *FieldStorage* or *MiniFieldStorage* object, which represents a key-value pair. The *value* property returns the value from the pair. The *name* property returns the key.

Tip: If the web browser sends multiple entries with the same key (for example, multiple form fields on an HTML page with the same name) then the entries in *form* are lists of *FieldStorage* or *MiniFieldStorage* objects instead. If you need to process all of the entries, use the *getlist()* method instead of *getvalue()*.

### Handling File Uploads using the Python CGI Module

When the web browser makes a form submission, it collects the values from all of the HTML input elements in the form and then sends them in a key-value string.

However, the process is slightly different if you make an HTML form that allows the user to upload a file. The HTML code below is a short example of how to create a form that prompts the user to upload a file:

```
<html>
<head><title>Form Upload Example</title></head>
<body>
   <form enctype="multipart/form-data" action="/cgi-bin/save.py" method="post">
   <p>File: <input type="file" name="uFile" /></p>
   <p><input type="submit" value="Upload" /></p>
   </form>
</body>
</html>
```

If the CGI module receives a file then it places the file name into the *filename* property of the object that represents the form field. To retrieve the file name, you need to access the form field using the same name as it has in the HTML.

To create a Python script to display the file name of an uploaded file: create the script */cgi-bin/save.py*[4](#part0008_split_006.html_fn4) and type in the following code:

```
#!/usr/bin/python
import cgi

form = cgi.FieldStorage()
print "Content-type: text/plain"
print
try:
    print "File: " + form["uFile"].filename
except:
    print "Error."
```

If the web browser requests the */cgi-bin/save.py* script without sending the form data then the Python interpreter raises an exception. The *try* and *except* statements stop the script from ending early and not sending back a response to the web browser.

To store the uploaded file somewhere, you need to create a new file on the file system (ideally on the microSD card) and write the file information to it. The file’s raw data is accessible through the *file* property of the *form* object.

For example, change the */cgi-bin/save.py* script to the following code:

```
#!/usr/bin/python
import cgi

print "Content-type: text/plain"
print

form = cgi.FieldStorage()
try:
    fn = "/mnt/sda1/" + form["uFile"].filename
    myfile = open(fn, "wb")
    myfile.write(form["uFile"].file.read())
    myfile.close()
    print "Thank you."
except:
    print "Error writing file, or no file uploaded."
```

The *read()* method of the *file* property returns all of the information from the file that the browser uploads. By passing this into the *write()* method of the open file, you can store the entire file with one line of code.

* * *

## Project 1 – Building a Web-Based Temperature Monitor

This project uses the Arduino Yún with an Adafruit MCP9808 ([http://www.adafruit.com/product/1782](http://www.adafruit.com/product/1782)) to create a web-based temperature monitor. Anyone on your local network (or across the Internet if you allow incoming connections on your router) can open the temperature monitor website to see the current room temperature.

The built-in web server on the Linux side of the Yún accepts connections from web browsers, and sends the HTML page, cascading style sheet (CSS) file, and images to the client. An Arduino sketch on the ATmega32u4 reads from the MCP9808 sensor and stores the current temperature in the AR9331’s memory.

To complete this project, you need:

1.  An Arduino Yún, connected to your local network over Ethernet or Wi-Fi.
2.  A microSD card, formatted for use with the Yún.
3.  An Adafruit MCP9808 high-accuracy I2C temperature sensor breakout board.
4.  (Optional) If your MCP9808 does not have header pins pre-installed, you need a soldering iron and solder to connect these.

If you do not have access to an MCP9808, there are many other I2C temperature sensors that you can use for this project. If you use a different board, consult the documentation for your sensor carefully. The connection diagrams and instructions that follow may be specific to the MCP9808.

### Connecting the Adafruit MCP9808 Temperature Sensor to the Arduino

The MCP9808 runs on 2.7 V–5.5 V, and uses an extremely small amount of current (around 200 μA). To simplify the process of connecting the sensor to the Arduino, the diagrams and instructions on the following pages power the board from the Arduino’s analog pins.

Caution: You can only do this when the device that you are using has very small power requirements. Drawing too much current from the Arduino’s pins can damage the Arduino. If you are unsure about a device, do not connect it this way.

To connect the Adafruit MCP9808 to the Arduino Yún:

1.  Solder the pin strip to the MCP9808 breakout board.
2.  Unplug the power supply from the Arduino Yún.
3.  Gently, but firmly, press the breakout board down into the analog inputs on the Arduino.

![](images/00009.jpeg) 

Figure 8\. Connecting the MCP9808 to the Arduino

This project uses the analog input pins on the Arduino as digital input/output pins. Pins A1 and A2 on the MCP9808 are not used in this project, and they have built-in, pull-down resistors so you can leave them unconnected.

The pins on the MCP9808 breakout board are:

| Pin | Description |
| --- | --- |
| Vdd | Power input. Can be 2.7 V–5.5 V. |
| Gnd | Ground. |
| SCL | I2C clock pin. |
| SDA | I2C data pin. |
| Alert | A pin that can warn you if the temperature changes by a set amount. |
| A0 | I2C address. The default address is 0x18\. If the Arduino brings this pin high then it adds 1 onto the I2C address. |
| A1 | I2C address. The default address is 0x18\. If this pin is high then it adds 2 onto the I2C address. |
| A2 | I2C address. The default address is 0x18\. If this pin is high then it adds 4 onto the I2C address. |

### Writing the Arduino Sketch

In this example, the MCP9808 is not connected to the Arduino using the standard pins for I2C, and so you cannot use the Wire library. To communicate with I2C devices over different pins, you can use the SoftI2CMaster library by Tod E. Kurt.[5](#part0008_split_006.html_fn5)

To install this library on Microsoft Windows or Mac OS X:

1.  If you use Windows: open **Windows Explorer**, and browse to the Arduino IDE’s installation directory.[6](#part0008_split_006.html_fn6) Then double-click **Libraries**.
2.  If you use Mac OS X: open **Finder**, browse to the Arduino IDE’s installation directory, and then double-click **Libraries**.
3.  Make a new directory and call it *SoftI2CMaster*.
4.  Download the *SoftI2CMaster.h* file from the following URL, and save it to the *SoftI2CMaster* directory: [http://arduinomeetslinux.com/download/SoftI2CMaster.h](http://arduinomeetslinux.com/download/SoftI2CMaster.h)
5.  Download the *SoftI2CMaster.cpp* file from the following URL, and save it to the *SoftI2CMaster* directory: [http://arduinomeetslinux.com/download/SoftI2CMaster.cpp](http://arduinomeetslinux.com/download/SoftI2CMaster.cpp)
6.  Restart, or open, the Arduino IDE.

In the Arduino IDE, start a new sketch. In the *setup()* function, add the following code to use two analog pins as a power supply for the MCP9808.

```
pinMode(A0, OUTPUT);        // create Vdd power.
digitalWrite(A0, HIGH);
pinMode(A1, OUTPUT);        // create GND.
digitalWrite(A1, LOW);
```

To use the SoftI2CMaster library, you need to import the library. Add the following code to the top of your sketch:

```
#include <SoftI2CMaster.h>
```

The example code below uses the *Console* class in the Bridge library to display messages. If you upload sketches to your Yún using a USB cable then you can use the *Serial* class and the Serial Monitor instead.

Add these lines to the top of your sketch, underneath the line *#include <SoftI2CMaster.h>*:

```
#include <Bridge.h>
#include <Console.h>

SoftI2CMaster i2c = SoftI2CMaster(A3, A2);
```

To create an instance of *SoftI2CMaster*, you need to pass in the pins that you are using for the *SDA* and *SCL* lines. The code above declares an instance of the *SoftI2CMaster* class, and tells it to use analog pin 3 as the *SDA* line and analog pin 2 as the *SCL* line.

To test the communication between the Arduino and the MCP9808, add the following code to the end of your sketch’s *setup()* function:

```
Bridge.begin();
Console.begin();
while (!Console);
Console.print("Testing I2C connection... ");

i2c.beginTransmission(0x18);
i2c.send(0x07);
i2c.endTransmission();

i2c.requestFrom(0x18);
uint16_t v = i2c.receive();
v <<= 8;
v |= i2c.receive();

Console.println(v, HEX);
```

To run this sketch:

1.  On the toolbar, click **Upload**.
2.  Login to the OpenWrt-Yun command line, and then type the following command and press **Enter**:

    ```
    telnet localhost 6571
    ```

You should see the text *400* (0x0400), which is the correct device ID for the Adafruit MCP9808.

The sketch fetches the device ID by sending the command *0x07* to the I2C address of the MCP9808 (*0x18*). It waits for a response from the same address and then receives the ID as two bytes, which it combines into a single 16-bit value.

If everything is correct so far, add the following function to the sketch:

```
uint16_t getDeviceId() {
    i2c.beginTransmission(0x18);
    i2c.send(0x07);
    i2c.endTransmission();

    i2c.requestFrom(0x18);
    uint16_t v = i2c.receive();
    v <<= 8;
    v |= i2c.receive();
    return v;
}
```

Then change the sketch’s *setup()* function. Replace everything after *Console.print("Testing I2C connection… ");* with:

```
if (getDeviceId() == 0x0400) {
    Console.println("OK.");
}
else {
    Console.println("Error. Could not find Adafruit MCP9808.");
    return;
}
```

The *return* statement in the *setup()* function prevents the sketch from entering the *loop()* function if the MCP9808 is not available.

Add the following function to the sketch:

```
float getTemperature() 
{ 
    i2c.beginTransmission(0x18);
    i2c.send(0x05);
    i2c.endTransmission();

    i2c.requestFrom(0x18);
    uint16_t v = i2c.receive();
    v <<= 8;
    v |= i2c.receive();

    float temp = v & 0x0FFF; 
    temp /= 16.0; 
    if (v & 0x1000) {
        temp -= 256;
    }
    return temp;
}
```

This function fetches the temperature in the same way as the *getDeviceId()* function fetches the device ID. To get a meaningful value, *getTemperature()* converts the value from the MCP9808 into a float that represents the temperature in degrees Celsius.[7](#part0008_split_006.html_fn7)In the sketch’s *loop()* function, add the following code:

```
float temp = getTemperature();
Console.print("Temperature: ");
Console.print(temp, 1);
Console.println("C");
delay(1000);
```

Run the sketch and then reopen the Console connection from the Linux command prompt. You should see the temperature updates every second.

To finish the Arduino sketch, you can store the temperature in the Atheros AR9331’s memory so that your website can read the value and display it.

After the line *Console.println("C");*, add this line:

```
Bridge.put("MCP9808_Temperature", String(temp));
```

To make sure that the sketch runs even if you do not open a Console connection to view the debugging messages, remove the line that reads *while(!Console);* from the *setup()* function.

You can find the full source code for this sketch in [Source Code – Sketch](#part0008_split_003.html_tc5s3s4).

### Creating the Temperature Monitor Website

The steps to display the temperature on a website are:

1.  Create a new website in the uHTTPd server.
2.  Write a Python script to: output the webpage; fetch the temperature from the shared-storage area of the AR9331’s memory; and put the temperature onto the webpage.
3.  Use a cascading style sheet to control the appearance of the webpage.

To begin, you need to create a new website in the configuration file for uHTTPd. For more information, see [Setting Up a Website on the Arduino Yún](#part0008_split_000.html_tc5s1).Add the following configuration options to the website in */etc/config/uhttpd*:

```
option index_page         index.py
option script_timeout     60
list interpreter          ".py=/usr/bin/python"
```

Then restart uHTTPd:

```
/etc/init.d/uhttpd restart
```

This project uses an interpreter setting to run the Python code, because you want the website’s default page to be a script.

At the command prompt, change your working directory to the location of the website. For example, if your website is in the folder */mnt/sda1/www2*, type the following command and then press the Enter key:

```
cd /mnt/sda1/www2
```

Then download the sample website for this project and decompress it.

1.  Type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/download/project1-a.tar.gz
    ```

2.  Type the following command and then press **Enter**:

    ```
    tar -zxvf project1-a.tar.gz
    ```

3.  Type the following command and then press **Enter**:

    ```
    rm project1-a.tar.gz
    ```

There are three directories and one Python script in the sample website:

css/

Contains a cascading style sheet file that makes the HTML look like a wall-mounted temperature monitor.

fonts/

This website uses a web font to simulate the appearance of text on a liquid crystal display (LCD). The files for this web font are in the *fonts* directory.

images/

Contains an image to use as the background for the monitor.

index.py

A server-side Python script that fetches the temperature from the shared-storage area of the AR9331’s memory and sends an HTML page to web browsers. The source code for this file is in [Source Code – Python](#part0008_split_003.html_tc5s3s5).

The script that generates the HTML content for this project is fairly basic.

In [Accessing Stored Data from Python Scripts](#part0007_split_002.html_tc4s2s5), you can see how to import the *BridgeClient* class into a Python script, and how to read the values from the memory area that the ATmega32u4 can access.

*index.py* first reads the temperature that the Arduino sketch places in the AR9331’s memory. It converts the temperature string to a float, so that later it can convert the temperature to Fahrenheit and round it to a single decimal place.

```
client = BridgeClient()
temp = float(client.get("MCP9808_Temperature"))
```

Then it uses the *os* module to check whether the query string is empty. If it is, the script sets the default unit to Fahrenheit.

```
unit = os.environ["QUERY_STRING"]
if unit == "":
    unit = "F"
```

The query string is usually empty until the user clicks the button labelled “°C / °F” on the webpage.

Next, the script finishes the HTTP response header by setting the *Content-Type* to *text/html* so that the web browser knows to expect an HTML page.

Using triple-quoted strings, the script sends HTML code to the web browser. When it needs to place a calculated value (such as the temperature) in that part of the page, it ends the triple-quoted string and prints the value separately.

For example, to add the current time to the HTML output, you can use the code:

```
print """
    </p>
    <p id="time" class="lcd">
"""

print time.strftime("%H:%M")

print """
    </p>
...
```

The text below shows the actual HTML page that this script outputs. The markup code on this page structures the information; it is the CSS file that makes the paragraphs of text look like a wall-mounted panel.

```
<!DOCTYPE html>
<html>
<head>
    <title>Project 1 - Building a Web-Based Temperature Monitor</title>
    <link rel="stylesheet" href="/css/normal.css" type="text/css" />
    <meta http-equiv="refresh" content="10">
    <meta charset="UTF-8">
</head>
<body>
    <div id="panel">
        <p id="temperature" class="lcd">
54.9
        </p>
        <p id="unit" class="lcd">
F
        </p>
        <p id="date" class="lcd">
01/17/2015
        </p>
        <p id="time" class="lcd">
12:34
        </p>
        <input type="button" id="btnUnit" 
               onclick="javascript:location.href='/?C'" value="Unit" />
        <input type="button" id="btnRefresh" 
               onclick="location.reload();" value="Refresh" />
    </div>
</body>
</html>
```

uHTTPd handles all of the other files that the web browser requests – the CSS file, the web font, and the background image.

To view this website:

1.  On a machine connected to the same network as your Arduino, open a web browser.
2.  In the address bar, type the URL that the website uses. For example, if your site listens on port 81, type *http://arduino.local:81*. If your site listens on port 80, you can use *http://arduino.local*

After 10 seconds, the refresh directive in the HTML code tells the web browser to reload the web page. Or you can click the button labelled “REFRESH” to reload the page immediately.

![](images/00010.jpeg) 

Figure 9\. The Arduino temperature monitor

### Source Code – Sketch

```
#include <SoftI2CMaster.h>
#include <Bridge.h>
#include <Console.h>

SoftI2CMaster i2c = SoftI2CMaster(A3, A2);

uint16_t getDeviceId() {
  i2c.beginTransmission(0x18);
  i2c.send(0x07);
  i2c.endTransmission();

  i2c.requestFrom(0x18);
  uint16_t v = i2c.receive();
  v <<= 8;
  v |= i2c.receive();
  return v;
}

float getTemperature() {
  i2c.beginTransmission(0x18);
  i2c.send(0x05);
  i2c.endTransmission();

  i2c.requestFrom(0x18);
  uint16_t v = i2c.receive();
  v <<= 8;
  v |= i2c.receive();

  float temp = v & 0x0FFF;
  temp /= 16.0;
  if (v & 0x1000) {
    temp -= 256;
  }
  return temp;
}

void setup() {
  pinMode(A0, OUTPUT);
  digitalWrite(A0, HIGH);
  pinMode(A1, OUTPUT);
  digitalWrite(A1, LOW);

  Bridge.begin();
  Console.begin();
  Console.print("Testing I2C setup... ");

  if (getDeviceId() == 0x0400) {
    Console.println("OK.");
  } 
  else {
    Console.println("Error. Could not find Adafruit MCP9808.");
    return;
  }
}

void loop() {
  float temp = getTemperature();
  Console.print("Temperature: ");
  Console.print(temp, 1);
  Console.println("C");
  Bridge.put("MCP9808_Temperature", String(temp));
  delay(1000);
}
```

### Source Code – Python

```
#!/usr/bin/python
import sys, time, os
sys.path.insert(0, "/usr/lib/python2.7/bridge/")
from bridgeclient import BridgeClient

client = BridgeClient()
temp = float(client.get("MCP9808_Temperature"))
unit = os.environ["QUERY_STRING"]
if unit == "":
   unit = "F"

print "Content-type: text/html"
print
print """
<!DOCTYPE html>
<html>
<head>
    <title>Project 1 - Building a Web-Based Temperature Monitor</title>
    <link rel="stylesheet" href="/css/normal.css" type="text/css" />
    <meta http-equiv="refresh" content="10">
    <meta charset="UTF-8">
</head>
<body>
    <div id="panel">
        <p id="temperature" class="lcd">
"""

if unit == "F":
    temp = (temp * (9/5)) + 32
print ("%.1f" % temp)

print """
        </p>
        <p id="unit" class="lcd">
"""

print unit

print """
        </p>
        <p id="date" class="lcd">
"""

print time.strftime("%m/%d/%Y")

print """
        </p>
        <p id="time" class="lcd">
"""

print time.strftime("%H:%M")

print """
        </p>
        <input type="button" id="btnUnit" 
"""

if unit == "F":
        print "onclick=\"javascript:location.href='/?C'\""
else:
        print "onclick=\"javascript:location.href='/?F'\""

print """
        value="Unit" />
        <input type="button" id="btnRefresh" onclick="location.reload();" value="Refresh" />
    </div>
</body>
</html>
"""
```

* * *

## Making Web Services and APIs

In programming terms, an application programming interface (API) is a collection of functions or classes. One program can use another’s API to communicate with the second program.

Web services and web APIs are two very similar techniques for using this type of communication over the Internet. Instead of requesting a webpage, programs that call your API specify the function that they want to run. And instead of sending back a web page, your server runs the function and sends back the result. The result is usually not something that you can display on a page – it is in a format that the client program can understand.

You do not need a different type of web server to run web services or web APIs – you can use any server that supports CGI or some form of scripting language.

### Building Web Services on the Arduino Yún (Overview)

A web service is usually defined as a program or script that accepts a request in extensible markup language (XML), and that sends back results in XML. The most common type of web service is simple object access protocol (SOAP). This is particularly well-suited for communication between two desktop applications, or one desktop application and a web server.

Web services usually use an accompanying file that describes all of the functions that the client can call. This file is written (or automatically generated) in web service definition language (WSDL). Several development environments (such as Microsoft Visual Studio) can automatically generate all of the code needed to use a web service from your program, just by analyzing this WSDL file.

Full web services can be difficult to process on the ATmega32u4, and so you should use the Atheros AR9331 and OpenWrt-Yun Linux to do as much of the work as possible.

The process for running a SOAP web service on the Yún comprises the following steps:

1.  Create a web site configuration in */etc/config/uhttpd*.
2.  Write a CGI program or server-side Python script to accept an HTTP request from the client program.
3.  If the HTTP request query string asks for the WSDL specification of the web service: respond with the information and then terminate the connection.
4.  If the client does not ask for the WSDL specification: read the XML request data (as a string) from the HTTP request, and convert it into an XML document. In Python scripts, you can use the *xml* package.
5.  If required, convert any objects or data in the XML document to other data types.
6.  Based on the information in the XML request, run the function that the client specifies.
7.  Collect any response information into an XML document.
8.  Write an HTTP response header, and send the XML response document back to the client.

### Building Web APIs on the Arduino Yún (Overview)

When people refer to a “web API”, they often mean a representational state transfer (REST) API. This is a simplified form of web service that you can use when smaller programs or scripts, running on less-powerful devices, want to use an API.

You can often see RESTful APIs used when JavaScript code in a web browser wants to make an API call on a web server. Many web APIs use JavaScript object notation (JSON) as a way of describing the requests and data objects in a way that web browsers can easily work with.

JSON represents objects and collections of objects in a structured text format – typically organized into key/value pairs, but each value can also be another collection of key/value pairs. The JavaScript interpreter in web browsers can create a data object directly from JSON, and this has helped make it extremely popular for use in web APIs.

A JSON object looks like this:

```
{
  "result": "ok",
  "values": [1, 2, 3, 4, 5, 6, 7, 8, 9]
}
```

When evaluated by the JSON parser, this data creates an object with two properties: *result* (which contains the text string “ok”), and *values* (an array of numbers, 1–9).

Because they are usually a little simpler, RESTful APIs can be run from either an Arduino sketch or from server-side Python scripts on OpenWrt-Yun. However, the AR9331 has much more power and resources than the ATmega32u4, and you should generally try to use this advantage in your projects.

The process for running a JSON-based web API on the Arduino Yún is very similar to that of running a web service:

1.  Create a web site configuration in */etc/config/uhttpd*.
2.  Write a CGI program or server-side Python script to accept an HTTP request from the web browser.
3.  Read the JSON request data (as a string) from the HTTP request, and then convert it into a structure that the CGI program or script can work with. In Python, you can convert the JSON data to a *dictionary* object using the *json* module.
4.  Based on the information in the JSON request, run the function that the browser specifies.
5.  Collect any response information into a response object.
6.  Convert this object into a JSON string.
7.  Write an HTTP response header, and send the JSON response back to the web browser.

* * *

## Project 2 – Controlling an LED Matrix through a Web API

In this project, you can see two ways of building an API on the Arduino Yún. In the first, you use a script built-in to OpenWrt-Yun to pass information from a web browser to the ATmega32u4\. The second part of this project describes some of the limitations of building an API in this way. It shows how to build an API in Python on the Atheros AR9331 and pass information to the ATmega32u4 through the Console.

This project uses an Adafruit 8x8 LED matrix and a custom website. If you open the site in a web browser, you can click the “LED” buttons on the webpage to turn the actual LEDs in the matrix on or off. Both versions of this project create a JavaScript object notation (JSON) API.

To complete this project, you need:

1.  An Arduino Yún, connected to your local network over Ethernet or Wi-Fi.
2.  A microSD card, formatted for use with the Yún.
3.  An Adafruit Mini 0.8” or 1.2” 8x8 LED Matrix with I2C backpack.
4.  A solderless breadboard and jumper wires.

### Connecting the 8x8 LED Matrix to the Yún

The Adafruit 8x8 LED matrix connects using four pins. These pins are labelled *+*, *-*, *D*, and *C*.

| Pin | Description |
| --- | --- |
| + | Power supply. Connect this to the Arduino’s *5V* pin. |
| - | Ground. Connect this to an Arduino *GND* pin. |
| D | I2C data pin (SDA). Connect this to digital pin 2 on the Arduino. |
| C | I2C clock pin (SCL). Connect this to digital pin 3 on the Arduino. |

To connect the matrix:

1.  Disconnect the Arduino from its power source.
2.  Gently, but firmly, press the header pins on the LED matrix into a breadboard.
3.  Connect jumper wires between the pin headers on the LED matrix and the Arduino.
4.  Reconnect the Arduino’s power supply.

![](images/00011.jpeg) 

Figure 10\. Connecting an Adafruit 8x8 LED matrix to the Arduino

### Building the Website

If you have previously created your own website in uHTTPd’s main configuration file and moved the Arduino Yún’s administration panels to a different port, you need the port number of the default site. To check this:

1.  Login to the OpenWrt-Yun command line.
2.  Type the following command and then press **Enter**:

    ```
    nano /etc/config/uhttpd
    ```

In the section labelled “config uhttpd main”, make a note of the value in the *list listen_http* setting. This should be an IP address followed by a colon and then the port number.

Close nano, and then type the following command and press the Enter key:

```
cd /www/sd
```

*/www/sd *is a symbolic link that makes the files in the directory */mnt/sda1/arduino/www*[8](#part0008_split_006.html_fn8)accessible from uHTTPd’s web files directory. If your microSD card does not have an */arduino/www* directory, the *cd* command fails.

To create the directory:

```
mkdir /mnt/sda1/arduino
mkdir /mnt/sda1/arduino/www
```

Create a new directory for the website files. For example,

*   Type the following command and then press **Enter**:

    ```
    mkdir /www/sd/LED && cd /www/sd/LED
    ```

To download the sample website for this project and put it on your microSD card,

1.  Type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/download/project2-a.tar.gz
    ```

2.  Type the following command and then press **Enter**:

    ```
    tar -zxvf project2-a.tar.gz
    ```

3.  Type the following command and then press **Enter**:

    ```
    rm project2-a.tar.gz
    ```

There are three directories and one HTML file in the sample website:

css/

Contains a cascading style sheet file that makes the HTML look like an Adafruit 8x8 LED matrix.

images/

Contains a background and button images.

scripts/

This project uses jQuery (a library that extends JavaScript). The jQuery library is in here.

index.html

Contains HTML and JavaScript code to display the matrix in the web browser. The JavaScript code creates the “LED” buttons the page, and sends click information to the Arduino sketch.

Tip: It is beyond the scope of this book to fully explain JavaScript and jQuery. But you can see how jQuery sends data to the Arduino in the next section of this chapter.

The URL that you use to access the website is:

*   *http://arduino.local/sd/LED/* if you have the administration panels on TCP port 80, and the website files are in a directory called “LED” in the */www/sd* directory.
*   *http://arduino.local:<PORT>/sd/LED/* if you have the administration panels on a different TCP port, and the website files are in the directory */www/sd/LED*.

![](images/00012.jpeg) 

Figure 11\. The LED matrix web interface

### Writing an Arduino Sketch to Receive Information from jQuery

When someone clicks an LED button in the sample website, a piece of jQuery code runs and sends a command to the URL *http://arduino.local/arduino* (or *http://arduino.local:PORT/arduino* if you are not using TCP port 80).

LEDs on the Adafruit matrix are arranged like a table. There are eight columns, and each column has eight rows.To turn on an LED, the script makes a request to *http://arduino.local/arduino/on/X/Y*, where

X

Is a number from 0 through 7 and states which column of the matrix contains the LED that the sketch should turn on.

Y

Is a number from 0 through 7 and states which row of the matrix contains the LED that the sketch should turn on.

To turn off an LED, the script makes a request to *http://arduino.local/arduino/off/X/Y*.

The jQuery code that sends these commands looks like this:

```
var jq = $.getJSON(call)
    .done(function (json) {
        if (json.result) {
            console.log("OK.")
        } else {
            console.log("API Error: Invalid LED coordinates.");
        }
    })
    .fail(function (jqxhr, textStatus, error) {
        var err = textStatus + ", " + error;
        console.log("API Error: " + err);
    });
```

The variable *call* contains the URL and command that you want to send to the Arduino sketch, and the *$.getJSON()* function makes the HTTP request.

This script sets up two functions that run depending on the result of the HTTP request. If the server receives the request and responds, the script runs the *.done()*function. If the request fails, the script runs the *.fail()* function.

*.done()* expects the server to send back a response in JSON format. The response should contain at least one variable, *result*. If *result* is zero then the script assumes that the Arduino sketch rejected the command. Note: this script takes no action if errors occur – the *.done()* and *.fail()* functions are here only as an example.

A successful response from the Arduino sketch looks like:

```
{ "result" : 1 }
```

When the web browser first displays the web page, the script makes a different request to the Arduino sketch. It makes a request to the URL *http://arduino.local/arduino/get*, and the sketch sends back a multidimensional array of 1s and 0s. This array matches the layout of the LED matrix. A *1* indicates that the LED is lit, and a *0* indicates that the LED is not lit. This means that if you reload the webpage, the script can make the interface look like the actual LED matrix.

OpenWrt-Yun contains a script that extracts everything after “http://arduino.local/arduino/” from the URL, and then sends it to the ATmega32u4 using TCP port 5555\. To receive the information on the Arduino side of the Yún, you can use the *YunServer* and *YunClient* classes from the Bridge library.

Tip: You can also use the Mailbox to receive this information from the web browser. The Mailbox is explained in [Using Mailbox and Sending Messages](#part0007_split_005.html_tc4s6). However, the Mailbox is less useful for sending back responses to the browser and so this project uses *YunServer* and *YunClient*.

For the sample website to work, you need to set the Arduino’s REST API to allow connections without a username and password. To change the REST API setting:

1.  On a machine that connects to the same network as the Arduino, open a web browser.
2.  In the address bar, type *http://arduino.local*[9](#part0008_split_006.html_fn9) and then press **Enter**.
3.  Type the current password[10](#part0008_split_006.html_fn10) and then click **LOG IN**.
4.  Click **CONFIGURE**.
5.  Scroll to the bottom of the page, and under **REST API ACCESS**, click the **Open** box.

There are two advantages to using the */arduino* script instead of pointing the web browser directly to *http://arduino.local:5555/*:

1.  The */arduino* script removes all of the HTTP headers so that you do not have to process them before you can access the data from the webpage.
2.  Non-standard TCP ports (ports that are not 80, or 443) are often blocked by public Internet connections, such as in Internet cafés and offices. If you run the Arduino’s administration panels on TCP port 80 and allow incoming connections on your router, everyone can access the */arduino* script.

To build the Arduino sketch, start a new sketch in the Arduino IDE and add the following code:

```
#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>

YunServer srv;

void setup() {
    Bridge.begin();

    srv.listenOnLocalhost();
    srv.begin();
}

void loop() {
    YunClient yc = srv.accept();
    if (yc) {
        yc.stop();
    }
}
```

The line that reads *YunServer srv;* creates an instance of the *YunServer* class. You can use this class when you want to receive incoming connections across the network.

*YunServer* contains only five methods:

| Method | Description |
| --- | --- |
| listenOnLocalhost() | Configures the instance of *YunServer* to listen for connections that come in on TCP port 5555 using the host name *localhost* or IP address 127.0.0.1. |
| noListenOnLocalhost() | Configures the instance of *YunServer* so that it does not listen for connections that use the host name *localhost* or IP address 127.0.0.1. |
| begin() | Starts listening for incoming connections. |
| accept() | If there is an incoming connection, *accept()* opens it and returns an instance of the *YunClient* class so that your sketch can exchange information with the client. |
| write() | If you have multiple client connections open at the same time, *write()* sends information to all of them at the same time. |

*YunServer* is automatically configured to listen for incoming connections on port 5555\. But because the */arduino* script connects to the Yún using *localhost* references, you need to enable these with the *listenOnLocalhost()* method.

Then all the *setup()* function needs to do is tell the server to start listening, using the *begin()* method.

Code in the sketch’s *loop()* function continually checks if there is an incoming request. If there is, it accepts the connection and obtains an instance of the *YunClient* class. The code in the *loop()* function then checks if it is a valid connection and immediately closes it using the *stop()* method.

The instance of the *YunClient* class that the sketch obtains from *YunServer*’s *accept()* method, represents an open connection to a web browser (or other client). It contains methods for reading information from the client, and sending back responses.

Tip: You can also use *YunClient* to initiate connections to servers. To do this: create a new instance of *YunClient*; call the *connect()* method, and pass in the IP address or domain name of the server and the TCP port to use.

| Method | Description |
| --- | --- |
| available() | If the client sends data to the Arduino, this method returns the number of bytes of data that you have not yet read. |
| connect() | Initiates connections with servers. |
| connected() | Returns *true* if there is an open connection to a client, or *false* if the connection is closed. |
| flush() | Ensures that any bytes that you have written with calls to *write()*, are sent to the web browser immediately. |
| peek() | Reads a byte from the client but does not remove it from the buffer. The next call to *peek()*, *read()*, *readBytes()*, *readBytesUntil()*, *readString()* or *readStringUntil()* returns the same byte. |
| print() | Prints data to the client as human-readable text. Works the same way as *Serial.print()*. |
| println() | Prints data to the client as human-readable text and adds on a line break character. Works the same way as *Serial.println()*. |
| read() | If you do not pass in any arguments, *read()* returns the next byte from the client. If you pass in an array (or pointer to an area of memory) and an integer specifying the number of bytes to read, then you can read multiple bytes with a single call to *read()*. |
| readBytes() | Reads from the client until the connection ends or the method receives no data. Then the method returns all of the data as an array of bytes. |
| readBytesUntil(char) | Reads from the client until the method receives the specified character, the connection ends, or the method receives no data. Then the method returns all of the data as an array of bytes. |
| readString() | Reads from the client until the connection ends or the method receives no data. Then the method returns all of the data as a string. |
| readStringUntil(char) | Reads from the client until the method receives the specified character, the connection ends, or the method receives no data. Then the method returns all of the data as a string. |
| stop() | Closes the connection to the client. |
| write() | Write a byte (or multiple bytes using a buffer array and an integer specifying the number of bytes) to the client. |

Before you can respond to incoming requests in this project, add the following line underneath the line that reads *YunServer srv;*:

```
byte matrix[8][8];
```

This creates a multidimensional array in the sketch. This array stores information about which LEDs are lit, and which LEDs are not lit.

Add the following function to the sketch:

```
int ctoi(char a) {
    if ( (a >= '0') && (a <= '7') ) {
        return a-48;
    }
    else {
        return -1;
    }
}
```

*ctoi()* converts a single ASCII character to a number. It only supports the values 0 through 7, because the LED matrix only has eight rows and eight columns. For example, *ctoi('0')* converts the ASCII character that looks a zero (but is actually the number 48) to an actual zero.

When your Arduino sketch receives an incoming connection from the */arduino* script, you need to read the commands that the web browser sends. You can do this using the *readString()* method.

Before the line that reads *yc.stop();*, add the following line:

```
String cmd = yc.readString();
```

You can then check which command the browser sends by using the *startsWith()* method of the string object. Add the following code underneath the previous line:

```
if (cmd.startsWith(F("on/"))) {
}
else if (cmd.startsWith(F("off/"))) {
}
else if (cmd.startsWith(F("get"))) {
}
```

Tip: Using strings to process data can take up a lot of memory. If you surround a string literal with *F()* then you can ensure that the Arduino access the string from program ROM, and does not use the RAM area.

If the browser sends the *on* or *off* command, the sketch needs to convert the *x* and *y* values from the request into usable numbers.

Add these lines into the code that runs if the command starts with “on/”:

```
int x = ctoi(cmd[3]);
int y = ctoi(cmd[5]);
if ( (x > -1) && (y > -1) ) {
    matrix[x][y] = 1;
    yc.print(F("{\"result\":1}"));
}
else {
    yc.print(F("{\"result\":0}"));
}
```

You can use square brackets to access the individual characters that make up a string. The first character is at position 0\. So the code above extracts the fourth and sixth characters from the string “on/X/Y” and converts each value to a number. It then checks that the numbers are valid.

If both *x* and *y* are valid, then the sketch sets the matching value in the *matrix* array to *1*. It then sends back a JSON string with the result ‘1’. If either *x* or *y* are invalid, the sketch sends back a JSON string with the result ‘0’.

The process for handling *off* commands is largely the same. Add the following lines to the code that runs if the command starts with “off/”:

```
int x = ctoi(cmd[4]);
int y = ctoi(cmd[6]);
if ( (x > -1) && (y > -1) ) {
    matrix[x][y] = 0;
    yc.print(F("{\"result\":1}"));
}
else {
    yc.print(F("{\"result\":0}"));
}
```

To handle the *get* command, you need to send back a JSON string that describes the state of each LED in the matrix. A valid response for this looks like the following example:

```
{ "result": 1,
  "LEDs": [
      [1, 0, 0, 0, 0, 0, 0, 0],
      [0, 1, 0, 0, 0, 0, 0, 0],
      [0, 0, 1, 0, 0, 0, 0, 0],
      [0, 0, 0, 1, 0, 0, 0, 0],
      [0, 0, 0, 0, 1, 0, 0, 0],
      [0, 0, 0, 0, 0, 1, 0, 0],
      [0, 0, 0, 0, 0, 0, 1, 0],
      [0, 0, 0, 0, 0, 0, 0, 1]
  ]
}
```

To create this kind of response in the Arduino sketch, you can paste the code below into the code that runs if *cmd* starts with “get”:

```
yc.print(F("{\"result\":1,\"LEDs\":["));
for (int x=0; x<8; x++) {
    yc.print('['];
    for (int y=0; y<8; y++) {
        if (matrix[x][y]) {
            yc.print('1');
        }
        else {
            yc.print('0');
        }
        if (y < 7) {
            yc.print(',');
        }
    }
    yc.print(']');
    if (x < 7) {
        yc.print(',');
    }
}
yc.print(']');
yc.print('}');
```

The full source code for the sketch so far is shown below. Upload the sketch to your Yún, and then open a web browser that is on the same network as your Arduino. Open the webpage, and then click a few “LED” buttons to turn them on.

```
#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>

YunServer srv;
byte matrix[8][8];

void setup() {
    Bridge.begin();

    srv.listenOnLocalhost();
    srv.begin();
}

void loop() {
    YunClient yc = srv.accept();
    if (yc) {
        String cmd = yc.readString();
        if (cmd.startsWith(F("on/"))) {
            int x = ctoi(cmd[3]);
            int y = ctoi(cmd[5]);
            if ( (x > -1) && (y > -1) ) {
                matrix[x][y] = 1;
                yc.print(F("{\"result\":1}"));
            }
            else {
                yc.print(F("{\"result\":0}"));
            }
        }
        else if (cmd.startsWith(F("off/"))) {
            int x = ctoi(cmd[4]);
            int y = ctoi(cmd[6]);
            if ( (x > -1) && (y > -1) ) {
                matrix[x][y] = 0;
                yc.print(F("{\"result\":1}"));
            }
            else {
                yc.print(F("{\"result\":0}"));
            }
        }
        else if (cmd.startsWith(F("get"))) {
            yc.print(F("{\"result\":1,\"LEDs\":["));
            for (int x=0; x<8; x++) {
                yc.print('['];
                for (int y=0; y<8; y++) {
                    if (matrix[x][y]) {
                        yc.print('1');
                    }
                    else {
                        yc.print('0');
                    }
                    if (y < 7) {
                        yc.print(',');
                    }
                }
                yc.print(']');
                if (x < 7) {
                    yc.print(',');
                }
            }
            yc.print(']');
            yc.print('}');
        }
        yc.stop();
    }
}

int ctoi(char a) {
    if ( (a >= '0') && (a <= '7') ) {
        return a-48;
    } else {
        return -1;
    }
}
```

If everything is working correctly then you should be able to reload the webpage (or open it on another computer) and see the same pattern. In the next section, you will use this functionality to control the LEDs on the Adafruit matrix.

### Controlling the Adafruit 8x8 LED Matrix

Adafruit supply full libraries and sample code for their LED matrices. However, this project does not use the Adafruit libraries. You can communicate directly with the LED matrix using I2C and the SoftI2CMaster library by Tod E. Kurt.[11](#part0008_split_006.html_fn11) To install this library on Microsoft Windows or Mac OS X:

1.  If you use Windows: open **Windows Explorer**, and browse to the Arduino IDE’s installation directory.[12](#part0008_split_006.html_fn12) Then double-click **Libraries**.
2.  If you use Mac OS X: open **Finder**, browse to the Arduino IDE’s installation directory, and then double-click **Libraries**.
3.  Make a new directory and call it *SoftI2CMaster*.
4.  Download the *SoftI2CMaster.h* file from the following URL, and save it to the *SoftI2CMaster* directory: [http://arduinomeetslinux.com/download/SoftI2CMaster.h](http://arduinomeetslinux.com/download/SoftI2CMaster.cpp)
5.  Download the *SoftI2CMaster.cpp* file from the following URL, and save it to the *SoftI2CMaster* directory: [http://arduinomeetslinux.com/download/SoftI2CMaster.cpp](http://arduinomeetslinux.com/download/SoftI2CMaster.cpp)
6.  Restart the Arduino IDE.
7.  Reload your sketch.

Include the SoftI2CMaster library in your sketch by adding the following line to the top of your code:

```
#include <SoftI2CMaster.h>
```

Then underneath the line that reads *YunServer srv;*, add the following line:

```
SoftI2CMaster i2c = SoftI2CMaster(2, 3);
```

To create an instance of *SoftI2CMaster*, you need to pass in the pins that you are using for the *SDA* and *SCL* lines. The code above declares an instance of the *SoftI2CMaster* class, and tells it to use digital pin 2 as the *SDA* line and digital pin 3 as the *SCL* line.

The LED matrix responds to I2C address 0x70.

To make the LED matrix work in this sketch, you need to perform a few short initialization routines. Add these two functions to the sketch:

```
void setBlinkRate(uint8_t b) {
    if (b > 3) {
      b = 3;
    }
    i2c.beginTransmission(0x70);
    i2c.send((byte)(0x81 | (b << 1)));
    i2c.endTransmission();
}

void setBrightness(uint8_t b) {
    if (b > 15) {
        b = 15;
    }
    i2c.beginTransmission(0x70);
    i2c.send((byte)(0xE0 | b));
    i2c.endTransmission();
}
```

In your sketch’s *setup()* function, add the following code:

```
i2c.beginTransmission(0x70);
i2c.send(0x21);
i2c.endTransmission();
setBlinkRate(0);
setBrightness(3);
```

The first I2C transmission makes the LED matrix active, but the process must be completed by setting the blink rate to *0*. The *setBrightness()* function accepts an integer from 0 through 15, and it controls the brightness of all the LEDs (with 15 being very bright).

To update the LED display, you need to make an I2C transmission that sends all of the information from the *matrix* array. However, the Adafruit LED matrix uses a different method of representing the state of each LED.

*matrix* uses a byte for each LED – with *1* meaning that the LED is on, and *0* meaning that the LED is off. The HT16K33 driver chip on the Adafruit board uses a 16-bit number to represent an entire row of LEDs. Eight bits of that number represent the eight different LEDs in that row. If a bit is set, the LED is on. If a bit is clear, the LED is off.

The least-significant bit (bit 0) does not control the first LED in the row. It controls the second LED. The first LED is actually bit 7.

To handle all this in the Arduino sketch, create the function below:

```
void reDisplay() {
    i2c.beginTransmission(0x70);
    i2c.send(0x00);
    for (byte y=0; y<8; y++) {
        byte tmp = 0;
        for (byte x=0; x<8; x++) {
            if (matrix[y][x]) {
                if (x == 0) {
                    tmp |= 0x80;
                }
                else {
                    tmp |= 1 << (x-1);
                }
            }
        }
        i2c.send(tmp);
        i2c.send(0x00);
    }
    i2c.endTransmission();
}
```

The first value that the function sends to the LED matrix is a zero. This tells the driver chip that it should start at its first memory location and then store everything that follows. It automatically moves to the next memory address every time it receives a 16-bit number.

The *reDisplay()* function loops through the *matrix* array in a different way than the other parts of the sketch. For each row, it assigns a zero to the variable *tmp*. Then it looks at each column in that row. If the value is *1*, it sets the appropriate bit in *tmp*. For the first LED, this is bit 7\. For the other LEDs, the bit number is one less than the position of the LED in matrix.

The *reDisplay()* function does not have to do anything if an LED is not lit, because it initializes *tmp* to zero (all LEDs off) and only turns on LEDs that are *1* in *matrix*.

When the value for *tmp* is calculated, the function sends it to the LED matrix. Since the HT16K33 driver expects a 16-bit number, the function also sends an additional byte (zero).

To complete this part of the project, add a call to *reDisplay()* to the end of the Arduino sketch’s *loop()* function. The full source code for this sketch is in [Source Code – Sketch](#part0008_split_005.html_tc5s5s6).

Upload the sketch to the Arduino, and test the project from a web browser.

There can be a short delay between clicking on an LED in the web browser and the display changing on the LED matrix. Opening connections to web servers can take several seconds, and this project is inefficient in that it makes a very short request every time the user clicks an LED.

### Moving the Project to Its Own Website

This project uses the */arduino* script that is part of the Arduino Yún’s administration panels, and stores the website files in the main site’s directory. Whatever port the site uses has to be accessible to the computers that want to load the webpage.

If you want to run this project from a new website (and move the administration panels to a different port), then you can do this in the */etc/config/uhttpd* file. For more information about using a different TCP port for the administration panels, see [Changing the TCP Port Number of the Administration Panels](#part0008_split_001.html_tc5s1s3).

The site that you create for this project should have the following setting:

```
option index_page         index.html 
```

However, if you move the Yún’s default website to a different port then you also have to change the JavaScript code to tell web browsers where to find the */arduino* script.

For example, if the default website is on TCP port 81, edit the file *index.html* and change the line that reads *api = "/arduino/";* to

```
api = "http://arduino.local:81/arduino/";
```

Accessing the */arduino* script this way fails if the web browser cannot connect on TCP port 81\. The visitor’s Internet connection may not allow them to make connections on that port, or your router configuration may not allow incoming connections on that port.

To make the */arduino* script available to your custom website, you can write a short server-side Python script that receives the information from the web browser and then forwards this to the */arduino* script on the correct port. This script also has to retrieve the response from */arduino* and send this back to the web browser.

Add the following settings to your website in */etc/config/uhttpd* and then restart the server:

```
option script_timeout     60
list interpreter          ".py=/usr/bin/python"
```

Then create the following Python script in your site’s directory, and name it *api.py*.

```
#!/usr/bin/python
import os, urllib
u = os.environ["QUERY_STRING"]
print "Content-type: application/json"
print
h = urllib.urlopen("http://127.0.0.1:81/arduino/" + u).read();
print h
```

If your Yún’s administration panels are not on TCP port 81, replace *81* with the port number that they use.

Edit the file *index.html* and change the line that reads *api = "/arduino/";* to

```
api = "api.py?";
```

### Source Code – Sketch

```
#include <SoftI2CMaster.h>
#include <Bridge.h>
#include <YunServer.h>
#include <YunClient.h>

YunServer srv;
SoftI2CMaster i2c = SoftI2CMaster(2, 3);
byte matrix[8][8];

int ctoi(char a) {
    if ( (a >= '0') && (a <= '7') ) {
        return a-48;
    } else {
        return -1;
    }
}

void reDisplay() {
    i2c.beginTransmission(0x70);
    i2c.send(0x00);
    for (byte y=0; y<8; y++) {
        byte tmp = 0;
        for (byte x=0; x<8; x++) {
            if (matrix[y][x]) {
                if (x == 0) {
                    tmp |= 0x80;
                }
                else {
                    tmp |= 1 << (x-1);
                }
            }
        }
        i2c.send(tmp);
        i2c.send(0x00);
    }
    i2c.endTransmission();
}

void setBlinkRate(uint8_t b) {
    if (b > 3) {
      b = 3;
    }
    i2c.beginTransmission(0x70);
    i2c.send((byte)(0x81 | (b << 1)));
    i2c.endTransmission();
}

void setBrightness(uint8_t b) {
    if (b > 15) {
        b = 15;
    }
    i2c.beginTransmission(0x70);
    i2c.send((byte)(0xE0 | b));
    i2c.endTransmission();
}

void setup() {
    i2c.beginTransmission(0x70);
    i2c.send(0x21);
    i2c.endTransmission();
    setBlinkRate(0);
    setBrightness(3);

    Bridge.begin();

    srv.listenOnLocalhost();
    srv.begin();
}

void loop() {
    YunClient yc = srv.accept();
    if (yc) {
        String cmd = yc.readString();
        if (cmd.startsWith(F("on/"))) {
            int x = ctoi(cmd[3]);
            int y = ctoi(cmd[5]);
            if ( (x > -1) && (y > -1) ) {
                matrix[x][y] = 1;
                yc.print(F("{\"result\":1}"));
            }
            else {
                yc.print(F("{\"result\":0}"));
            }
        }
        else if (cmd.startsWith(F("off/"))) {
            int x = ctoi(cmd[4]);
            int y = ctoi(cmd[6]);
            if ( (x > -1) && (y > -1) ) {
                matrix[x][y] = 0;
                yc.print(F("{\"result\":1}"));
            }
            else {
                yc.print(F("{\"result\":0}"));
            }
        }
        else if (cmd.startsWith(F("get"))) {
            yc.print(F("{\"result\":1,\"LEDs\":["));
            for (int x=0; x<8; x++) {
                yc.print('['];
                for (int y=0; y<8; y++) {
                    if (matrix[x][y]) {
                        yc.print('1');
                    }
                    else {
                        yc.print('0');
                    }
                    if (y < 7) {
                        yc.print(',');
                    }
                }
                yc.print(']');
                if (x < 7) {
                    yc.print(',');
                }
            }
            yc.print(']');
            yc.print('}');
        }
        yc.stop();
    }
    reDisplay();
}
```

### Building an API in Python

Using */arduino* to create a web services and web APIs on the Arduino Yún has two significant disadvantages:

1.  If you use a Python script to forward the information from the web browser to the */arduino* script, it causes an additional delay.
2.  The */arduino*script only passes on information that the web browser sends in the query string. Full SOAP web services and web APIs can send complicated objects in the body of their HTTP request. */arduino* cannot accept this and so you cannot use it to build full APIs.

You can use a server-side Python script (as in the previous section) to forward information from the web browser, directly to the ATmega32u4 over port 5555\. However, you then have to do a lot of work to process the HTTP request and perform additional API tasks that are not directly related to turning on LEDs. This approach can use a lot of memory on the ATmega32u4 and can take a lot of program code.

When building projects for the Arduino Yún, try to use the Linux side as much as possible. It has a lot more power and resources than the Arduino side.

In the following sections, you can see how to revise Project 2 to run a JSON API from Python on the Arduino Yún. In this example, the AR9331 sends information to the ATmega32u4 using the Console.

Tip: If you want to download the modified website files and completed Python script, you can do so from [http://www.arduinomeetslinux.com/download/project2-b.tar.gz](http://www.arduinomeetslinux.com/download/project2-b.tar.gz)

To begin, create a new website and, in */etc/config/uhttpd*, set the following options:

```
option cgi_prefix         /api
option max_requests       200
option script_timeout     60
```

URLs for APIs usually do not use file extensions. By using a cgi-bin, you can write server-side Python scripts that reside in the cgi-bin and have no file extension.

If you click the “LED” buttons on the webpage rapidly, the JavaScript code sends multiple HTTP requests to the Arduino at the same time. If *max_requests* is lower than the number of requests that the browser sends to your Arduino, then uHTTPd may ignore some of them.

Make an *api* directory inside the directory on the microSD card that contains the files for this web site.

You can also find the Python script in [Source Code – Python](#part0008_split_005.html_tc5s5s11). But if you want to create the file yourself: inside the *api* directory, start a new Python script – call it *leds* and do not give it a file extension.

Add the following code to the file:

```
#!/usr/bin/python
import json, os, socket, sys
res = { "result":0 }

def on(x, y):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("localhost", 6571))
    s.send("on/" + x + "/" + y + "\00")
    s.close()
    res["result"] = 1

def off(x, y):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("localhost", 6571))
    s.send("off/" + x + "/" + y + "\00")
    s.close()
    res["result"] = 1

def get():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("localhost", 6571))
    s.send("get\00")
    res["result"] = 1
    matrix = [[0 for x in range(8)] for y in range(8)]
    for y in range(0, 8):
        for x in range(0, 8):
            matrix[x][y] = s.recv(1)
    res["LEDs"] = matrix
    s.close()

print "Content-type: application/json"
print
print json.dumps(res)
```

The script contains three functions that you want to make available to the web browser: *on()*, *off()*, and *get()*. The first two functions open a Console connection to ATmega32u4, send a command, and then close the connection.The third function, *get()*, does not close the Console connection immediately because it needs a response from the Arduino sketch. It builds a two dimensional array and reads the LED status information from the Console connection. Finally, it adds the array to the *res* object that the script sends back to the browser.Each function adds a null (0) to the end of the command string. This helps the Arduino sketch process the commands.The Python module *json* contains functions to help you convert Python objects to JSON strings, and JSON strings to Python objects. This example script creates a dictionary, and sends it to the browser as the result of the API call. The method *dumps()* converts the dictionary to a JSON string that the JavaScript code on the webpage can understand. *dumps()* accepts most types of Python object.

Tip: JSON APIs put the name of the function that they call in the URL. For large projects, you can place code for each method in its own Python script inside the *api* directory.

To complete the script, you need to work out which of the three functions you should run. In the next section, you can see how to modify the JavaScript code in the web page to send JSON requests using the HTTP “POST” method. POST is a more appropriate request method when you send large or complicated information to the web server. Instead of putting the information in the query string, the web browser sends the data after the HTTP request headers.

To retrieve the POST data from a Python CGI script, you need to read from the *sys.stdin* object. The CGI environment variable *CONTENT_LENGTH* contains the numbers of bytes of data that the browser sends after its HTTP request headers. Since the environment variable is a string, you need to convert it to an integer.

After the three function definitions, add the following lines:

```
try:
    if os.environ["REQUEST_METHOD"] == "POST":
        data = sys.stdin.read(int(os.environ["CONTENT_LENGTH"]))
        js = json.loads(data)
except:
    pass
```

If there is an error processing the request, the *try* and *except* statements ensure that the script does not end with an error message, and that it still sends back the *res* object with the *result* property in its default state (0).

The *loads()* method of the *json* module converts the JSON string from the web browser into a usable Python object – usually a dictionary.

In this example, the web browser sends a JSON object that has up to three properties: *cmd*, *x*, and *y*. *cmd* is always present, but the browser only sends *x* and *y* if it calls the *on()* or *off()* functions. To run the appropriate method, add the following code before the *except* statement:

```
if js["cmd"] == "on":
    on(js["x"], js["y"])
elif js["cmd"] == "off":
    off(js["x"], js["y"])
elif js["cmd"] == "get":
    get()
```

Tip: There are various frameworks available for Python that handle this logic for you – automatically calling methods depending on the information that the web browser sends. The most common of these is “Flask”. However, Flask runs as a separate web server and so you can have problems using both uHTTPd and Flask at the same time.

To use this Python script as your API, you need to make a few small changes the Arduino sketch and then modify the JavaScript code in the webpage.

### Modifying the Arduino Sketch

The Arduino sketch for the Python-based API does not use the *YunClient* and *YunServer* classes to communicate with the AR9331\. Instead, it uses the Console connection.

To keep the amount of changes to a minimum, the Python script sends commands in the same format as the webpage in the previous example. In your future projects, you may have to implement better methods of sending data through the Console. And you should perform more error checking than this example sketch does.

There is one issue to be aware of. When the web browser (or multiple web browsers) sends many HTTP requests to uHTTPd at the same time, uHTTPd starts multiple copies of the Python script. All of these scripts then access the same Console connection.

If you use the *Console.readString()*method then you can sometimes find that there are multiple commands in one string. This does not happen in the previous sketch because, when using *YunClient* and *YunServer*, you only read data from one connection at a time.

The Python script adds a null (0) to the end of each command, so that the Arduino sketch can separate the commands if they appear as one string. Instead of using *Console.readString()*, you can use the *Console.readStringUntil()*method and pass in zero. This means that the method stops when it reaches the null, and so the sketch reads each command one at a time.

To modify the Arduino sketch:

1.  Open the sketch in the Arduino IDE.
2.  Remove the following two lines:

    ```
    #include <YunServer.h>
    #include <YunClient.h>
    ```

3.  Add this line:

    ```
    #include <Console.h>
    ```

4.  Remove these three lines:

    ```
    YunServer srv;
    srv.listenOnLocalhost();
    srv.begin();
    ```

5.  In the sketch’s *setup()* function, add the following code:

    ```
    Console.begin();
    ```

6.  Remove the existing *loop()* function, and then add the following code:

    ```
    void loop() {
        String cmd = Console.readStringUntil(0);
        if (cmd.startsWith(F("on/"))) {
            int x = ctoi(cmd[3]);
            int y = ctoi(cmd[5]);
            if ((x > -1) && (y > -1)) {
               matrix[x][y] = 1;
            }
        }
        else if (cmd.startsWith(F("off/"))) {
            int x = ctoi(cmd[4]);
            int y = ctoi(cmd[6]);
            if ((x > -1) && (y > -1)) {
                matrix[x][y] = 0;
            }
        }
        else if (cmd.startsWith(F("get"))) {
            for (int y=0; y<8; y++) {
               for (int x=0; x<8; x++) {
                  if (matrix[x][y]) {
                       Console.write('1');
                   }
                   else {
                       Console.write('0');
                   }
                }
            }
        }
        reDisplay();
    }
    ```

The full source code for this sketch is in [Source Code – Sketch](#part0008_split_005.html_tc5s5s10).

The other difference between this sketch and the previous one is that to handle a *get* command, the sketch dumps the contents of the *matrix* array out to the Console as a sequence of the characters ‘1’ or ‘0’. The Python script reads each character and builds an array from this information.

### Modifying the Website

You can download an archive of the files needed for this website at [http://www.arduinomeetslinux.com/download/project2-b.tar.gz](http://www.arduinomeetslinux.com/download/project2-b.tar.gz)

The *index.html* file contains several changes to the JavaScript code:

1.  The URL of the API is now *http://arduino.local/api/leds* (or *http://arduino.local:<PORT>/api/leds* if you are not using TCP port 80 for your website).
2.  Instead of appending command information to the API URL, the JavaScript uses the *$.post()* function to send an object (containing a command, and optionally two numbers representing the location of the LED) in an HTTP POST request.
3.  To convert a JavaScript object to a JSON string, you use the method *JSON.stringify()*.

Inside the *api* directory of the sample files, you can find the Python script for the Python JSON API.

This project only sends small pieces of information to the Arduino. But by using JSON in the web browser and the *json* module in a Python-based API, you can exchange very large and very complicated objects between the client and server.

### Source Code – Sketch

```
#include <SoftI2CMaster.h>
#include <Bridge.h>
#include <Console.h>

SoftI2CMaster i2c = SoftI2CMaster(2, 3);
byte matrix[8][8];

int ctoi(char a) {
    if ( (a >= '0') && (a <= '7') ) {
        return a-48;
    } else {
        return -1;
    }
}

void reDisplay() {
    i2c.beginTransmission(0x70);
    i2c.send(0x00);
    for (byte y=0; y<8; y++) {
        byte tmp = 0;
        for (byte x=0; x<8; x++) {
            if (matrix[y][x]) {
                if (x == 0) {
                    tmp |= 0x80;
                }
                else {
                    tmp |= 1 << (x-1);
                }
            }
        }
        i2c.send(tmp);
        i2c.send(0x00);
    }
    i2c.endTransmission();
}

void setBlinkRate(uint8_t b) {
    if (b > 3) {
      b = 3;
    }
    i2c.beginTransmission(0x70);
    i2c.send((byte)(0x81 | (b << 1)));
    i2c.endTransmission();
}

void setBrightness(uint8_t b) {
    if (b > 15) {
        b = 15;
    }
    i2c.beginTransmission(0x70);
    i2c.send((byte)(0xE0 | b));
    i2c.endTransmission();
}

void setup() {
    Bridge.begin();
    Console.begin();

    i2c.beginTransmission(0x70);
    i2c.send(0x21);
    i2c.endTransmission();
    setBlinkRate(0);
    setBrightness(3);
}

void loop() {
    String cmd = Console.readStringUntil(0);
    if (cmd.startsWith(F("on/"))) {
        int x = ctoi(cmd[3]);
        int y = ctoi(cmd[5]);
        if ((x > -1) && (y > -1)) {
           matrix[x][y] = 1;
        }
    }
    else if (cmd.startsWith(F("off/"))) {
        int x = ctoi(cmd[4]);
        int y = ctoi(cmd[6]);
        if ((x > -1) && (y > -1)) {
           matrix[x][y] = 0;
        }
    }
    else if (cmd.startsWith(F("get"))) {
        for (int y=0; y<8; y++) {
            for (int x=0; x<8; x++) {
                if (matrix[x][y]) {
                    Console.write('1');
                }
                else {
                    Console.write('0');
                }
            }
        }
    }
    reDisplay();
}
```

### Source Code – Python

```
#!/usr/bin/python
import json, os, socket, sys
res = { "result":0 }

def on(x, y):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("localhost", 6571))
    s.send("on/" + x + "/" + y + "\00")
    s.close()
    res["result"] = 1

def off(x, y):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("localhost", 6571))
    s.send("off/" + x + "/" + y + "\00")
    s.close()
    res["result"] = 1

def get():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("localhost", 6571))
    s.send("get\00")
    res["result"] = 1
    matrix = [[0 for x in range(8)] for y in range(8)]
    for y in range(0, 8):
        for x in range(0, 8):
            matrix[x][y] = s.recv(1)
    res["LEDs"] = matrix
    s.close()

try:
    if os.environ["REQUEST_METHOD"] == "POST":
        data = sys.stdin.read(int(os.environ["CONTENT_LENGTH"]))
        js = json.loads(data)
        if js["cmd"] == "on":
            on(js["x"], js["y"])
        elif js["cmd"] == "off":
            off(js["x"], js["y"])
        elif js["cmd"] == "get":
            get()
except:
    pass

print "Content-type: application/json"
print
print json.dumps(res)
```

* * *

## Installing and Using PHP

Since Python is a versatile, general-purpose programming language, it has many uses on the Arduino Yún. This book concentrates on Python so that you do not have to learn additional languages to build the projects.

However, it is more common for web developers to use PHP: hypertext processor (PHP) to add dynamic content to their websites. In the two projects in this chapter, you can see how Python scripts send HTML code to web browsers by printing them to the standard output stream. In PHP, you use the opposite approach: writing script code inside HTML documents.

For example:

```
<html>
<head><title>Hello from PHP</title></head>
<body>
    <p>
    <?php
        echo "Hello from PHP.";
    ?>
    </p>
</body>
</html>
```

Put your PHP code in between *<?php* and *?>* tags. You can use as many of these script blocks as you need.

Tip: If you are not familiar with programming in PHP and would like to learn more, there is a comprehensive (and free) tutorial available at [http://www.w3schools.com/php/](http://www.w3schools.com/php/)

### Installing PHP on the Arduino Yún

To add support for PHP to the Yún, you need to install a PHP interpreter – a program that can read, understand, and run your PHP scripts. The PHP interpreter and its related libraries are quite large, and so you should expand the OpenWrt-Yun file system to the microSD card before installing PHP. For more information, see [Expanding the Linux File System onto the microSD Card](#part0005_split_005.html_tc2s6).

To install PHP version 5 and the program that adapts PHP for use with CGI:

1.  Login to the OpenWrt-Yun command line.
2.  Type the following command and then press **Enter**:

    ```
    opkg update
    ```

3.  Type the following command and then press **Enter**:

    ```
    opkg install php5 php5-cgi
    ```

To enable PHP, add an interpreter to your website’s configuration in */etc/config/uhttpd*

1.  Type the following command and then press **Enter**:

    ```
    nano /etc/config/uhttpd
    ```

2.  Find the options for website that you want to enable PHP on, and add the following line:

    ```
    list interpreter          ".php=/usr/bin/php-cgi"
    ```

3.  Press **Ctrl + X**.
4.  Press **Y**, and then press **Enter**.
5.  Type the following command and then press **Enter**:

    ```
    /etc/init.d/uhttpd restart
    ```

To test that you successfully installed PHP and added the script interpreter, you can write a short script that uses the PHP function *phpinfo()* to display information about the system.

1.  Use the Linux command *cd* to move into your website’s content directory.
2.  Type the following command and then press **Enter**:

    ```
    nano phpinfo.php
    ```

3.  Add this code to the file:

    ```
    <?php
        phpinfo();
    ?>
    ```

4.  Press **Ctrl + X**.
5.  Press **Y**, and then press **Enter**.
6.  In a web browser on a machine that connects to the same network as your Arduino, open the *phpinfo.php* page.

The default installation of PHP does not always work with custom websites in uHTTPd. If you only see the message “No input file specified” on the webpage, you need to edit PHP’s *.ini* file.

1.  Type the following command and then press **Enter**:

    ```
    nano /etc/php.ini
    ```

2.  Change the line that reads *doc_root = “/www”* to:

    ```
    doc_root = ""
    ```

3.  Press **Ctrl + X**.
4.  Press **Y**, and then press **Enter**.
5.  Reload the webpage in your web browser.

### Accessing the Bridge from PHP

The version of Python in OpenWrt-Yun already has a module for working with the Yún’s Bridge library; the version of PHP on the Arduino Yún has a very similar extension. This extension is *bridgeclient.class.php*, and it is in */usr/lib/php/bridge*.

To make sure that you can use all of the features of the Bridge extension on your Yún, install (or update) a few extra files that the script works with.

1.  At the OpenWrt-Yun command prompt, type the following command and then press **Enter**:

    ```
    opkg update
    ```

2.  Type the following command and then press **Enter**:

    ```
    opkg install php5-mod-sockets php5-mod-json
    ```

To use the extension, add the following line to the top of your PHP script files:

```
<?php require("/usr/lib/php/bridge/bridgeclient.class.php") ?>
```

Then, like the Python version, you need to create an instance of the class:

```
$client = new bridgeclient();
```

The PHP version of the Bridge library contains the same methods as the Python version. These methods are summarized in the following table, and you can find examples of these methods in [Accessing Stored Data from Python Scripts](#part0007_split_002.html_tc4s2s5) and [Sending Messages from a Python Script](#part0007_split_006.html_tc4s6s3). You can also find example PHP code in the file */usr/lib/php/bridge/example.php*.

To call one of these methods in PHP, write *->* between the name of your instance and the method name. For example:

```
$client->put("PHP", "Yes");
```

| Method | Description |
| --- | --- |
| delete(key) | Deletes a key-value pair from the shared-storage memory that both the ATmega32u4 and Atheros AR331 can access. |
| get(key) | Gets the value of the specified item. |
| getall() | Returns a collection of all of the items in the shared-storage memory. |
| mailbox(string) | Sends a message to the ATmega32u4 using the Mailbox. |
| put(key, value) | Adds a value to the storage area and identifies it with the specified key. |

* * *

[1](#part0008_split_001.html_nf1)If you connect your Arduino to your network using both Wi-Fi and Ethernet, the Yún can have three IP addresses (including 127.0.0.1, which always refers to the current device). uHTTPd supports one website for each TCP port on the specified IP address. So you can have three websites on TCP port 80, if you use a different IP address for each one.[2](#part0008_split_001.html_nf2)'/' means that the entire website is protected. But you can also use the names of directories or files.[3](#part0008_split_001.html_nf3)If you have enabled basic authentication on this site then you already enabled an httpd.conf file.[4](#part0008_split_002.html_nf4)To use a cgi-bin directory, check that you have set the cgi_prefix to /cgi-bin in /etc/config/uhttpd.[5](#part0008_split_003.html_nf5)http://todbot.com/blog/[6](#part0008_split_003.html_nf6)This is usually C:\Program Files\Arduino\ or similar.[7](#part0008_split_003.html_nf7)When the webpage in this project displays this value, it has the option to convert the temperature to Fahrenheit.[8](#part0008_split_005.html_nf8)Or any other directory on the microSD card if you create this symbolic link yourself.[9](#part0008_split_005.html_nf9)Or http://arduino.local:<PORT> if your administration panel does not use TCP port 80.[10](#part0008_split_005.html_nf10)If you have not changed it, the password is arduino.[11](#part0008_split_005.html_nf11)http://todbot.com/blog/[12](#part0008_split_005.html_nf12)This is usually C:\Program Files\Arduino\ or similar.

# Project 3 – Making an MP3 Jukebox

In this project, you will build an MP3 player, or jukebox-style device. The project comprises an Arduino sketch, a Python script, and a prototype circuit that contains: an LCD screen on which to display track information; two buttons for browsing through the MP3 files on the microSD card; and a button to start playing a track.

To build this kind of project on other Arduinos, you usually need a shield (such as the Wave Shield or MP3 Player Shield). However, OpenWrt-Yun on the Arduino Yún can use small, cheap, USB audio devices to connect the Yún to speakers or headphones.

The Arduino sketch handles button presses and sending text to the LCD display. The Python script (and OpenWrt-Yun’s built-in support for audio devices) handles playing MP3 files through the audio interface.

In This Chapter

[Building the MP3 Player on a Breadboard](#part0009_split_000.html_tp3s1)

[Playing MP3 Files from Python Scripts](#part0009_split_001.html_tp3s2)

[Handling Button Presses and Starting the Music](#part0009_split_002.html_tp3s3)

[Stopping an MP3](#part0009_split_003.html_tp3s4)

[Source Code – Sketch](#part0009_split_004.html_tp3s5)

[Source Code – Python](#part0009_split_005.html_tp3s6)

* * *

## Building the MP3 Player on a Breadboard

To complete this project, you need:

1.  An Arduino Yún, connected to your local network over Ethernet or Wi-Fi.[1](#part0009_split_006.html_fn1)
2.  A microSD card, with the OpenWrt-Yun Linux file system expanded onto it. For more information, see .
3.  A USB audio interface (see below).
4.  Desktop PC speakers, with a 3.5 mm stereo jack plug and their own power supply. Or a set of headphones with a 3.5 mm stereo jack plug.
5.  A parallel 16x2 LCD display with HD44780 driver.
6.  A potentiometer, between 10 kΩ and 47 kΩ.
7.  (Optional) An LED and 220 Ω resistor.
8.  Three 10 kΩ resistors.
9.  Three momentary push buttons.[2](#part0009_split_006.html_fn2)
10.  A solderless breadboard and jumper wires.

### Buying a USB Audio Interface for the Arduino Yún

Modern Linux systems have good support for USB devices, particularly basic devices that follow a standard behavior. The simplest way to connect the Arduino Yún to speakers, is to use a USB audio interface and play the music files from OpenWrt-Yun.

USB audio interfaces range from a few dollars, to several hundred dollars. For this project, you want a very simple device with a 3.5 mm headphone or speaker output socket. You can usually use small USB audio interface, such as the one shown in Figure 12, with no drivers or additional software requirements.

Tip: Try to buy an audio interface with a microphone input. In [Project 7 – Controlling your Arduino Projects with Voice Commands](#part0013_split_000.html_tp7), you can use the same device to record audio from the microphone.![](images/00013.jpeg) 

Figure 12\. A basic USB audio interface

Connect your speakers to the headphone or speaker output socket, and then plug the USB device into the vertically-mounted USB socket on your Arduino Yún.

### Connecting the Circuit

The circuit for this project is based on three beginners’ Arduino tutorials: using the *LiquidCrystal* library with an LCD; “Blink”; and digital input using a push button or switch.

![](images/00014.jpeg) 

Figure 13\. Connecting the jukebox circuit to the Arduino

Figure 13 shows a full-size, solderless breadboard for clarity. However, you can fit all of the connections on a half-size breadboard.

The pins for the LCD are numbered 1–16 (or 1–14 on LCDs without a backlight), from left to right. Follow the diagram in Figure 13, or the table below, to connect the LCD.

| LCD Pin | Description | Connect To |
| --- | --- | --- |
| 1 | Ground. | Arduino GND pin. |
| 2 | 5 V power input. | Arduino 5V pin. |
| 3 | Contrast adjustment. | The potentiometer, as shown in Figure 13. |
| 4 | Register select. Controls which part of the LCD’s memory you write to or read from. | Arduino digital pin 7. |
| 5 | Read/write. This project only writes to the LCD. | Arduino GND pin. |
| 6 | Enables writing to the LCD. | Arduino digital pin 6. |
| 11 | Data 4. | Arduino digital pin 5. |
| 12 | Data 5. | Arduino digital pin 4. |
| 13 | Data 6. | Arduino digital pin 3. |
| 14 | Data 7. | Arduino digital pin 2. |

Leave all of the other pins unconnected.

This project uses an LED to indicate when a track is playing. If the LED is lit, the Linux side of the Yún is not currently playing music, and the user is able to press the “play” button to start a track. If the LED is not lit, the Yún is playing a track and the user cannot start another.

To connect the LED:

1.  Connect the anode (positive, long-leg) end of the LED to Arduino digital pin 13.
2.  Connect one end of a 220 Ω resistor to the cathode (the other leg of the LED).
3.  Connect the other end of the resistor to ground.

The three buttons in this circuit are: previous, play, and next. You can use the previous and next buttons to browse through the *.mp3* files on the microSD card. If the LED is lit, you can press the play button to start the track that is displayed on the LCD.

To connect the buttons:

1.  Connect the top-left pin of each button to the Arduino’s “5V” pin.
2.  Connect the top-right pin of each button to a 10 kΩ resistor (see Figure 2).
3.  Connect the other end of the resistor to ground.
4.  Connect the bottom-right pin of each button to the Arduino, as shown in the table below.

| Button | Connect To |
| --- | --- |
| 1 | Arduino digital pin 8. |
| 2 | Arduino digital pin 9. |
| 3 | Arduino digital pin 10. |

In the circuit shown in Figure 13, the Arduino digital pins connect to ground through the 10 kΩ resistors. The 5 V power inputs go nowhere. This causes the pin to read *LOW*.

When you press the button, it connects the 5 V power line to the Arduino digital pin and this causes the pin to read *HIGH* in the Arduino sketch. Both the 5 V and Arduino digital pin lines now connect to ground through the resistor. However, the value of the resistor is high so that enough voltage still moves into the digital pin for it to read as *HIGH*.

Tip: You can make a simpler circuit by using the Arduino’s internal pull-up and pull-down resistors and connecting a button or switch between the digital pin and ground. But if you set the digital pin as a *HIGH* output and press the switch then you have a short circuit, which may damage your Arduino.

* * *

## Playing MP3 Files from Python Scripts

This project uses the Linux command-line program *madplay* to play music.

Before you can install madplay and call it from your Python script, you need to install a library that it depends on.

1.  Login to the OpenWrt-Yun command line.
2.  Type the following command and then press **Enter**:

    ```
    opkg update
    ```

3.  Type the following command and then press **Enter**:

    ```
    opkg install kmod-usb-audio
    ```

To download and install madplay,

*   Type the following command and then press **Enter**:

    ```
    opkg install madplay
    ```

Test madplay by copying an MP3 file to your microSD card, or by uploading one to your Arduino over the network. Then, at the command line, change to the directory where the *.mp3* is and run the following command:

```
madplay music_file.mp3
```

If you want to stop the music, press Ctrl + C.

The Python script in this project performs two functions depending on the commands that the Arduino sketch sends to it:

1.  Send back the title, artist, and album information from the ID3 tag of the file name that the Arduino sketch specifies.
2.  Play an MP3 file that the Arduino sketch specifies.

To write the player script, you need the Python *id3reader* module. To install this, see [Downloading and Installing Python Packages](#part0006_split_008.html_tc3s8s1). The *id3reader* module is an example in that section of the chapter.

The player script looks at the command line arguments that the Arduino sketch uses to start it. There are two arguments: command, and then file.

command

Can be *-info* or *-play*.

file

The file name and file path of the MP3 file.

Create a directory on your microSD card for this project. For example, create the directory */mnt/sda1/P3*. Then create another directory inside that one, called "MP3", and transfer a few *.mp3* files into it.

Start a new Python script in the project directory (call it *player.py*) and type the following code at the beginning.

```
#!/usr/bin/python
import id3reader, os, sys

mp3opt = "-a -10"
```

The variable *mp3opt* contains extra command-line parameters that the script passes to madplay. The *-a* option adjusts the volume of playback. To see the other options that you can specify, run the following command from the OpenWrt-Yun command line:

```
madplay --help
```

You can fetch the command and file arguments from the command line using the array *sys.argv[]*. The first item in this array is always the name of the script. If there are any other arguments, they are in the array in the order that they are typed on the command line.

Add the following code to the file:

```
if len(sys.argv) > 2:
    if sys.argv[1] == "-info":
        try:
            id3 = id3reader.Reader(sys.argv[2])
            print id3.getValue("title")
            print id3.getValue("performer") + " - " + id3.getValue("album")
        except IOError:
            print
            print
    elif sys.argv[1] == "-play":
        os.system("madplay " + mp3opt + " \"" + sys.argv[2] + "\" &>/dev/null")
```

To test this script from the OpenWrt-Yun command line, type the following command and then press the Enter key:

```
./player.py -info "<music file.mp3>"
```

Then test that it plays the MP3 file correctly:

```
./player.py -play "<music file.mp3>"
```

By putting the file name in quotes, you can ensure that the shell passes the entire file name as a single argument to *player.py*. Without the quotes, spaces in the file name cause the shell to split the file name into several arguments.

* * *

## Handling Button Presses and Starting the Music

The Python script in the previous section takes its input from the command line. After each task, the script ends. The *Process* class in the Bridge library is a good choice for controlling Linux programs that only need input from the command line, and that end quickly.

The first thing that the Arduino sketch needs to do, is work out how many MP3 files are on the microSD card. This is so that the sketch does not try to access files that don’t exist if the user presses the next or previous buttons too many times.

Tip: You can handle of all the file routines from Python on the Linux side of the Yún. However, this project uses the *File* and *FileSystem* classes from the Bridge library to demonstrate how to access files on the SD card from an Arduino sketch.

Open the Arduino IDE and start a new sketch.

At the top of the file, add the following include directives:

```
#include <Bridge.h>
#include <FileIO.h>
#include <LiquidCrystal.h>
```

To use the *LiquidCrystal* library, you need to create an instance of it and specify the digital pins that you connect the LCD to. To do this, add the following line underneath the include directives:

```
LiquidCrystal lcd(7, 6, 5, 4, 3, 2);
```

Then define the Arduino pins that connect to your input buttons and output LED:

```
int prev = 8;
int play = 9;
int next = 10;
int LED = 13;
```

In your sketch’s *setup()* function, set the three buttons to *INPUT*, and the LED to *OUTPUT*. Then start the Bridge library and the *lcd* instance.

```
void setup() {
    pinMode(next, INPUT);
    pinMode(play, INPUT);
    pinMode(prev, INPUT);
    pinMode(LED, OUTPUT);

    Bridge.begin();
    lcd.begin(16, 2);
}
```

The arguments that you pass into *lcd.begin()* specify the size of your LCD. In this example, you use a 16x2 display and so the arguments are *16* and *2*.

### Counting MP3s

You can use Linux commands to count the number of files in the MP3 directory on the microSD card. However, you can also do this from an Arduino sketch by using the *File* and *FileSystem* classes from the Bridge library.

Create a new global variable near the top of your sketch:

```
int _max = 0;
```

Then declare a new function:

```
void countMP3s() {
}
```

To count the number of MP3 files in a directory, you need to:

1.  Open the directory using *FileSystem.open()*.
2.  Rewind the directory to ensure that your code finds all of the files.
3.  Use *openNextFile()* to open each file in the directory.
4.  Increment *_max* every time you open a file that’s name ends with “.mp3”.
5.  Stop when *openNextFile()* returns a *File* object that evaluates to *false*.

Add the following code to the *countMP3s()* function:

```
_max = 0;
File mp3s = FileSystem.open("/mnt/sda1/P3/MP3");
mp3s.rewindDirectory();
while (true) {
    File f = mp3s.openNextFile();
    if (f) {
        if (String(f.name()).endsWith(".mp3") ) {
            _max++;
        }
        f.close();
    }
    else {
        break;
    }
}
mp3s.close();
```

To test everything so far, add the following code underneath the line *lcd.begin(16, 2);* in your sketch’s *setup()* function:

```
countMP3s();
lcd.clear();
lcd.home();
lcd.print(_max);
```

Upload this sketch to your arduino. When the sketch starts, the LCD displays the number of *.mp3* files that are on the microSD card.

When you finish testing, remove these three lines from your sketch’s *setup()* function:

```
lcd.clear();
lcd.home();
lcd.print(_max);
```

### Displaying ID3 Tags on the LCD

When the sketch begins, it should display the information for the first MP3 file and be ready to play it.

To keep track of which MP3 is on the LCD, create two new global variables at the top of the sketch:

```
int _track = 1;
String _mp3 = "";
```

To fetch the ID3 tag information, you can use the Python script that you created in [Playing MP3 Files from Python Scripts](#part0009_split_001.html_tp3s2). This script expects the Arduino sketch to pass in the file name of an MP3.

It would take a lot of memory to store the file names of all of the MP3 files. Instead, you only want to store the file name of the MP3 that is currently shown on the LCD.

Create a new function in the sketch:

```
void getMP3Filename() {
    _mp3 = "";
    File mp3s = FileSystem.open("/mnt/sda1/P3/MP3");
    mp3s.rewindDirectory();
    for (int t=1; t<=_track; t++) {
        File f = mp3s.openNextFile();
        if (f) {
            if (t == _track) {
               _mp3 = f.name();
            }
            f.close();
        }
    }
    mp3s.close();
}
```

This function loops through the directory in the same way as *countMP3s()*. However, when it reaches the file that *_track* indicates, it fetches the file name from the *File* object.

You can now access ID3 tags by starting the *player.py* script and passing in the contents of the *_mp3* variable.

Add the following function to the sketch:

```
void showMP3Info() {
    Process p;
    p.runShellCommand("/mnt/sda1/P3/player.py -info \"" + _mp3 + "\"");
    String t1 = p.readStringUntil('\n');
    String t2 = p.readStringUntil('\n');
    p.close();

    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print(t1);
    lcd.setCursor(0, 1);
    lcd.print(t2);
}
```

When you ask the *player.py* script for the ID3 tag information, it returns two lines. *showMP3Info()* reads these two lines into strings. It then uses three methods of the *LiquidCrystal* class to show the information on the LCD.

| Method | Description |
| --- | --- |
| clear() | Clears the LCD. |
| print() | Displays a string on the LCD, starting at the current cursor position. |
| setCursor() | Moves the LCD cursor to the specified character position, on the specified row of the display. |

There are several other methods in the *LiquidCrystal* class that you can use in your projects:

| Method | Description |
| --- | --- |
| home() | Moves the LCD cursor to the top-left of the display. |
| write() | Writes a single character to the LCD. |
| cursor() | Turns on the graphic that shows the LCD cursor position on the display. |
| noCursor() | Turns off the graphic that shows the position of the LCD cursor. |
| blink() | If the LCD cursor is turned on, *blink()* makes it flash on and off repeatedly. |
| noBlink() | Stops the LCD cursor from flashing. |
| noDisplay() | Turns off the LCD, but does not clear its contents. |
| display() | Turns on the LCD, and re-displays the text that was previously visible. |
| scrollDisplayLeft() | Scrolls each line of the LCD one character to the left. |
| scrollDisplayRight() | Scrolls each line of the LCD one character to the right. |
| autoscroll() | Turns on auto-scrolling. Before the LCD displays a character, it scrolls the visible contents one character. |
| noAutoscroll() | Turns off auto-scrolling. |
| leftToRight() | Sets the direction of text. If auto-scrolling is enabled, text scrolls to the left. |
| rightToLeft() | Sets the direction of text. If auto-scrolling is enabled, text scrolls to the right. |
| createChar() | To create a custom graphic character, pass in a number from 0–7 and then eight bytes of data. Each byte represents a row of eight pixels in the character – each bit is a single pixel. To display the character, call *write()* and pass in 0–7. |

To continue, add the following code underneath the line that reads *countMP3s();*:

```
getMP3Filename();
showMP3Info();
digitalWrite(LED, HIGH);
```

Upload the sketch to your Arduino. The LCD shows the track name and artist information of the first MP3 file on the microSD card. And the LED is lit, to indicate that the Arduino is ready to play a file.

### Responding to Button Presses

The breadboard circuit in [Connecting the Circuit](#part0009_split_001.html_tp3s1s2) contains three buttons. Each of these buttons connects to an Arduino digital pin that is *HIGH* when someone presses the button, and *LOW* when the button is not in use.

When you press a button or close a switch, it actually makes and breaks contacts several times in a very short amount of time. For the Arduino sketch to work, you need to “debounce” the buttons. Debouncing means checking the state of the button twice, very quickly, to check that a good contact is made.

One way to debounce a button, is to wait for it to go *HIGH*. Then wait a few milliseconds and check the button again. For example:

```
if (digitalRead(next) == HIGH) {
    delay(50);
    if (digitalRead(next) == HIGH) {
        // button press
    }
}
```

In this project, when you detect that the *next* button is *HIGH*, you need to:

1.  Debounce the button.
2.  Increment the *_track* variable.
3.  If *_track* is now greater than the *_max* number of MP3 files on the SD card, set *_track* to *1* so that the display shows the first MP3 file in the directory.
4.  Update the file name in *_mp3*.
5.  Update the information on the LCD.

For the *prev* button:

1.  Debounce the button.
2.  Decrement the *_track* variable.
3.  If *_track* is now less than *1*, set *_track* to *_max* so that the display shows the last MP3 file in the directory.
4.  Update the file name in *_mp3*.
5.  Update the information on the LCD.

Add the following code to your sketch’s *loop()* function:

```
if (digitalRead(next) == HIGH) {
    delay(50);
    if (digitalRead(next) == HIGH) {
        _track++;
        if (_track > _max) {
            _track = 1;
        }
        getMP3Filename();
        showMP3Info();
        delay(500);
    }
}
else if (digitalRead(prev) == HIGH) {
    delay(50);
    if (digitalRead(prev) == HIGH) {
        _track--;
        if (_track < 1) {
            _track = _max;
        }
        getMP3Filename();
        showMP3Info();
        delay(500);
    }
}
```

Upload this sketch to your Arduino and check that you can now browse through the contents of the MP3 directory on the microSD card.

Because jukeboxes normally play a track through to the end, you only want to detect the *play* button if the Arduino is not already playing an MP3\. In the next section, [Stopping an MP3](#part0009_split_003.html_tp3s4), you can see how to change this behavior.

Add the following global variable to your sketch:

```
Process playing;
```

Then add the following code to your sketch’s *loop()* function, underneath the code for the *next* and *prev* buttons:

```
if (!playing.running()) {
    digitalWrite(LED, HIGH);
    if (digitalRead(play) == HIGH) {
        delay(50);
        if (digitalRead(play) == HIGH) {
            digitalWrite(LED, LOW);
            playing.runShellCommandAsynchronously("/mnt/sda1/P3/player.py " 
                                                  + "-play \"" + _mp3 + "\"");
            delay(500);
        }
    }
}
```

If the Arduino is not playing an MP3, the code keeps the LED on.

If this code detects that someone presses the *play* button, it turns off the LED and then starts the Python script on the AR9331\. It passes “-play” and the file name of the MP3 into the script, so that *player.py* tells madplay to play the file. *playing.running()* then returns *true*, and so this part of *loop()* does not run again until the MP3 ends.When the MP3 ends, *playing.running()* returns *false*, and so the code lights the LED and is able to detect the state of the *play* button.Using this structure in *loop()* lets you accept input from the *next* and *prev* buttons while the Arduino is playing a track.

* * *

## Stopping an MP3

To build an MP3 player that stops the current MP3 before starting another, you need to make a few small changes to the project. These modifications are not included in the following Source Code sections of this chapter.

Every time Linux runs a program or command, it assigns the program a process identifier (PID). With this number, you can stop the process from Python using the *kill()* method of the *os* module.

To change the *player.py* script so that it accepts “-stop” as a command:

1.  Import the *signal* module.
2.  Change the line that reads *if len(sys.argv) > 2:* to

    ```
    if len(sys.argv) > 1:
    ```

3.  Add the following *elif* statement to the *if* statement that checks which command the Arduino sketch sends:

    ```
    elif sys.argv[1] == "-stop":
        pid = os.popen("pgrep madplay").read()
        os.kill(int(pid), signal.SIGKILL)
    ```

The Linux command *pgrep* searches the list of running processes for the keyword that you specify. If it finds a process containing that keyword, *pgrep* returns the PID. In this example, the Python script runs the command using *os.popen()* so that it can read the output of the command into a variable. *os.popen()* performs the same function as *os.system()*. However, the way that you access the output information is different.

The *os.kill()* method accepts an integer PID and an argument that describes the type of quit message that you want to send. There are many different types of quit message on Linux systems. *SIGKILL* is one that cannot be ignored.

Tip: You can find a list of POSIX signal names, and descriptions, on Wikipedia at [http://en.wikipedia.org/wiki/Unix_signal#POSIX_signals](http://en.wikipedia.org/wiki/Unix_signal#POSIX_signals)

To complete the modifications to this project, you need to change the Arduino sketch so that it responds to the *play* button even if it already playing a track.

Replace the *loop()* function in your sketch with this one:

```
void loop() {
    if (digitalRead(next) == HIGH) {
        delay(50);
        if (digitalRead(next) == HIGH) {
            _track++;
            if (_track > _max) {
                _track = 1;
            }
            getMP3Filename();
            showMP3Info();
            delay(500);
        }
    }
    else if (digitalRead(prev) == HIGH) {
        delay(50);
        if (digitalRead(prev) == HIGH) {
            _track--;
            if (_track < 1) {
                _track = _max;
            }
            getMP3Filename();
            showMP3Info();
            delay(500);
        }
    }
    else if (digitalRead(play) == HIGH) {
        delay(50);
        if (digitalRead(play) == HIGH) {
            digitalWrite(LED, LOW);
            if (playing.running()) {
                Process p;
                p.runShellCommand("/mnt/sda1/P3/player.py -stop");
                p.close();
            }
            playing.runShellCommandAsynchronously("/mnt/sda1/P3/player.py "
                                                  + "-play \"" + _mp3 + "\"");
            delay(500);
        }
    }

    if (!playing.running()) {
        digitalWrite(LED, HIGH);
    }
}
```

When you press the *play* button, *loop()* checks whether the Arduino is playing a track. If it is, it calls *player.py -stop* to stop the MP3\. Then it starts the new track.

The additional *if* statement at the end of *loop()* keeps the LED turned on when the Arduino is not playing a file.

* * *

## Source Code – Sketch

```
#include <Bridge.h>
#include <FileIO.h>
#include <LiquidCrystal.h>

LiquidCrystal lcd(7, 6, 5, 4, 3, 2);

int prev = 8;
int play = 9;
int next = 10;
int LED = 13;

int _max = 0;
int _track = 1;
String _mp3 = “”;
Process playing;

void countMP3s() {
    _max = 0;
    File mp3s = FileSystem.open("/mnt/sda1/P3/MP3");
    mp3s.rewindDirectory();
    while (true) {
        File f = mp3s.openNextFile();
        if (f) {
            if (String(f.name()).endsWith(".mp3") ) {
                _max++;
            }
            f.close();
        }
        else {
            break;
        }
    }
    mp3s.close();
}

void getMP3Filename() {
    _mp3 = "";
    File mp3s = FileSystem.open("/mnt/sda1/P3/MP3");
    mp3s.rewindDirectory();
    for (int t=1; t<=_track; t++) {
        File f = mp3s.openNextFile();
        if (f) {
            if (t == _track) {
               _mp3 = f.name();
            }
            f.close();
        }
    }
    mp3s.close();
}

void showMP3Info() {
    Process p;
    p.runShellCommand("/mnt/sda1/P3/player.py -info \"" + _mp3 + "\"");
    String t1 = p.readStringUntil('\n');
    String t2 = p.readStringUntil('\n');
    p.close();

    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print(t1);
    lcd.setCursor(0, 1);
    lcd.print(t2);
}

void setup() {
    pinMode(next, INPUT);
    pinMode(play, INPUT);
    pinMode(prev, INPUT);
    pinMode(LED, OUTPUT);

    Bridge.begin();
    lcd.begin(16, 2);
    countMP3s();
    getMP3Filename();
    showMP3Info();
    digitalWrite(LED, HIGH);
}

void loop() {
    if (digitalRead(next) == HIGH) {
        delay(50);
        if (digitalRead(next) == HIGH) {
            _track++;
            if (_track > _max) {
                _track = 1;
            }
            getMP3Filename();
            showMP3Info();
            delay(500);
        }
    }
    else if (digitalRead(prev) == HIGH) {
        delay(50);
        if (digitalRead(prev) == HIGH) {
            _track--;
            if (_track < 1) {
                _track = _max;
            }
            getMP3Filename();
            showMP3Info();
            delay(500);
        }
    }
    else if (digitalRead(play) == HIGH) {
        delay(50);
        if (digitalRead(play) == HIGH) {
            digitalWrite(LED, LOW);
            if (playing.running()) {
                Process p;
                p.runShellCommand("/mnt/sda1/P3/player.py -stop");
                p.close();
            }
            playing.runShellCommandAsynchronously("/mnt/sda1/P3/player.py "
                                                  + "-play \"" + _mp3 + "\"");
            delay(500);
        }
    }
    if (!playing.running()) {
        digitalWrite(LED, HIGH);
    }
}
```

* * *

## Source Code – Python

```
#!/usr/bin/python
import id3reader, os, signal, sys

mp3opt = "-a -10"

if len(sys.argv) > 1:
    if sys.argv[1] == "-info":
        try:
            id3 = id3reader.Reader(sys.argv[2])
            print id3.getValue("title")
            print id3.getValue("performer") + " - " + id3.getValue("album")
        except IOError:
            print
            print
    elif sys.argv[1] == "-play":
        os.system("madplay " + mp3opt + " \"" + sys.argv[2] + "\" &>/dev/null")
    elif sys.argv[1] == "-stop":
        pid = os.popen("pgrep madplay").read()
        os.kill(int(pid), signal.SIGKILL)
```

* * *

[1](#part0009_split_001.html_nf1)When you finish the project, you can disconnect the Arduino from your network.[2](#part0009_split_001.html_nf2)Or “tactile switches”.

# Project 4 – Hosting a USB Game Controller

OpenWrt-Yun Linux has built-in drivers for most types of USB device, and you can use many devices from shell scripts and Python programs without writing support for them yourself.

However, OpenWrt-Yun does not automatically support every USB device – there are some that do not work correctly on Linux, and some that OpenWrt-Yun does not know about at all. In these situations, you have three options:

1.  Check if there is a piece of software for another version of Linux that you can make work on OpenWrt-Yun;
2.  Write a Linux device driver; or
3.  Write code into a single project to use the USB device.

A device driver is a program that the operating system loads when it detects a device. These drivers provide a way for other programs on the system to use the hardware, without communicating with it at a low level. Usually only experienced programmers write device drivers because it requires a lot of technical knowledge. For more information about writing drivers, you may wish to read Linux Device Drivers from O’Reilly Media Inc.[1](#part0010_split_005.html_fn1)

Writing code into your project to use the device is often the simplest approach. However, only your project can use the USB device – no other programs on the Yún are able to access the device.

In this project, you can see how to take full control of USB devices using your own Python scripts. This chapter provides an introduction to how USB devices work; a short tutorial on how to figure out what you need to do to receive input from USB devices; and example code that reads input from a USB game controller and sends it to an Arduino sketch to control a servo motor and some LEDs.

In This Chapter

[Introducing the Universal Serial Bus](#part0010_split_000.html_tp4s1)

[Spying On USB Devices](#part0010_split_001.html_tp4s2)

[Installing and Using PyUSB](#part0010_split_002.html_tp4s3)

[Building a Test Circuit](#part0010_split_003.html_tp4s4)

[Source Code – Sketch](#part0010_split_004.html_tp4s5)

* * *

## Introducing the Universal Serial Bus

To complete this project, you need:

1.  An Arduino Yún, connected to your local network over Ethernet or Wi-Fi.[2](#part0010_split_005.html_fn2)
2.  A 5 V power supply that supplies at least 1 A of current (2 A recommended).
3.  A microSD card, with the OpenWrt-Yun file system expanded onto it. For more information, see [Expanding the Linux File System onto the microSD Card](#part0005_split_005.html_tc2s6).
4.  Four light-emitting diodes (LEDs).
5.  Four 220 Ω resistors.
6.  One 3-pin, standard RC servo motor.
7.  A solderless breadboard and jumper wires.
8.  A USB game controller.

To connect this many high-current devices to the Arduino Yún, you need more power than most PC USB sockets supply. The project may not work correctly unless you use a good quality power supply.

This chapter contains instructions and information to help you host and use one of the following game controllers:

*   Microsoft Xbox 360® wired controller;
*   PC USB game controller (for example, a Thrustmaster® Firestorm Dual Power / Dual Analog 3);
*   Sony PlayStation® DualShock® 4 (PS4™ controller through a micro-USB cable); or
*   Sony PlayStation® DualShock® 3 (PS3™ controller through a mini-USB cable).

If you do not have one of these controllers, you may be able to make other USB controllers work using the information in the next section, [Spying On USB Devices](#part0010_split_001.html_tp4s2). If you buy a controller for use with this project, it is advisable to get an Xbox 360® or PlayStation® controller because PC game controllers can sometimes be quite different from each other.

Tip: This project does not cover using Bluetooth controllers (such as PS3™ or PS4™ controllers without the USB cable), or radio frequency (RF) controllers that use an additional receiver dongle. RF receivers often need more current than the maximum 500 mA that the Arduino Yún supplies to the USB socket.

### Understanding the USB Protocol

This overview of USB devices and protocols is intended help you work with USB human interface devices (HID), such as game controllers. It is beyond the scope of this book to fully cover all of the details and variations of the USB specification. For a more detailed view of designing and programming USB peripherals, you may wish to read USB Complete by Jan Axelson.[3](#part0010_split_005.html_fn3)

USB is a serial protocol – it sends information one bit at a time (using *HIGH* and *LOW* electrical signals to represent 1 and 0). The USB specification defines how you should structure and transmit information.

Unlike many other types of serial connection, a USB message contains many layers of information. Each layer has a slightly different purpose. For example, when sending a message to a peripheral, the message includes additional information that tells the USB hub which device the message is for. Each layer is more device-specific and function-specific than the last. Until, in the final layer, there is the actual data.

Tip: These layers of messages are similar to how network protocols work. Or imagine putting a message in an envelope, and then putting that envelope inside another envelope, and so on. Each recipient processes and removes one envelope and then sends the message on to the next recipient.

When writing Python scripts to control USB peripherals on the Arduino Yún, you do not need to construct all of the data for these layers yourself. However, it is useful to know that these layers exist when you try to find out how a specific USB peripheral works.

There are two main types of USB communication: enumeration and application. During enumeration, the host operating system talks to its USB bus and hub devices to discover any USB peripherals that are in your computer. If it finds a device, it sends special messages to learn what kind of device it is and what features it has.

Application communications cover a wide range of different messages. These are often specific to the particular device that you write software to control. However, USB peripherals of the HID class are relatively simple devices, and they are often very similar to each other.

All application communications travel to and from *endpoints*. It may be helpful to think of an endpoint as the USB equivalent of a TCP or UDP port – different endpoints are programmed to respond to different types of message. Every USB device has at least one endpoint – this is the control endpoint and it is always bi-directional. Other endpoints can be inputs (“IN” – for sending information from the device to the computer) or outputs (“OUT” – for sending information to the device, from the computer).

The USB game controllers in this project all have: a control (or “setup”) endpoint; at least one IN endpoint that sends the state of the buttons and analog sticks; and an OUT endpoint that the computer can use to activate LEDs and rumble effects.

The USB 2.0 specification defines four different ways that computers and USB peripherals can send messages:

Control

The first endpoint (endpoint 0) in a USB device is always a control. This is used for configuration messages, but it can also be a general-purpose way of sending information from one device to another.

Bulk

Bulk transfers are for sending large amounts of data. Devices use this method when it is acceptable for the delivery of the message to be delayed a short time. However, a bulk transfer is usually quicker than sending a large number of small messages.

Interrupt

Interrupt transfers are useful for sending a small amount of data that must be received and processed quickly. For example, computers need to receive messages from a keyboard quickly, or the user may see the delay between pressing a key and the character appearing on their screen. However, this is not like the interrupts used by microprocessors and microcontrollers – the USB controller still asks the peripheral if it has any data to send; peripherals do not spontaneously send data.

Isochronous

Isochronous transfers are a continual stream of data. This is very fast. However, using this mode disables error checking and automatic retransmission of data if there is a problem.

The manufacturer of the USB device chooses how their device communicates when they build the product. HID peripherals, like game controllers, usually send their information to the host computer using control or interrupt transfers.

Tip: The USB specification also includes *interfaces* and *configurations* that the device can use to support multiple ways of communicating. However, you do not need to understand these in order to work with most HID peripherals.

* * *

## Spying On USB Devices

Most device manufacturers do not publish all of the technical information about their products. If you want to write a script to control a USB device that OpenWrt-Yun does not understand, you may have to try and discover how the device works yourself.There are two main ways of doing this:

*   Look at source code for driver software that is available on other computers; or
*   Install the device on a system that you can obtain driver software for. Then look at the messages that the computer sends to the device and the messages that the device sends to the computer.

The second option is often called “spying”, “snooping”, or “sniffing”. It is often simplest to do this on a Windows PC because the tools that you need are free, and there are Windows drivers available for almost all of the USB devices that you can buy.

Sniffing USB devices and writing a Python script to replicate them can take time. It is often trial and error. The more complicated the device, the longer it usually takes to discover how it works.

You do not need to work through this section to complete the game controller project. If you want to skip this, you can turn to [Installing and Using PyUSB](#part0010_split_002.html_tp4s3). The remainder of this section provides a brief introduction to sniffing USB devices and discovering how they work.

### Sniffing on Microsoft Windows

To use a USB peripheral in a Python script on the Arduino, you need to know its vendor and product identifiers. These are 32-bit numbers, and the combination of the two is unique to a specific device. However, manufacturers sometimes use the vendor and product identifiers from products that their peripheral is compatible with. For example, most game controllers that work on the Sony PlayStation® 4 games console use the identifiers that are assigned to Sony’s official DualShock® 4 controller.

To find the vendor and product identifiers for a USB device on Windows 8/7/Vista/XP:

1.  Plug the USB peripheral into a USB slot on your computer.
2.  Press the **Windows Logo key + R**.
3.  Type *devmgmt.msc* and press **Enter**.

You can usually find HID peripherals under *Human Interface Devices*, *Mice and other pointing devices*, *Sound video and game controllers*, or *Other devices*.

When you find your device:

1.  Right-click the device and then click **Properties**.
2.  In the **Details** tab, under **Property**, click **Hardware IDs**.
3.  Make a note of the information under **Value**.

For example, the Windows Device Manager shows the Microsoft Xbox 360® controller with the hardware identifiers:

```
HID\VID_045E&PID_028E&IG_00
```

The two numbers are in hexadecimal notation. The four characters after *VID_* are the vendor identifier. The four characters after *PID_* are the product identifier.

To intercept the messages that travel between your computer and the USB device, you need additional pieces of software. There are many different USB sniffing programs available for Windows computers. Many of these are commercial products, but USBPcap ([http://desowin.org/usbpcap/](http://desowin.org/usbpcap/)) and Wireshark ([http://www.wireshark.org](http://www.wireshark.org)) are free.

USBPcap is a command line tool for logging USB messages. It does not have a graphical user interface to make it easy for you to look at messages. However, you can send the results of USBPcap to Wireshark.

Install both USBPcap and Wireshark, and then:

1.  Plug the USB peripheral into a USB slot on your computer.
2.  On Windows 8, press the **Windows Logo key**, type *cmd*, and then right-click **Command Prompt**. Click **Run as administrator** and then click **Yes**.
3.  On Windows 7, press the **Windows Logo key + R**, type *cmd*, and then press **Ctrl + Shift + Enter**.
4.  On Windows Vista/XP, press the **Windows Logo key + R**, type *cmd*, and then press **Enter**.
5.  Type the following command and then press **Enter**:

    ```
    "c:\program files\usbpcap\usbpcapcmd.exe"
    ```

6.  In the list of devices, find your peripheral and make a note of the USBPcap device identifier. For example: *\\.\USBPcap6*.
7.  Type *q* and then press **Enter**.
8.  Type the following command on one line, and then press **Enter**:[4](#part0010_split_005.html_fn4)

    ```
    "c:\program files\usbpcap\usbpcapcmd.exe" -d \\.\USBPcap6 -o - | "c:\program files\wireshark\wireshark.exe" -k -i -
    ```

Tip: If you do not have appropriate driver software for the USB peripheral then you may not be able to see all of the messages that you need.

Wireshark displays incoming and outgoing messages for the USB peripheral in the top panel. The remainder of this section is an example of working with a Microsoft Xbox 360® controller, and you need to press a button on that device before you see any messages.

![](images/00015.jpeg) 

Figure 14\. Viewing USB messages in WIRESHARK on Windows 8

The *source* and *destination* columns show which device sent the message and which device received it. If the value in the *destination* column is *host* then the controller sent the message to your PC.

To view more information about a message, click it. The Wireshark application displays the contents of the message in the middle panel.

Click the box next to *USB URB* to expand that section. USB request blocks (URBs) contain information about the USB message. Of particular interest are the lines:

```
Endpoint: 0x81, Direction: IN
URB transfer type: URB_INTERRUPT (0x01)
Packet Data Length: 20
```

This information tells you that the Xbox 360® controller sends an interrupt message from endpoint 0x81 whenever you press a button, and that the message is 20 bytes long.

Click *Leftover Capture Data* in the middle panel to highlight part of the USB message in the bottom panel. The highlighted part of the message in Figure 14 is the actual data that the controller sends; all of the bytes before this help the USB protocol deliver and understand the message.

The controller data is 20-bytes long (just as the *Packet Data Length* entry says it is) and looks like this:

```
00 14 00 00 00 00 ce 11 a2 f7 79 f8 bd 01 00 00 00 00 00 00
```

This is the button input report. By viewing different messages, you can see that the second byte in this part of the message is usually *14*. *14* is the hexadecimal version of *20*. So you can guess, with reasonable certainty, that the second byte in this 20-byte button report is the length of the message.

Press and release the A button on the controller a few times.

Looking through the different messages, you can see that when you press the A button, the controller sends a message with the fourth byte in the input report as *10*. When you press the X button, this byte is *40*. If you release a button then this byte is *00*. If you press A and X together, the value is *50*. The binary representations of these hexadecimal numbers are:

| Hexadecimal | Binary |
| --- | --- |
| 00 | 00000000 |
| 10 | 00010000 |
| 40 | 01000000 |
| 50 | 01010000 |

From looking at the binary representations, you can see that the Xbox 360® controller uses one bit to represent the state of each of the main buttons. Bit 6 represents the X button, and bit 4 represents the A button. If you press the Xbox Guide, LB, or RB buttons then they change the same byte in the report. Other buttons change bits in other bytes.

Using this method of pressing buttons and comparing the messages, you can start to interpret the controller’s report. In [Working with Microsoft Xbox 360® Controllers](#part0010_split_003.html_tp4s3s1), you can see more information about the message format of the Xbox 360® controller.

When you plug a Microsoft Xbox 360® controller into a Windows PC, the USB drivers send various messages to the controller. Sometimes you need to know what these messages are and to replicate them in your Python scripts. For example, the USB driver tells the Xbox controller to light an LED to show the controller or player number. If you want to control the LEDs from your Python script, you need to know how to send this message.

But because the device is already running when you start USBPcap and Wireshark, you cannot see those messages. To see all of the messages that the host sends to the device, you need to have USBPcap and Wireshark running before you connect the controller to your system:

1.  On the **File** menu, click **Quit**.
2.  Click **Stop and Quit without Saving**.
3.  In the command prompt that is running USBPcap, press **Ctrl + C**.
4.  Unplug the USB peripheral from your system.
5.  Type the following command on one line, and then press **Enter**:[5](#part0010_split_005.html_fn5)

    ```
    "c:\program files\usbpcap\usbpcapcmd.exe" -d \\.\USBPcap6 -o - | "c:\program files\wireshark\wireshark.exe" -k -i -
    ```

6.  Plug the USB peripheral into the same USB slot.

When you connect the device to the system in the same USB socket, it will usually use the same USBPcap device identifier.

![](images/00016.jpeg) 

Figure 15\. Capturing the USB setup messages

Many of these are standard USB messages that you do need to understand. For some devices, the *SET CONFIGURATION* and *SET INTERFACE* messages are important and you may have to replicate them in your Python scripts. By trial and error, you can discover if the device works without them. In this case, the Xbox controller does not actually need to receive those messages.

In the example above, the *USB_INTERRUPT out* messages are interesting. In the USB URB view, you can see that these are labelled “vendor specific”, which means that they do something specific to that controller and are not one of the usual HID peripheral messages. If you have software on your PC that lets you send different LED messages to the controller, you would find a *USB_INTERRUPT out*message every time you change the LED pattern. The first byte is always *01*, and the second byte is always *03*. But the third byte changes depending on the LEDs that you want to set.

This is how the set LED commands in [Setting the LEDs](#part0010_split_003.html_tp4s3s1s1) were discovered.

The same process applies to working out how to activate the rumble feature. You need to trigger the rumble from software and then find the messages sent from your computer to the controller. When you have a message (and its endpoint information) that you think might control the rumble, you can try it from your own script on the Arduino.

* * *

## Installing and Using PyUSB

On Linux, you can use the *libusb* library to read from and write to USB devices. However, this library is for C programmers. Python users have the module PyUSB. PyUSB is a wrapper for *libusb*, and it contains functions to access USB devices at a low level – so that you can communicate with a device even if OpenWrt-Yun does not know how.

You need to download and build PyUSB from its source code. To do this, you need the GNU GCC package and some supporting tools from the Arduino Yún repository. These packages are quite large, and so you should make sure that you expand Linux file system onto the microSD card. For more information, see [Expanding the Linux File System onto the microSD Card](#part0005_split_005.html_tc2s6).

1.  Login to the OpenWrt-Yun command line.
2.  Type the following command and then press **Enter**:

    ```
    opkg update
    ```

3.  Type the following command and then press **Enter**:

    ```
    opkg install unzip
    ```

4.  Type the following command and then press **Enter**:

    ```
    opkg install binutils
    ```

5.  Type the following command and then press **Enter**:

    ```
    opkg -t /root install yun-gcc
    ```

To install PyUSB:

1.  Change your working directory to the microSD card.
2.  Type the following command on one line and then press **Enter**:

    ```
    wget --no-check-certificate http://github.com/walac/pyusb/archive/master.zip
    ```

3.  Type the following command and then press **Enter**:

    ```
    unzip master.zip
    ```

4.  Type the following command and then press **Enter**:

    ```
    cd pyusb-master
    ```

5.  Type the following command and then press **Enter**:

    ```
    python setup.py install
    ```

You can now delete the *pyusb-master* directory, and the *master.zip* archive.

In this project, the Arduino sketch starts a Python script that reads input from the USB controller and then sends it to the ATmega32u4\. Any of the methods of exchanging information between the Atheros AR9331 and the ATmega32u4 work, but this example script writes to the standard output device. Because the Arduino sketch starts the Python script, it can read the output data through the *Process* class in the Bridge library.

Make a new directory on the microSD card for your project files. For example, at the command prompt, type the following command and then press the Enter key:

```
mkdir /mnt/sda1/P4 && cd /mnt/sda1/P4
```

Start a new script, *controller.py*, and then save it.

At the top of the script, add the following code:

```
#!/usr/bin/python
import signal
import sys
import usb.backend.libusb1
import usb.core
import usb.util
```

To use PyUSB on the Arduino Yún, you need to specify the location of version 1.0 of the *libusb* library and create an instance of the correct backend. To do this, add the lines:

```
backend = usb.backend.libusb1.get_backend(
          find_library=lambda x: "/usr/lib/libusb-1.0.so"
          )
```

Before you can make a connection to a controller, you need to find it. You can do this by calling the *find()* method in *usb.core* and passing in the vendor identifier and product identifier of the controller that you have. The table below shows the ID numbers (in hexadecimal format) for the controllers that this project supports.

| Controller | Vendor ID | Product ID |
| --- | --- | --- |
| Microsoft Xbox 360® controller | 0x045E | 0x028E |
| Sony PlayStation® DualShock® 4 | 0x054C | 0x05C4 |
| Sony PlayStation® DualShock® 3 or SIXAXIS™ | 0x054C | 0x0268 |
| Thrustmaster® Firestorm Dual Power / Dual Analog | 0x044F | 0xB304 |

Tip: To check the hardware identifiers of any USB devices that you plug into the Yún, type *lsusb* at the OpenWrt-Yun command line and then press the Enter key.

Add the following line to your Python script to create an object that connects to your controller. Replace the hexadecimal values in this line with the ones that refer to the controller you use.

```
dev = usb.core.find(idVendor=0x054C, idProduct=0x05C4)
```

If *find()* cannot locate the type of controller that you specify, it returns *None*. You can check whether a suitable device is available by adding the following lines:

```
if dev is None:
    sys.stdout.write(chr(0))
    sys.stdout.flush()
    sys.exit(0)
else:
    sys.stdout.write(chr(1))
    sys.stdout.flush()
```

If PyUSB does not find the controller, the script sends *0* (null) to the standard output device, and then the call to *sys.exit()* terminates the script. If the script finds the controller, it sends *1*.

Tip: This code uses *sys.stdout.write()* instead of *print()* because *write()* method does not send a line break. To ensure that it only sends one byte (one character), the code also uses the *chr()* method.

The call to *sys.stdout.flush()* ensures that the Python interpreter sends the information to the Arduino as soon as possible.

When you connect a USB device to the Arduino Yún, OpenWrt-Yun tries to load an appropriate driver for it. If it succeeds, you are not able to control the device from PyUSB.

The PyUSB module contains methods that you can use to find out if Linux is using the device and, if necessary, tell Linux to release its control and allow PyUSB to use the USB device.

Add the following lines to the end of the script:

```
if dev.is_kernel_driver_active(0):
    dev.detach_kernel_driver(0)
usb.util.claim_interface(dev, 0)
while (1):
    pass
```

Before you can run this script, you should make sure that it exits cleanly and releases the USB device back to Linux.

Near the top of the script, underneath the *import* directives, add the following code:

```
def clean_getaway(sig, frame):
    usb.util.release_interface(dev, 0)
    sys.exit(0)
signal.signal(signal.SIGINT, clean_getaway)
```

This code states that the Python interpreter should run the function *clean_getaway()* when the script receives the *SIGINT* signal. When you press Ctrl + C at the command line to cancel the Python script, Linux sends *SIGINT* to it. Ordinarily, the Python interpreter closes the script immediately, but now it calls *clean_getaway()* instead.

The next part of the script is different, depending on which game controller you use.

*   To use an Xbox 360® controller, see [Working with Microsoft Xbox 360® Controllers](#part0010_split_003.html_tp4s3s1).
*   To use a PlayStation® controller, see [Working with Sony PlayStation® DualShock® 4 Controllers](#part0010_split_003.html_tp4s3s2) or [Working with Sony PlayStation® DualShock® 3 and SIXAXIS™ Controllers](#part0010_split_003.html_tp4s3s3).
*   To use a Thrustmaster® Firestorm Dual Power controller, see [Working with PC USB Controllers](#part0010_split_003.html_tp4s3s4).

### Working with Microsoft Xbox 360® Controllers

Wired Microsoft Xbox 360® controllers make very good controllers for use with the Arduino Yún. They often come with very long USB cables and have a variety of buttons, triggers and analog sticks.

When first powered, the controller enters its default configuration. In this mode, the controller sends the state of every button on the device whenever you press one of the buttons or move a stick. And you can set the pattern of LEDs, or activate the rumble motors, by sending control messages.

To read from the controller, you can use the *read()* method of the PyUSB device instance. This method accepts two arguments – the endpoint address, and the maximum number of bytes to read. The IN endpoint from which the controller sends button press information is at address 0x81\. And the maximum length of a valid input report is 20 bytes.Replace the line in the *while* loop that reads “pass” with the following code, and then indent it:

```
try:
    inp = dev.read(0x81, 20)
    print inp
except usb.core.USBError:
    pass
```

There are several small errors that can occur during USB transmission. The *try* and *except* statements ensure that if one of these occurs, the script will continue to try and read from the controller instead of ending with an error message.

Connect the controller to the vertically-mounted USB socket on your Yún (if it is not connected), and then run this script from the command line. Press a few buttons on the controller. The script sends an array of bytes to the Linux console, and each byte represents a button or analog stick position on the controller.

When you finish testing, press Ctrl + C to end the script.

The button press report from the Microsoft Xbox 360® controller consists of 20 bytes. The controller may sometimes send shorter messages than this, however, those reports are not button presses and you can ignore them. The first byte of a button press report is always 0\. The second byte contains the value 20 – the length of the report.

The table that follows show a description of the most-commonly used bytes. This information starts with the third byte, which is at position 2 of the *inp* array.

The main values are:

| Byte No. | Description |
| --- | --- |
| 2 | Represents the state of the d-pad buttons, BACK, START, LS, and RS. Each bit represents a different button. If a bit is set, the button is pressed. If a bit is clear, the button is not pressed. From most-significant to least-significant: Bit 7 – RS Bit 6 – LS Bit 5 – back Bit 4 – start Bit 3 – right Bit 2 – left Bit 1 – down Bit 0 – up |
| 3 | Represents the state of the A, X, Y, B, LB, RB, and Xbox Guide buttons. Each bit represents a different button. If a bit is set, the button is pressed. If a bit is clear, the button is not pressed. From most-significant to least-significant: Bit 7 – Y Bit 6 – X Bit 5 – B Bit 4 – A Bit 3 – Bit 2 – Xbox Guide Bit 1 – RB Bit 0 – LB |
| 4 | The state of LT. This is a value in the range 0–255 and represents how far the player pulls the left trigger. |
| 5 | The state of RT. This is a value in the range 0–255 and represents how far the player pulls the right trigger. |
| 7 | The x-axis position of the left analog stick. This is a signed byte in the range -128–127 (left to right) with the midpoint at 0. |
| 9 | The y-axis position of the left analog stick. This is a signed byte in the range -128–127 (down to up) with the midpoint at 0. |
| 11 | The x-axis position of the right analog stick. This is a signed byte in the range -128–127 (left to right) with the midpoint at 0. |
| 13 | The y-axis position of the right analog stick. This is a signed byte in the range -128–127 (down to up) with the midpoint at 0. |

Note: The *controller.py* script does not display the negative numbers correctly yet. You can fix this later.

#### Setting the LEDs

Four light-emitting diodes (LEDs) surround the Xbox Guide button. The LEDs usually indicate the number of the controller when your Xbox 360® has more than one controller. There are also several predefined animations.

To set the state of the LEDs, you can send a short message to the controller’s OUT endpoint at address 0x01\. The data that you need to send is an array of three bytes. For example:

```
[0x01, 0x03, 0x0A]
```

The first byte in this sequence is the message type; this is always *1* when setting the LEDs. The next byte is the length of the message; this is *3* because there is a total of three bytes in the data. The third byte specifies the LED pattern, and this can be one of the following values:

| Value | Description |
| --- | --- |
| 0x00 | Turns all of the LEDs off. |
| 0x01 | Turns all of the LEDs on and off repeatedly. |
| 0x02 | LED number 1 flashes twice and then remains on. |
| 0x03 | LED number 2 flashes twice and then remains on. |
| 0x04 | LED number 3 flashes twice and then remains on. |
| 0x05 | LED number 4 flashes twice and then remains on. |
| 0x06 | Turns on LED number 1. |
| 0x07 | Turns on LED number 2. |
| 0x08 | Turns on LED number 3. |
| 0x09 | Turns on LED number 4. |
| 0x0A | Animates the LEDs in a rotating pattern. |
| 0x0B | Blinks any LEDs that are currently on, and then reverts to the previous setting. |
| 0x0C | Slowly blinks any LEDs that are currently on, and then reverts to the previous setting. |
| 0x0D | Alternates between two pairs of LEDs for a short time and then reverts to the previous setting. |

To send a message to the controller that tells it to start the rotating pattern, add the following line above the *while* loop:

```
dev.write(0x01, [0x01, 0x03, 0x0A])
```

The *write()* method accepts two arguments – the endpoint address (in this case, *0x01* for the output endpoint) and an array of bytes that are the message to the controller.

#### Turning On Rumble

The Microsoft Xbox 360® controller contains two small motors that you can use to “rumble” or vibrate the device. The first motor creates a low-frequency, deep (or big) rumble, and the second motor creates a higher-frequency rumble. To control the speed or strength of each motor, you can send a value in the range 0–255 to the controller. To the send a rumble message, you need an array of eight bytes. For example:

```
[0x00, 0x08, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00]
```

The second byte is the length of the message, and this is always *0x08* for rumble messages. The fourth byte controls the deep rumble and the fifth controls the shallow rumble. To turn both motors on to the maximum strength, you can use the following code and send the rumble message to the controller’s OUT endpoint at address 0x01.

```
dev.write(0x01, [0x00, 0x08, 0x00, 0xFF, 0xFF, 0x00, 0x00, 0x00])
```

After you start the rumble feature, you have to turn it off yourself. If you are testing the rumble in *controller.py*, you can add this line to the top of the *clean_getaway()* function.

```
dev.write(0x01, [0x00, 0x08, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00])
```

This ensures that the rumble ends when the script does.

#### Finishing the Python Script

To complete the *controller.py* script, send the x position of the left analog stick and a single byte that represents the state of four buttons to the Arduino sketch. The ATmega32u4 can struggle to read a full-length report quickly enough, so it is more efficient to send only the data that the sketch needs.

The sketch in [Building a Test Circuit](#part0010_split_003.html_tp4s4) reads input from the OpenWrt-Yun shell’s standard output device. If you use the Python *print()* function to send these numbers then it may convert them to text. Instead, you can use the *sys.stdout.write()* method.

The eighth byte of the input report (position 7 in the array *inp*) is a signed byte that specifies the x position of the left analog stick. However, Python is not great at handling signed 8-bit numbers, and it loses the sign when it reads the position from the USB device. Since the lowest eight bits of the number are not changed, you can restore the sign.

Add the following *import* declaration to the script:

```
import ctypes
```

And then replace the line that reads *print inp*, with the following code:

```
if len(inp) == 20:
    sys.stdout.write(chr(ctypes.c_byte(inp[7]).value + 128))
    sys.stdout.write(chr(inp[3] >> 4))
    sys.stdout.flush()
```

The *ctypes* module contains functions and data types that closely correspond to the data types used in C. *c_byte* is an 8-bit signed byte. The code above first converts *inp[7]* to a *c_byte*, which preserves negative values. It then gets a Python integer from this, using the *value* property. The result is a signed Python integer in the range -128–127\. However, the Arduino sketch expects the analog stick position to be in the range 0–255\. By adding 128 to the value, you convert -128–127 numbers to 0–255 numbers.

The fourth byte (position 3 in the *inp* array) of the input report represents the state of the A, X, Y, B, and several other buttons. To keep the Arduino sketch the same (regardless of which controller you use with this project), the sketch only looks for four buttons. And it expects that the buttons are the least-significant four bits of the number. To send only the state of the A, X, Y, and B buttons, you can right-shift the value from the Xbox 360® controller by four places.

The call to *sys.stdout.flush()* ensures that the Python interpreter sends the information to the Arduino as soon as possible.

Without sending any messages to control the LEDs or rumble, your Python script should now look like this:

```
#!/usr/bin/python
import ctypes
import signal
import sys
import usb.backend.libusb1
import usb.core
import usb.util

def clean_getaway(sig, frame):
    try:
        usb.util.release_interface(dev, 0)
    except:
        pass
    sys.exit(0)

signal.signal(signal.SIGINT, clean_getaway)

backend = usb.backend.libusb1.get_backend(
          find_library=lambda x: "/usr/lib/libusb-1.0.so"
          )
dev = usb.core.find(idVendor=0x045E, idProduct=0x028E)
if dev is None:
    sys.stdout.write(chr(0))
    sys.stdout.flush()
    sys.exit(0)
else:
    sys.stdout.write(chr(1))
    sys.stdout.flush()

if dev.is_kernel_driver_active(0):
    dev.detach_kernel_driver(0)
usb.util.claim_interface(dev, 0)

while (1):
    try:
        inp = dev.read(0x81, 20)
        if len(inp) == 20:
            sys.stdout.write(chr(ctypes.c_byte(inp[7]).value + 128))
            sys.stdout.write(chr(inp[3] >> 4))
            sys.stdout.flush()
    except usb.core.USBError:
        pass
```

### Working with Sony PlayStation® DualShock® 4 Controllers

The Sony PlayStation® DualShock® 4 controller is a wireless gamepad for the PS4\. It normally communicates with the console over Bluetooth. However, you can connect it to the Arduino Yún using a USB to micro-USB cable. When in wired mode, the controller works in the same way as most other USB controllers.

The DualShock® 4 contains more endpoints and configuration options than other USB controllers, because it supports additional hardware such as headsets. The DualShock® 4 continually reports the state of all buttons, analog sticks, and accelerometer/gyroscope sensors.

To read from the controller, you can use the *read()* method of the PyUSB device instance. This method accepts two arguments – the endpoint address, and the maximum number of bytes to read. The IN endpoint from which the controller sends button press information is at address 0x84\. And the maximum length of a valid input report is 64 bytes.

Replace the line in the *while* loop (which reads “pass”) with the following code, and then indent it:

```
try:
    inp = dev.read(0x84, 64)
    print inp
except usb.core.USBError:
    pass
```

There are several small errors that can occur during USB transmission. The *try* and *except* statements ensure that if one of these occur, the script continues to read from the controller.

Connect the controller to the vertically-mounted USB socket on your Yún (if it is not connected). Then run this script from the command line, and press a few buttons on the controller. The script sends an array of bytes to the Linux console, and each byte represents a button, analog stick position, or sensor value on the controller.

Tip: When working with DualShock® 4 controllers, there are a lot of values to process. In the following sections, you will see how to extract the individual buttons and pieces of information that you want to use.

When you finish testing, press Ctrl + C to end the script.

The button press report from PS4™ controllers consists of 64 bytes. The table that follows shows a description of the most-commonly used bytes – starting with the second byte, which is at position 1 of the *inp* array.

The first byte (byte 0) specifies the report type. This is always *1* for button input reports. PS4™ controllers may sometimes send shorter reports of a different type.

The main values are:

| Byte No. | Description |
| --- | --- |
| 1 | The x-axis position of the left analog stick. This is an unsigned byte in the range 0–255 (left to right) with the midpoint at 128. |
| 2 | The y-axis position of the left analog stick. This is an unsigned byte in the range 0–255 (up to down) with the midpoint at 128. |
| 3 | The x-axis position of the right analog stick. This is an unsigned byte in the range 0–255 (left to right) with the midpoint at 128. |
| 4 | The y-axis position of the right analog stick. This is an unsigned byte in the range 0–255 (up to down) with the midpoint at 128. |
| 5 | Represents the state of the triangle, circle, cross, and square buttons, and the d-pad. For the d-pad, the least-significant four bits can be one of the following values: 0b0111 – up and left 0b0110 – left 0b0101 – down and left 0b0100 – down 0b0011 – down and right 0b0010 – right 0b0001 – up and right 0b0000 – up 0b1000 – no button pressed For the other buttons, the most-significant four bits each represent the state of one button. If a bit is set, the button is pressed. If a bit is not set, the button is not pressed. From most-significant to least-significant: Bit 7 – triangle Bit 6 – circle Bit 5 – cross Bit 4 – square |
| 6 | Represents the state of the L1, L2, L3, R1, R2, R3, OPTIONS, and SHARE buttons. If a bit is set, the button is pressed. If a bit is not set, the button is not pressed. From most-significant to least-significant: Bit 7 – R3 Bit 6 – L3 Bit 5 – options Bit 4 – share Bit 3 – R2 Bit 2 – L2 Bit 1 – R1 Bit 0 – L1 |
| 7 | The eighth byte of the input report contains a number that automatically increments every time the controller sends a report. However, the least-significant two bits of this value represents the state of the trackpad button and PlayStation Home button. If a bit is not set, the button is not pressed. From most-significant to least-significant: Bit 1 – trackpad button Bit 0 – PlayStation home |

Note: The DualShock® 4 does not have the pressure-sensitive buttons that the DualShock® 3 does.

You can also find the trackpad, accelerometer and gyroscope data in the same input report. However, these features are not used in this project.

#### Controlling the Light Bar and Rumble

The DualShock® 4’s light bar is a 24-bit color device, made up of three channels – red (R), green (G), and blue (B). You can set each channel to a value in the range 0–255\. These values indicate the brightness or strength of each of the primary colors. 0 is off (or black), and 255 is the maximum brightness.

The light bar blends these three values to create colors. For example R:255 G:0 B:0 is a bright red. R:255 G:0 B:255 is a bright purple. And R:255 G:255 B:255 is white.

To set the color of the light bar from your Python script, you can send three bytes (one for each RGB channel) as part of a special message to endpoint 0x03\. In the same message, you can also tell the DualShock® 4 to flash the light bar continuously.

As well as the light bar, the controller contains two small motors that you can use to “rumble” or vibrate the device. The first motor creates a low-frequency, deep (or big) rumble, and the second motor creates a higher-frequency rumble. To control the speed or strength of each motor, you can send a value in the range 0–255 in the same message that you use to control the light bar.

The actual length of the message that you send can vary. However, 11 bytes is enough to set the color of the light bar, the timing of the flashes, and the strength of the rumble. For example:

```
[0x05, 0xFF, 0x00, 0x00, SMALLR, BIGR, RED, GREEN, BLUE, FLASHON, FLASHOFF]
```

The first byte, *0x05*, specifies the message type that you are sending. This is always the same when you send a message to control the light bar and rumble. The next byte is always *0xFF* (255). Bytes 3 and 4 should be zero. The remaining bytes are:

| Option | Description |
| --- | --- |
| SMALLR | A value in the range 0–255 that specifies the strength/speed of the small, high-frequency rumble motor. 0 is off. 255 is the maximum. |
| BIGR | A value in the range 0–255 that specifies the strength/speed of the big, low-frequency rumble motor. 0 is off. 255 is the maximum. |
| RED | The setting for the light bar’s red channel. |
| GREEN | The setting for the light bar’s green channel. |
| BLUE | The setting for the light bar’s blue channel. |
| FLASHON | A value in the range 0–255 that specifies the length of time that the light bar stays on. |
| FLASHOFF | A value in the range 0–255 that specifies the length of time that the light bar stays off. |

The controller uses the *FLASHON* and *FLASHOFF* options together to create a repeating flash. If both options are *0* then the light bar does not flash.

If you activate the rumble feature, the controller automatically turns it off after approximately 3 seconds.

To send a message to the DualShock® 4 to control these features, you need to write it to endpoint 0x03\. For example, to activate both rumble motors and set the light bar to a flashing purple:

```
dev.write(0x03, [0x05,0xFF,0x00,0x00,0xFF,0xFF,0xFF,0x00,0xFF,0x80,0x80])
```

#### Finishing the Python Script

To complete the *controller.py* script, send the x position of the left analog stick and a single byte that represents the state of four buttons to the Arduino sketch. The ATmega32u4 struggles to read the full 64-byte report quickly enough, so it is more efficient to only send the data that the sketch needs.

The sketch in [Building a Test Circuit](#part0010_split_003.html_tp4s4) reads input from the OpenWrt-Yun shell’s standard output device. If you use the Python *print()* function to send these numbers then it may convert them to text. Instead, you can use the *sys.stdout.write()* method.

Replace the line that reads *print inp*, with the following code:

```
if len(inp) == 64:
    sys.stdout.write(chr(inp[1]))
    sys.stdout.write(chr(inp[5] >> 4))
    sys.stdout.flush()
```

The sixth byte (position 5 in the *inp* array) of the input report represents the state of the triangle, circle, cross, and square buttons, as well as the d-pad. To keep the Arduino sketch the same (regardless of which controller you use with this project), the sketch only looks for four buttons. And it expects that the buttons are the least-significant four bits of the number. This means that you must right-shift the value from the PS4™ controller by four places.

The call to *sys.stdout.flush()* ensures that the Python interpreter sends the information to the Arduino as soon as possible.

Without sending any messages to control the DualShock® 4’s light bar or rumble, your Python script should now look like this:

```
#!/usr/bin/python
import signal
import sys
import usb.backend.libusb1
import usb.core
import usb.util

def clean_getaway(sig, frame):
    try:
        usb.util.release_interface(dev, 0)
    except:
        pass
    sys.exit(0)

signal.signal(signal.SIGINT, clean_getaway)

backend = usb.backend.libusb1.get_backend(
          find_library=lambda x: "/usr/lib/libusb-1.0.so"
          )
dev = usb.core.find(idVendor=0x054C, idProduct=0x05C4)
if dev is None:
    sys.stdout.write(chr(0))
    sys.stdout.flush()
    sys.exit(0)
else:
    sys.stdout.write(chr(1))
    sys.stdout.flush()

if dev.is_kernel_driver_active(0):
    dev.detach_kernel_driver(0)
usb.util.claim_interface(dev, 0)

while (1):
    try:
        inp = dev.read(0x84, 64)
        if len(inp) == 64:
            sys.stdout.write(chr(inp[1]))
            sys.stdout.write(chr(inp[5] >> 4))
            sys.stdout.flush()
    except usb.core.USBError:
        pass
```

### Working with Sony PlayStation® DualShock® 3 and SIXAXIS™ Controllers

The Sony PlayStation® DualShock® 3 and SIXAXIS™ controllers are wireless gamepads for the PS3™ game console. They normally communicate with the console over Bluetooth. However, you can connect them to the Arduino Yún using a USB to mini-USB cable. When in wired mode, the controllers work in the same way as most other USB controllers.

Before you read from one of these controllers, you need to tell the controller to send a report that contains the status of the buttons. Add the following code above the line that reads *while (1):*

```
dev.ctrl_transfer(0x21, 0x09, 0x03F4, 0x00, [0x42, 0x0C, 0x00, 0x00])
```

To read from the controller, you can use the *read()* method of the PyUSB device instance. This method accepts two arguments – the endpoint address, and the maximum number of bytes to read. The IN endpoint from which the controller sends button press information is at address 0x81\. And the maximum length of a valid input report is 49 bytes.

Replace the line in the *while* loop that reads “pass” with the following code, and then indent it:

```
try:
    inp = dev.read(0x81, 49)
    print inp
except usb.core.USBError:
    pass
```

There are several small errors that can occur during USB transmission. The *try* and *except* statements ensure that if one of these occurs, the script continues to read from the controller.

Connect the controller to the vertically-mounted USB socket on your Yún (if it is not connected). Then run this script from the command line, and press a few buttons on the controller. The script sends an array of bytes to the Linux console, and each byte represents a button, analog stick position, or accelerometer value on the controller.

When you finish testing, press Ctrl + C to end the script.

The button status report from DualShock® 3 or SIXAXIS™ controllers consists of 49 bytes. The tables that follow show a description of the most-commonly used bytes – starting with the third byte, which is at position 2 of the *inp* array.

The first byte (byte 0) specifies the report type. This is always *1* for button input reports. PS3™ controllers may sometimes send shorter reports of a different type. These do not usually contain button information, and you can ignore them.

Bytes 1, 5, 10, 11, 12, 13, 26, 27, 28, 32, 33, 34, 35, 36, 37, 38, 39, and 40 are reserved and you can ignore them.The main values are:

| Byte No. | Description |
| --- | --- |
| 2 | Represents the state of the d-pad buttons, SELECT, START, L3, and R3\. Each bit represents a different button. If a bit is set, the button is pressed. If a bit is not set, the button is not pressed. From most-significant to least-significant: Bit 7 – left Bit 6 – down Bit 5 – right Bit 4 – up Bit 3 – start Bit 2 – R3 Bit 1 – L3 Bit 0 – SELECT |
| 3 | Represents the state of the cross, circle, triangle and square buttons on the face of the controller, and the L1, L2, R1, and R2 shoulder buttons. Each bit represents a different button. If a bit is set, the button is pressed. If a bit is not set, the button is not pressed. From most-significant to least-significant: Bit 7 – square Bit 6 – cross Bit 5 – circle Bit 4 – triangle Bit 3 – R1 Bit 2 – L1 Bit 1 – R2 Bit 0 – L2 |
| 4 | If the PS button is pressed, this value is *1*. If the button is not pressed, this value is *0*. |
| 6 | The x axis of the left analog stick. This is an unsigned value in the range 0–255 (left to right) with 128 as the midpoint. |
| 7 | The y axis of the left analog stick. This is an unsigned value in the range 0–255 (up to down) with 128 as the midpoint. |
| 8 | The x axis of the right analog stick. This is an unsigned value in the range 0–255 (left to right) with 128 as the midpoint. |
| 9 | The y axis of the right analog stick. This is an unsigned value in the range 0–255 (up to down) with 128 as the midpoint. |

As well as reporting whether each button is pressed, the DualShock® 3 and SIXAXIS™ controllers also report how much pressure the player presses the buttons with. The pressure values are a single byte in the range 0–255, and you can find them at the following positions in the report:

| Byte No. | Pressure Value for |
| --- | --- |
| 14 | up (d-pad) |
| 15 | right (d-pad) |
| 16 | down (d-pad) |
| 17 | left (d-pad) |
| 18 | L2 |
| 19 | R2 |
| 20 | L1 |
| 21 | R1 |
| 22 | triangle |
| 23 | circle |
| 24 | cross |
| 25 | square |

You can also find the accelerometer and gyroscope data in the same input report. However, these features are not used in this project.

#### Setting the DualShock® 3 or SIXAXIS™ LEDs

The DualShock® 3 and SIXAXIS™ have four LED *port indicators*that the PS3™ console can light to tell players which controller number they are. This is useful when you connect multiple controllers to the console.

Tip: Most PS3™ controllers will automatically turn off if you do not set the controller number. It usually a good idea to do this after you send the control message to turn on the button report from the controller.

To set a port indicator, you need to send a message to the controller. This message consists of 48 bytes, and many of the values in this report are predefined. The tenth byte is the port indicator, and it can be one of the following values:

| Value | Description |
| --- | --- |
| 0x00 | Turns off all LEDs and tells the controller that the console is not using it. |
| 0x02 | Turns on LED 1. |
| 0x04 | Turns on LED 2. |
| 0x08 | Turns on LED 3. |
| 0x10 | Turns on LED 4. |
| 0x1F | Turns on all LEDs. |

You can also turn on combinations of LEDs by adding the values together. For example, to turn on LEDs 2 and 4, you can use the value *0x12* (0x02 + 0x10).

Add the following function to your Python script:

```
def setLED(ledn):
    dev.ctrl_transfer(0x21, 0x09, 0x0201, 0 [
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, ledn, 0xFF, 0x27, 0x10, 0x00, 0x32, 0xFF,
        0x27, 0x10, 0x00, 0x32, 0xFF, 0x27, 0x10, 0x00,
        0x32, 0xFF, 0x27, 0x10, 0x00, 0x32, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00
    ])
```

Then, after the line that reads *dev.ctrl_transfer(0x21, 0x09, 0x03F4, 0x00, [0x42, 0x0C, 0x00, 0x00])*, add the following statement:

```
setLED(0x02)
```

#### Controlling the DualShock® 3 Rumble

The DualShock® 3 controller also contains two small motors that you can use to “rumble” or vibrate the device. The first motor creates a low-frequency deep (or big) rumble, and the second motor creates a higher-frequency rumble. You can use four bytes to control the strength of the motors and the duration of time that they stay on for – two bytes for each motor.

Tip: Because of a legal dispute between Sony Computer Entertainment Inc. and the Immersion Corporation, PS3™ controllers without the “DUALSHOCK3” mark do not support rumble. And not all DualShock® 3 controllers support rumble when you connect them over a mini-USB cable.

The control message that you send to the controller is the same as the one that you use to set the port indicator LEDs. In that 48-byte message, bytes 2 and 3 control the right motor and bytes 4 and 5 control the left motor.

The first byte in each pair is a duration. *0xFF* tells the controller to rumble forever (or until you manually set the strength to *0*). Most drivers for DualShock® 3 and SIXAXIS™ gamepads control the rumble this way, and they turn it off manually. The second byte in each pair is the strength of the rumble. The left motor accepts values in the range 0–255\. However, the setting for the right motor can only be *0* or *1*.

For example, the following function extends the *setLED()* function with two additional parameters that activate and deactivate the rumble. This project does not use the rumble features of PS3™ controllers, but you can include this function in the *controller.py* Python script if you want to.

```
def setRumble(ledn, left, righ):
    dev.ctrl_transfer(0x21, 0x09, 0x0201, 0 [
        0x00, 0xFF, righ, 0xFF, left, 0x00, 0x00, 0x00,
        0x00, ledn, 0xFF, 0x27, 0x10, 0x00, 0x32, 0xFF,
        0x27, 0x10, 0x00, 0x32, 0xFF, 0x27, 0x10, 0x00,
        0x32, 0xFF, 0x27, 0x10, 0x00, 0x32, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00
    ])
```

#### Finishing the Python Script

To complete the *controller.py* script, send the x position of the left analog stick and a single byte that represents the state of four buttons to the Arduino sketch. The ATmega32u4 can struggle to read a full-length report quickly enough, so it is more efficient to only send the data that the sketch needs.

The sketch in [Building a Test Circuit](#part0010_split_003.html_tp4s4) reads input from the OpenWrt-Yun shell’s standard output device. If you use the Python *print()* function to send these numbers then it may convert them to text. Instead, you can use the *sys.stdout.write()* method.

Replace the line that reads *print inp*, with the following code:

```
if len(inp) == 49:
    sys.stdout.write(chr(inp[6]))
    sys.stdout.write(chr(inp[3] >> 4))
    sys.stdout.flush()
```

The fourth byte (position 3 in the *inp* array) of the input report represents the state of the triangle, circle, cross, square, and trigger buttons. To keep the Arduino sketch the same (regardless of which controller you use with this project), the sketch only looks for four buttons. And it expects that the buttons are the least-significant four bits of the number. To use the triangle, circle, cross and square buttons with this project, you can right-shift the value from the PS3™ controller by four places.

The call to *sys.stdout.flush()* ensures that the Python interpreter sends the information to the Arduino as soon as possible.

Your Python script should now look like this:

```
#!/usr/bin/python
import signal
import sys
import usb.backend.libusb1
import usb.core
import usb.util

def clean_getaway(sig, frame):
    try:
        usb.util.release_interface(dev, 0)
```

```
 except:
        pass
    sys.exit(0)

signal.signal(signal.SIGINT, clean_getaway)

def setLED(ledn):
    dev.ctrl_transfer(0x21, 0x09, 0x0201, 0 [
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, ledn, 0xFF, 0x27, 0x10, 0x00, 0x32, 0xFF,
        0x27, 0x10, 0x00, 0x32, 0xFF, 0x27, 0x10, 0x00,
        0x32, 0xFF, 0x27, 0x10, 0x00, 0x32, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00
    ])

backend = usb.backend.libusb1.get_backend(
          find_library=lambda x: "/usr/lib/libusb-1.0.so"
          )
dev = usb.core.find(idVendor=0x054C, idProduct=0x0268)
if dev is None:
    sys.stdout.write(chr(0))
    sys.stdout.flush()
    sys.exit(0)
else:
    sys.stdout.write(chr(1))
    sys.stdout.flush()

if dev.is_kernel_driver_active(0):
    dev.detach_kernel_driver(0)
usb.util.claim_interface(dev, 0)

dev.ctrl_transfer(0x21, 0x09, 0x03F4, 0, [0x42, 0x0C, 0x00, 0x00])
setLED(0x02)
while (1):
    try:
        inp = dev.read(0x81, 49)
        if len(inp) == 49:
            sys.stdout.write(chr(inp[6]))
            sys.stdout.write(chr(inp[3] >> 4))
            sys.stdout.flush()
    except usb.core.USBError:
        pass
```

### Working with PC USB Controllers

USB game controllers for the PC come in many different shapes and sizes, with a wide-variety of buttons. Because of this, it is not possible to provide detailed instructions for all of the different controllers. This section is an example of using a Thrustmaster® Firestorm Dual Power gamepad. However, most PC gamepads are fairly similar.

In its default configuration, the Firestorm Dual Power reports the state of all buttons and the positions of the analog sticks continuously. You only need to read from the input endpoint.

To read from the controller, you can use the *read()* method of the PyUSB device instance. This method accepts two arguments – the endpoint address, and the maximum number of bytes to read. The IN endpoint from which the controller sends button press information is at address 0x81\. And the maximum length (in bytes) of a valid input report is seven.

Replace the line in the *while* loop that reads “pass” with the following code, and then indent it:

```
try:
    inp = dev.read(0x81, 7)
    print inp
except usb.core.USBError:
    pass
```

There are several small errors that can occur during USB transmission. The *try* and *except* statements ensure that if one of these occurs, the script will continue to try and read from the controller instead of ending with an error message.

Connect the controller to the vertically-mounted USB socket on your Yún (if it is not connected). Then run this script from the command line, and press a few buttons on the controller. The script sends an array of bytes to the Linux console, and each byte represents a button, analog stick position, or accelerometer value on the controller.

When you finish testing, press Ctrl + C to end the script.

The input report consists of seven bytes. The following table shows a description of each byte – starting with the first byte, which is at position 0 of the *inp* array.

| Byte No. | Description |
| --- | --- |
| 0 | Represents the state of the four buttons on the face of the controller, and the four shoulder buttons. Each bit represents a different button. If a bit is set, the button is pressed. If a bit is not set, the button is not pressed. From most-significant to least-significant: Bit 7 – bottom-right shoulder button Bit 6 – top-right shoulder button Bit 5 – bottom-left shoulder button Bit 4 – top-left shoulder button Bit 3 – button 4 Bit 2 – button 3 Bit 1 – button 2 Bit 0 – button 1 |
| 1 | Represents the state of the two trigger buttons and the analog stick buttons. Each bit represents a different button. If a bit is set, the button is pressed. If a bit is not set, the button is not pressed. From most-significant to least-significant: Bit 3 – right analog stick button Bit 2 – left analog stick button Bit 1 – right trigger Bit 0 – left trigger |
| 2 | If digital mode is enabled, this value is always 224\. If dual analog mode is enabled then this is value is 240 unless the d-pad is pressed. If the d-pad is pressed, this byte can have the following values: 0 – up 16 – up and right 32 – right 48 – down and right 64 – down 80 – down and left 96 – left 112 – up and left |
| 3 | In digital mode, this value is 0 unless the left or right d-pad button is pressed. If the value is 127 then the right d-pad is pressed; if this value is -128 then the left d-pad is pressed. In dual analog mode, this is a value that represents the x axis of the left analog stick. It is a signed 8-bit number, in the range -128–127 (left to right) with 0 as the midpoint. |
| 4 | In digital mode, this value is 0 unless the up or down d-pad buttons are pressed. If the value is 127 then the down d-pad is pressed; if this value is -128 then the up d-pad is pressed. In dual analog mode, this is a value that represents the y axis of the left analog stick. It is a signed 8-bit number, in the range -128–127 (up to down) with 0 as the midpoint. |
| 5 | The x axis of the right analog stick. This is a signed value in the range -128–127 (left to right) with 0 as the midpoint. |
| 6 | The y axis of the right analog stick. This is a value in the range 0–255 (up to down), with 128 as the midpoint. |

Note: The *controller.py* script does not display the negative numbers correctly yet. You can fix this later.

#### Turning On Rumble

The Thrustmaster® Firestorm Dual Power controller contains two small motors that you can use to “rumble” or vibrate the device. The first motor creates a high-frequency rumble, and the second motor creates a low-frequency rumble. To control the speed or strength of each motor, you can send a value in the range 0–255 to the controller.

To the send a rumble message, you need an array of four bytes. For example:

```
[0xFF, 0xFF, 0x00, 0x00]
```

The first byte is the strength of the “fast” (high-frequency) rumble. The second byte is the strength of the “slow” (low-frequency) rumble.

To send this information to the controller, you can use the following code:

```
dev.write(0x21, 0x09, 0x0200, 0, [0xFF, 0xFF, 0x00, 0x00])
```

After you start the rumble feature, you have to turn it off yourself. If you are testing the rumble in *controller.py*, you can add this line to the top of the *clean_getaway()* function.

```
dev.write(0x21, 0x09, 0x0200, 0, [0x00, 0x00, 0x00, 0x00])
```

This ensures that the rumble ends when the script does.

#### Finishing the Python Script

To complete the controller.py script, send the x position of the left analog stick and a single byte that represents the state of four buttons to the Arduino sketch. The ATmega32u4 can struggle to read a full-length report quickly enough, so it is more efficient to only send the data that the sketch needs.

The sketch in [Building a Test Circuit](#part0010_split_003.html_tp4s4) reads input from the OpenWrt-Yun shell’s standard output device. If you use the Python *print()* function to send these numbers then it may convert them to text. Instead, you can use the *sys.stdout.write()* method.

Add the following *import* declaration to the script:

```
import ctypes
```

And then replace the line that reads *print inp*, with the following code:

```
if len(inp) == 7:
    sys.stdout.write(chr(ctypes.c_byte(inp[3]).value + 128))
    sys.stdout.write(chr(inp[0]))
    sys.stdout.flush()
```

The fourth byte of the input report (position 3 in the array *inp*) is a signed byte that specifies the x position of the left analog stick. However, Python is not adept at handling signed 8-bit numbers, and it loses the sign when it reads the position from the USB device. Since the lowest eight bits of the number are not changed, you can restore the sign.

The *ctypes* module contains functions and data types that closely correspond to the data types used in C. *c_byte* is an 8-bit signed byte. The code above first converts *inp[7]* to a *c_byte*, which preserves negative values. It then gets a Python integer from this, using the *value* property. The result is a signed Python integer in the range -128–127\. However, the Arduino sketch expects the analog stick position to be in the range 0–255\. By adding 128 to the value, you convert -128–127 numbers to 0–255 numbers.The call to *sys.stdout.flush()* ensures that the Python interpreter sends the information to the Arduino as soon as possible.Your Python script should now look like this:

```
#!/usr/bin/python
import ctypes
import signal
import sys
import usb.backend.libusb1
import usb.core
import usb.util

def clean_getaway(sig, frame):
    try:
        usb.util.release_interface(dev, 0)
    except:
        pass
    sys.exit(0)

signal.signal(signal.SIGINT, clean_getaway)

backend = usb.backend.libusb1.get_backend(
          find_library=lambda x: "/usr/lib/libusb-1.0.so"
          )
dev = usb.core.find(idVendor=0x044F, idProduct=0xB304)
if dev is None:
    sys.stdout.write(chr(0))
    sys.stdout.flush()
    sys.exit(0)
else:
    sys.stdout.write(chr(1))
    sys.stdout.flush()

if dev.is_kernel_driver_active(0):
    dev.detach_kernel_driver(0)
usb.util.claim_interface(dev, 0)

while (1):
    try:
        inp = dev.read(0x81, 7)
        if len(inp) == 7:
            sys.stdout.write(chr(ctypes.c_byte(inp[3]).value + 128))
            sys.stdout.write(chr(inp[0]))
            sys.stdout.flush()
    except usb.core.USBError:
        pass
```

* * *

## Building a Test Circuit

You can build the circuit for this project on a standard, half-size breadboard. If you want to expand the project by adding more LEDs, you can do so by connecting them in the same way that the following diagram shows.

If you want to add additional servo motors, you should be aware that servos can draw significant amounts of current. The Arduino is not a suitable power source if you are using more than one or two servos. In those situations, you should power the servos from an external battery, or DC adapter and voltage regulator.

Disconnect the Yún from its power supply (or unplug the USB cable), and then build the circuit as shown in Figure 16.

![](images/00017.jpeg) 

Figure 16\. Connecting LEDs and a servo to the Arduino

On this diagram, the longer, left leg of each LED is the anode and you should connect these to an Arduino digital pin. One for each LED. The right leg of each LED is the cathode; connect these to ground through 220 Ω resistors.

Reconnect the power to the Arduino Yún. Then start the Arduino IDE and add the following line to the top of a new sketch:

```
#include <Bridge.h>
```

Then declare the LED pins. For example:

```
#define LED1    2
#define LED2    3
#define LED3    4
#define LED4    5
```

Tip: *#define* is a compiler instruction. It tells the Arduino’s C compiler to replace every instance of the first term with the second. For example, when you hit *Verify* or *Upload*, every time the compiler sees the word “LED1” in the source code, it uses the text “2” instead.

In the sketch’s *setup()* function, set the digital pins to *OUTPUT*.

```
pinMode(LED1, OUTPUT);
pinMode(LED2, OUTPUT);
pinMode(LED3, OUTPUT);
pinMode(LED4, OUTPUT);
```

Then set all of the LEDs *HIGH*, to show that the sketch runs.

```
digitalWrite(LED1, HIGH);
digitalWrite(LED2, HIGH);
digitalWrite(LED3, HIGH);
digitalWrite(LED4, HIGH);
```

When it starts, the *controller.py* script tries to detect a game controller. If it finds one, the script sends *1* to the ATmega32u4\. If it does not find the controller, it sends *0* and then ends.

To communicate with the Python script, the Arduino sketch needs to: start the Bridge library; start the Python script; and then read the information from the script process.

In [Running Commands and Scripts](#part0007_split_002.html_tc4s3), you can see how to control Linux processes and run commands through the Arduino Bridge library. This project reuses one instance of the *Process* class, and so you should declare it as a global variable, underneath the *#define* statements.

```
Process p;
```

Then add the following code to the sketch’s *setup()* function, underneath the calls to *digitalWrite()*:

```
Bridge.begin();
p.runShellCommand("killall controller.py");
p.runShellCommandAsynchronously("/mnt/sda1/P4/controller.py");
while (p.available() == 0);
if (p.read() != 1) {
    while (1) {
        digitalWrite(LED1, LOW);
        digitalWrite(LED2, LOW);
        digitalWrite(LED3, LOW);
        digitalWrite(LED4, LOW);
        delay(500);
        digitalWrite(LED1, HIGH);
        digitalWrite(LED2, HIGH);
        digitalWrite(LED3, HIGH);
        digitalWrite(LED4, HIGH);
        delay(500);
    }
}
else {
        digitalWrite(LED1, LOW);
        digitalWrite(LED2, LOW);
        digitalWrite(LED3, LOW);
        digitalWrite(LED4, LOW);
}
```

Change the file name and file path in the call to *runShellCommandAsynchronously()* to specify the location of your *controller.py* Python script.

If you run one copy of your script and then start another, the second process is unable to access the controller safely. Since the sketch on the ATmega32u4 starts the Python script on the AR9331, this can happen if the ATmega32u4 resets but the AR9331 does not.

To prevent this, the code uses the Linux command *killall* to terminate the older script before the sketch starts a new one.

```
p.runShellCommand("killall controller.py");
```

If the script does not find the correct USB peripheral, the Arduino sketch enters an infinite loop and flashes the LEDs until you reset the Arduino. This prevents the sketch from moving into its *loop()* function.

If the Python script does find the controller, the Arduino sketch turns off all of the LEDs and moves into the *loop()* function.

In *loop()*, you need to:

1.  Read the input report into a buffer array.
2.  Check which buttons are pressed on the controller.
3.  Turn on the appropriate LEDs.
4.  Check the position of the analog stick.
5.  Adjust the position of the servo.

To start this, add the following code to your sketch’s *loop()*function:

```
char buf[2];
for (int i=0; i<2; i++) {
    while (p.available() == 0);
    buf[i] = p.read();
}
```

The Python script sends a 2-byte message. The first byte is the horizontal position of an analog stick; the second byte contains the status of four buttons.

The least-significant four bits of this number represent the state of the buttons. To detect an individual button press, you need to use bitwise operations. Since arrays on the Arduino start at position 0, you can access the button information using the code *buf[1]*. To check each button and set the LEDs, add the following code underneath the *for* loop:

```
if (buf[1] & 0b00000001) {
    digitalWrite(LED1, HIGH);
}
else {
    digitalWrite(LED1, LOW);
}

if (buf[1] & 0b00000010) {
    digitalWrite(LED2, HIGH);
}
else {
    digitalWrite(LED2, LOW);
}

if (buf[1] & 0b00000100) {
    digitalWrite(LED3, HIGH);
}
else {
    digitalWrite(LED3, LOW);
}

if (buf[1] & 0b00001000) {
    digitalWrite(LED4, HIGH);
}
else {
    digitalWrite(LED4, LOW);
}
```

Each of these comparisons works the same way – the code “and”s a number to the button input. Each number only has one bit set. The result of this operation is *0* if the selected bit is clear in *buf[1]*, or a different number if the bit is set in *buf[1]*. When used in an *if* statement, *0* evaluates as *false* and anything else evaluates as *true*.

### Controlling the Angle of the Servo

Standard servos allow the rotation of the shaft to be set from 0 through 180 degrees, with 90 as the center point. This sketch should work with all standard RC (hobby) servo motors that connect with three pins: 5 V, pulse, and ground. However, you should check the datasheet for the part that you have, to ensure that you are using the component within its capabilities and have wired it up correctly.

The Arduino IDE comes with a library for controlling servos – Servo.h. Include this library at the top of the sketch:

```
#include <Servo.h>
```

In this project, the pulse line of the servo connects to Arduino digital pin 6, and the servo library uses this line to move the motor. Add these two lines underneath the existing *#define* lines:

```
#define SRV1    6
Servo servo1;
```

To prepare the servo for use, you call the *attach()* method from the *Servo* class. Then use the method *write()* to move the servo to its center position – it may have moved while connecting the wires, or could be out of position if the sketch has run previously.

Add the following lines to the *setup()* function in your sketch, before the call to *Bridge.begin()*:

```
servo1.attach(SRV1);
servo1.write(90);
```

The *controller.py* Python script sends one unsigned byte to represent the horizontal position of the analog stick. An unsigned byte contains values in the range 0–255, with 128 as the midpoint or center position. However, the servo only accepts values in the range 0–180, with 90 as the center position.

Tip: Signed numbers can be negative or positive values, or zero. Unsigned numbers can only be zero or positive. The difference is in how the compiler performs mathematical operations on the binary number. For example, the binary number 0b10000000 is 128 if the compiler treats it as unsigned. But it is -128 if the compiler treats it as signed.

To make the servo move correctly, you can translate the position of the analog stick into a signed byte in the range -90–90\. If you subtract this number from the servo center point (90) then the sketch can move the servo in the appropriate direction.

You can use the Arduino *map()* function to translate the analog stick position into the range -90–90\. This function takes five arguments:

| Argument | Description |
| --- | --- |
| value | The number that the function translates. |
| fromLow | The lowest number that *value* can be. |
| fromHigh | The highest number that *value* can be. |
| toLow | The lowest number that the result can be. |
| toHigh | The highest number that the result can be. |

For example:

```
map(buf[0], 0, 255, -90, 90)
```

To move the servo in response to the position of the analog stick, add this line to the bottom your sketch’s *loop()* function:

```
servo1.write(90 - map((unsigned char)buf[0], 0, 255, -90, 90));
```

Note that *(unsigned char)* forces the Arduino C compiler to treat *buf[0]* as an unsigned byte. This is a precaution in case the compiler thinks that *buf[0]* is a signed number.

If your servo turns in a different direction, or has a wider range of motion than standard RC servo motors, then you may need to adjust this code.

* * *

## Source Code – Sketch

```
#include <Servo.h>
#include <Bridge.h>

#define LED1    2
#define LED2    3
#define LED3    4
#define LED4    5
#define SRV1    6

Servo servo1;
Process p;

void setup() {
    pinMode(LED1, OUTPUT);
    pinMode(LED2, OUTPUT);
    pinMode(LED3, OUTPUT);
    pinMode(LED4, OUTPUT);
    digitalWrite(LED1, HIGH);
    digitalWrite(LED2, HIGH);
    digitalWrite(LED3, HIGH);
    digitalWrite(LED4, HIGH);

    servo1.attach(SRV1);
    servo1.write(90);

    Bridge.begin();
    p.runShellCommand("killall controller.py");
    p.runShellCommandAsynchronously("/mnt/sda1/P4/controller.py");
    while (p.available() == 0);
    if (p.read() != 1) {
        while (1) {
            digitalWrite(LED1, LOW);
            digitalWrite(LED2, LOW);
            digitalWrite(LED3, LOW);
            digitalWrite(LED4, LOW);
            delay(500);
            digitalWrite(LED1, HIGH);
            digitalWrite(LED2, HIGH);
            digitalWrite(LED3, HIGH);
            digitalWrite(LED4, HIGH);
            delay(500);
        }
    }
    else {
        digitalWrite(LED1, LOW);
        digitalWrite(LED2, LOW);
        digitalWrite(LED3, LOW);
        digitalWrite(LED4, LOW);
    }
}

void loop() {
    char buf[2];
    for (int i=0; i<2; i++) {
        while (p.available() == 0);
        buf[i] = p.read();
    }

    if (buf[1] & 0b00000001) {
        digitalWrite(LED1, HIGH);
    }
    else {
        digitalWrite(LED1, LOW);
    }

    if (buf[1] & 0b00000010) {
        digitalWrite(LED2, HIGH);
    }
    else {
        digitalWrite(LED2, LOW);
    }

    if (buf[1] & 0b00000100) {
        digitalWrite(LED3, HIGH);
    }
    else {
        digitalWrite(LED3, LOW);
    }

    if (buf[1] & 0b00001000) {
        digitalWrite(LED4, HIGH);
    }
    else {
        digitalWrite(LED4, LOW);
    }

    servo1.write(90 - map((unsigned char)buf[0], 0, 255, -90, 90));
}
```

* * *

[1](#part0010_split_000.html_nf1)Rubini, Alessandro, and Jonathan Corbet. 2005\. Linux Device Drivers. Sebastopol: O’Reilly Media Inc.[2](#part0010_split_001.html_nf2)When you finish coding the project, you can disconnect the Arduino from your network and still use the circuit.[3](#part0010_split_001.html_nf3)Axelson, Jan. 2009\. USB Complete. Madison, Wis: Lakeview Research LLC.[4](#part0010_split_002.html_nf4)Replace \\.\USBPcap6 with the device that you want to spy on.[5](#part0010_split_002.html_nf5)Replace \\.\USBPcap6 with the device that you want to spy on.

# Project 5 – Making a USB Accelerometer Mouse

When you connect an Arduino Yún to a computer using a micro-USB cable, the computer identifies the Yún as a serial port. This allows the Arduino IDE to upload sketches, and you can communicate with the Yún from any terminal software that supports serial connections.

Many Arduinos (and other development boards) use a dedicated chip to tell the computer that the device is a USB serial port, and to exchange data. However, the ATmega32u4 on the Arduino Yún, Arduino Leonardo, and Arduino Micro has a built-in USB connection. These Arduinos do not need an additional chip.

Because the ATmega32u4 is programmable, you can make the Arduino Yún appear as different types of USB device. The Arduino IDE compiles sketches so that they include the option of using the Yún as a mouse or keyboard.

This project reads values from an accelerometer sensor module and uses this information to move the mouse pointer – it creates a prototype controller that you use by tilting the Arduino.To complete this project, you need:

1.  An Arduino Yún.
2.  A USB to micro-USB cable.
3.  An MPU-6050 triple-axis accelerometer and gyroscope breakout board.
4.  Two 10 kΩ resistors.
5.  Two momentary push buttons[1](#part0011_split_003.html_fn1).
6.  A mini breadboard from an Arduino ProtoShield.
7.  Jumper wires.

In This Chapter

[Connecting to an Accelerometer Module](#part0011_split_000.html_tp5s1)

[Using the Mouse Class](#part0011_split_001.html_tp5s2)

[Source Code – Sketch](#part0011_split_002.html_tp5s3)

* * *

## Connecting to an Accelerometer Module

Gyroscopes and accelerometers are two types of sensor that you can use to measure movement and orientation.

A gyroscope has a tiny, spinning disc inside. When you tilt or turn a spinning disc, it pushes back in the opposite direction to try and remain in the same position. This is the gyroscopic effect, and a gyroscope uses this to determine the orientation of the sensor. Over time, and with large movements, gyroscopes become less accurate.

An accelerometer measures acceleration or movement in a specific direction. When you stop moving the device, even if it is still at an angle, the value returned by an accelerometer usually return to zero.

To avoid the limitations that each type of sensor has if used on its own, manufacturers create devices that have both types of sensor in one module. The MPU-6050 is a single-chip sensor that combines a triple-axis gyroscope with a triple-axis accelerometer. You communicate with this device using I2C.

Many different companies produce breakout boards that contain an MPU-6050\. The list below shows a few links to appropriate boards, but you can find others by searching the web for “MPU-6050 breakout board”.

*   [http://www.sainsmart.com/sainsmart-mpu-6050-3-axis-gyroscope-module.html](http://www.sainsmart.com/sainsmart-mpu-6050-3-axis-gyroscope-module.html)
*   [http://www.sparkfun.com/products/11028](http://www.sparkfun.com/products/11028)
*   [http://www.geeetech.com/triple-axis-accelerometergyro-breakout-mpu6050-p-539.html](http://www.geeetech.com/triple-axis-accelerometergyro-breakout-mpu6050-p-539.html)
*   [http://www.robotshop.com/en/6-dof-gyro-accelerometer-imu-mpu6050.html](http://www.robotshop.com/en/6-dof-gyro-accelerometer-imu-mpu6050.html)

You can use most MPU-6050 breakout boards with both 3 V and 5 V Arduinos. For this project, make sure your sensor is able to work with 5 V.

If your breakout board does not have header pins, you need to solder some onto the board. The code in this project assumes that you solder the pins so that the breakout board fits into the breadboard as shown in Figure 17\. If you solder the pins so that the breakout board fits in upside down, the readings from the sensor change. This is fixable in the sketch code.

Remove the power from your Yún and connect the circuit as shown in the following diagram.

![](images/00018.jpeg) 

Figure 17\. Connecting an MPU-6050 to an Arduino

The mini breadboard from an Arduino ProtoShield fits on top of the Arduino Yún. You do not need to stick the breadboard to the Arduino for this project.

Your MPU-6050 breakout board may have a different number of pins than the one in Figure 17\. You should connect:

| MPU-6050 | To Arduino Pin: |
| --- | --- |
| VCC | 5V. |
| GND | GND. |
| SCL | Digital pin 3. |
| SDA | Digital pin 2. |

Connect one leg of each button to ground. Connect the other leg of each button to a 10 kΩ resistor. One resistor connects to Arduino digital pin 4, and the other connects to Arduino digital pin 5.

Electricity should not flow between the two legs of each button, unless you press the switch.

If you want to use the full Arduino ProtoShield, you can use extra-long pin headers to increase the space between the Yún and the ProtoShield. Without these headers, the ProtoShield’s pins do not fully-connect with the Arduino and the shield may not work correctly.

![](images/00019.jpeg) 

Figure 18\. Using pin headers to fit a ProtoShield to an Arduino Yún

### Installing the MPU-6050 and I2Cdev Libraries

Using data from gyroscopes and accelerometers involves a lot of calculations and algorithms. This project uses Jeff Rowberg’s MPU-6050 library to simplify working with the sensor module. The MPU-6050 library uses an additional library, I2Cdev.

To download these libraries and install them in your Arduino IDE on Microsoft Windows or Mac OS X,

1.  Download the I2Cdev library from the following URL: [http://arduinomeetslinux.com/download/I2Cdev.zip](http://arduinomeetslinux.com/download/I2Cdev.zip)
2.  Open the Arduino IDE.
3.  On the **Sketch** menu, click **Import Library**, and then click **Add Library**.
4.  Find the *I2Cdev.zip* file, click it, and then click **Open**.
5.  Download the MPU-6050 library from the following URL: [http://arduinomeetslinux.com/download/MPU6050.zip](http://arduinomeetslinux.com/download/MPU6050.zip)
6.  In the Arduino IDE, on the **Sketch** menu, click **Import Library**, and then click **Add Library**.
7.  Find the *MPU6050.zip* file, click it, and then click **Open**.

The MPU-6050 library is a very comprehensive and large collection of code. You may want to read the library’s source code to learn about the other features that it has.

### Working with the MPU-6050

Start a new sketch in the Arduino IDE, and then add the following *include* directives:

```
#include <Wire.h>
#include <I2Cdev.h>
#include <MPU6050.h>
```

Then declare an instance of *MPU6050* class:

```
MPU6050 mpu;
```

In your sketch’s *setup()* function, add the following code:

```
Serial.begin(115200);
while (!Serial);
```

You can start the MPU-6050 by calling the *initialize()* method from the *MPU6050* class. This method does not return a result, but you can check whether you wired the breakout board correctly by using the method *testConnection()*.

Add this code underneath *while (!Serial);*:

```
Serial.print("Testing MPU-6050 connection... ");
Wire.begin();
mpu.initialize();
if (!mpu.testConnection()) {
    Serial.println("Not connected!");
    while (1);
}
Serial.println("OK.");
```

Connect the Arduino to your PC using the micro-USB cable. Upload the sketch to your Arduino, and then open the Serial Monitor in the Arduino IDE.

If you see the text “Testing MPU-6050 connection… OK.” then the sketch communicates with the breakout board successfully and you can continue.

Tip: If you see the text “Testing MPU-6050 connection… Not connected!”, or if “Testing MPU-6050 connection…” remains on the display for a long period, check your circuit matches the one in [Connecting to an Accelerometer Module](#part0011_split_000.html_tp5s1).

The *MPU6050* method *getMotion6()* reads from the MPU-6050 and returns six values. The first three values represent the three axis values from the accelerometers. The last three values represent the three axis values from the gyroscope.

To call this method, you need to pass in the address of six variables. *getMotion6()* writes the information to these memory addresses.

Underneath the line *MPU6050 mpu;* add the following variables:

```
int16_t ax, ay, az, gx, gy, gz;
```

The *int16_t* type ensures that each variable is a signed 16-bit integer number.

In your sketch’s *loop()* function, add the following line:

```
mpu.getMotion6(&ax, &ay, &az, &gx, &gy, &gz);
```

In this code, the ampersand is the *address of* operator. This tells the compiler to pass in the memory address of the variable, not the value of the variable.

Underneath that line, add:

```
Serial.print("X: ");
Serial.print(ax);
Serial.print(" Y: ");
Serial.println(ay);
delay(20);
```

Upload this sketch and then open the Serial Monitor. If you move and tilt the Arduino, the numbers change. Even though accelerometers usually do not maintain a value when they stop moving, the MPU-6050 and the accompanying library ensure that *ax*, *ay*, and *az* are always useful.

*ax* and *ay* contain all of the data you need. These numbers are usually in the range -18000 through 18000\. Using the Arduino *map()* function, you can scale the data to a more workable range.

The *map()* function takes five arguments:

| Argument | Description |
| --- | --- |
| value | The number that the function translates. |
| fromLow | The lowest number that *value* can be. |
| fromHigh | The highest number that *value* can be. |
| toLow | The lowest number that the result can be. |
| toHigh | The highest number that the result can be. |

Add the following lines before *Serial.print(“X: “);*:

```
int vx = map(ax, -18000, 18000, 90, -90);
int vy = map(ay, -18000, 18000, 90, -90);
```

This maps the values to angles in the range 90° through -90°, with zero as the midpoint.

Now change *Serial.print(ax);* to

```
Serial.print(vx);
```

And *Serial.println(ay);* to:

```
Serial.println(vy);
```

Upload this sketch and then open the Serial Monitor.

If you tilt the Arduino up and down, the *Y* value changes. In the next section of this chapter, this controls the vertical position of the mouse pointer.

If you twist the Arduino, the *X* value changes. This controls the horizontal position of the mouse pointer.

![](images/00020.jpeg) 

Figure 19\. Twisting and turning the Arduino

In the next section, you can see how to use these values to move the mouse pointer on your computer. If the mouse pointer moves in the wrong direction – if it moves up when it should move down, or left when it should move right – you can change the range in the calls to *map()*.

For example:

```
int vx = map(ax, -18000, 18000, -90, 90);
int vy = map(ay, -18000, 18000, -90, 90);
```

* * *

## Using the Mouse Class

Before continuing, remove all references to the *Serial* class. You do not need them.

When you compile an Arduino sketch and upload it to the ATmega32u4, the Arduino IDE combines your sketch with some standard code. On the Arduino Yún, part of this code describes the Arduino to the USB control devices in a PC.

The code tells the PC that the Yún contains three USB devices – a serial port, a mouse, and a keyboard. To send a mouse message from the Yún, you only need to call methods in the *Mouse* class.

Tip: To keep compatibility with other mouse libraries and example code, the Yún’s *Mouse* class includes the methods *begin()* and *end()*. However, these methods are empty on the Yún; you do not need to use them.

The *Mouse* class contains the following methods:

| Method | Description |
| --- | --- |
| begin() | On the Yún, this method is not required. |
| click() | Sends a click event to the computer. Without any arguments, this is a left click. Or you can pass in one of the following values: *MOUSE_LEFT*, *MOUSE_RIGHT*, or *MOUSE_MIDDLE*. |
| end() | On the Yún, this method is not required. |
| isPressed() | Returns *true* if the selected button is pressed, or *false* if it is not. Without any arguments, this checks the state of the left button. Or you can pass in one of the following values: *MOUSE_LEFT*, *MOUSE_RIGHT*, or *MOUSE_MIDDLE*. |
| move() | Moves the mouse pointer by the specified amount. This method accepts two or three arguments. The first argument specifies the distance to move the mouse pointer on the horizontal axis. This can be negative (to move the pointer to the left) or positive (to move the pointer to the right). The second argument specifies the distance to move the pointer on the vertical axis. The third argument is the amount that the scroll wheel moves. |
| press() | Sends a mouse button “down” event to the computer to tell it that one of the mouse buttons is pressed. Without any arguments, this is the left button. Or you can pass in one of the following values: *MOUSE_LEFT*, *MOUSE_RIGHT*, or *MOUSE_MIDDLE*. |
| release() | Sends a mouse button “up” event to the computer to tell it that one of the mouse buttons is not pressed. Without any arguments, this is the left button. Or you can pass in one of the following values: *MOUSE_LEFT*, *MOUSE_RIGHT*, or *MOUSE_MIDDLE*. |

To modify your sketch so that it moves the mouse pointer, you need to translate the *ax* and *ay* angles into distances. The approach taken in this project is to move the mouse pointer by a predefined amount depending on the orientation of the Arduino. The more you tilt the Arduino, the more the sketch moves the mouse pointer.

There are many ways of doing this. The example below is not elegant, but it is easy to modify to suit your preferences.

Add the following function to the sketch:

```
int angleToDistance(int a) {
    if (a < -80) {
        return -40;
    }
    else if (a < -65) {
        return -20;
    }
    else if (a < -50) {
        return -10;
    }
    else if (a < -15) {
        return -5;
    }
    else if (a < -5) {
        return -1;
    }
    else if (a > 80) {
        return 40;
    }
    else if (a > 65) {
        return 20;
    }
    else if (a > 50) {
        return 10;
    }
    else if (a > 15) {
        return 5;
    }
    else if (a > 5) {
        return 1;
    }
    else {
        return 0;
    }
}
```

Then add the following line, before *delay(20);*:

```
Mouse.move(angleToDistance(vx), angleToDistance(vy));
```

The combination of the values returned by *angleToDistance()* and the value in the call to *delay()* determine how responsive the mouse pointer is, and how fast it moves. Too fast or responsive and the pointer is difficult to control. To slow or unresponsive and the mouse is frustrating to use. You should adjust these values until you find a setting that is comfortable for you.

Upload the sketch to your Arduino. After the sketch begins, moving the Arduino should move the mouse pointer on your PC.

When a sketch sends mouse events to the PC, you may find it difficult to upload new sketches over a USB cable. If this happens, either:

*   Press the **32U4 RST** button twice, and then click **Upload** in the Arduino IDE; or
*   Connect your Yún to your local network, and then upload the sketch over TCP/IP.

### Adding the Left and Right Mouse Buttons

The circuit in [Connecting to an Accelerometer Module](#part0011_split_000.html_tp5s1) uses two push buttons to act as left and right mouse buttons. These buttons connect to digital pins 4 and 5.

Add the following code underneath the *#include* directives in your sketch:

```
#define LBUT    4
#define RBUT    5
```

Tip: *#define* is a compiler instruction. It tells the Arduino’s C compiler to replace every instance of the first term with the second. For example, when you hit *Verify* or *Upload*, every time the compiler sees the word “LED1” in the source code, it uses the text “2” instead.

The wiring in this circuit connects the buttons to ground when you press them. This reads as *LOW* in the Arduino sketch.

When a button is not pressed, it connects to an Arduino digital pin at one end, but nothing at the other. To stop the pin “floating”, you can enable the Arduino’s internal pull-up resistors. This ensures that when the button is not pressed, it always reads *HIGH* in the sketch.

Add the following lines to the top of your sketch’s *setup()* function:

```
pinMode(LBUT, INPUT);
digitalWrite(LBUT, HIGH);
pinMode(RBUT, INPUT);
digitalWrite(RBUT, HIGH);
```

Writing a *HIGH* to an *INPUT* pin enables the pull-up resistor.

Before the line that reads *delay(20);* in your sketch’s *loop()* function, add the following code:

```
if (digitalRead(LBUT) == LOW) {
    if (!Mouse.isPressed(MOUSE_LEFT)) {
        Mouse.press(MOUSE_LEFT);
    }
}
else {
    if (Mouse.isPressed(MOUSE_LEFT)) {
        Mouse.release(MOUSE_LEFT);
    }
}

if (digitalRead(RBUT) == LOW) {
    if (!Mouse.isPressed(MOUSE_RIGHT)) {
        Mouse.press(MOUSE_RIGHT);
    }
}
else {
    if (Mouse.isPressed(MOUSE_RIGHT)) {
        Mouse.release(MOUSE_RIGHT);
    }
}
```

If the sketch reads that a button is *LOW*, it only needs to send a mouse event message to the PC if the state of the button is different from the last time that it sent a message. The *Mouse* class stores the last state of the mouse buttons, so you can use *isPressed()* to check whether things change.

If the push button is down but *isPressed()* returns *false*, the code calls *press()* to tell the PC that the mouse button is down. If the push button is up (not pressed) but *isPressed()* returns *true*, the code calls *release()* to tell the PC that the mouse button is not down anymore.

You can find the source code for the completed sketch in the following section.

* * *

## Source Code – Sketch

```
#include <Wire.h>
#include <I2Cdev.h>
#include <MPU6050.h>

#define LBUT    4
#define RBUT    5

MPU6050 mpu;
int16_t ax, ay, az, gx, gy, gz;

int angleToDistance(int a) {
    if (a < -80) {
        return -40;
    }
    else if (a < -65) {
        return -20;
    }
    else if (a < -50) {
        return -10;
    }
    else if (a < -15) {
        return -5;
    }
    else if (a < -5) {
        return -1;
    }
    else if (a > 80) {
        return 40;
    }
    else if (a > 65) {
        return 20;
    }
    else if (a > 50) {
        return 10;
    }
    else if (a > 15) {
        return 5;
    }
    else if (a > 5) {
        return 1;
    }
    else {
        return 0;
    }
}

void setup() {
    pinMode(LBUT, INPUT);
    digitalWrite(LBUT, HIGH);
    pinMode(RBUT, INPUT);
    digitalWrite(RBUT, HIGH);

    Wire.begin();
    mpu.initialize();
    if (!mpu.testConnection()) {
        while (1);
    }
}

void loop() {
    mpu.getMotion6(&ax, &ay, &az, &gx, &gy, &gz);
    int vx = map(ax, -18000, 18000, 90, -90);
    int vy = map(ay, -18000, 18000, 90, -90);
    Mouse.move(angleToDistance(vx), angleToDistance(vy));

    if (digitalRead(LBUT) == LOW) {
        if (!Mouse.isPressed(MOUSE_LEFT)) {
            Mouse.press(MOUSE_LEFT);
        }
    }
    else {
        if (Mouse.isPressed(MOUSE_LEFT)) {
            Mouse.release(MOUSE_LEFT);
        }
    }

    if (digitalRead(RBUT) == LOW) {
        if (!Mouse.isPressed(MOUSE_RIGHT)) {
            Mouse.press(MOUSE_RIGHT);
        }
    }
    else {
        if (Mouse.isPressed(MOUSE_RIGHT)) {
            Mouse.release(MOUSE_RIGHT);
        }
    }

    delay(20);
}
```

* * *

[1](#part0011_split_000.html_nf1)Or “tactile switches”.

# Project 6 – Making a Translating Keyboard

The Arduino Yún has the ability to act as a USB keyboard. This project builds a proof-of-concept device that: reads from a USB keyboard that you plug into the Yún; sends key presses to the PC; and translates sentences and paragraphs from English to one of three foreign languages.

When you connect an Arduino Yún to a computer using a micro-USB cable, the ATmega32u4 reports that the Yún contains a serial port, a mouse, and a keyboard. When this project reads a key press from an external keyboard, it sends the information to the PC. When you press the Enter key, or a push button, the Arduino sketch translates the text and then resends it to your computer.

To translate text, you can use Microsoft’s Translator web service. However, accessing this service is complicated on the Yún. Temboo is a web service that simplifies how you can work with other, more-complicated web services.

To complete this project, you need:

1.  An Arduino Yún, connected to the Internet over Ethernet or Wi-Fi.
2.  A microSD card, with the OpenWrt-Yun file system expanded onto it. For more information, see [Expanding the Linux File System onto the microSD Card](#part0005_split_005.html_tc2s6).
3.  A USB to micro-USB cable.
4.  A USB keyboard.
5.  One common-cathode RGB light-emitting diode (LED).
6.  One 330 Ω resistor.
7.  One 10 kΩ resistor.
8.  A momentary push button.
9.  One 4-way rotary switch.
10.  A solderless breadboard and jumper wires.

In This Chapter

[Hosting a USB Keyboard](#part0012_split_000.html_tp6s1)

[Translating with Temboo and Microsoft Translator](#part0012_split_001.html_tp6s2)

[Building the Circuit and Finishing the Sketch](#part0012_split_002.html_tp6s3)

[Source Code – Sketch](#part0012_split_003.html_tp6s4)

[Source Code – Python](#part0012_split_004.html_tp6s5)

* * *

## Hosting a USB Keyboard

OpenWrt-Yun knows how to work with many USB devices. You do not have to write support for keyboard devices yourself, but you do need to install a small module.

1.  At the OpenWrt-Yun command prompt, type the following command and then press **Enter**:

    ```
    opkg update
    ```

2.  Type the following command and then press **Enter**:

    ```
    opkg install kmod-usb-hid
    ```

To begin this project, connect the Arduino to your PC using a micro-USB cable. Then plug a USB keyboard into the vertically-mounted USB socket on the Arduino Yún.

At the OpenWrt-Yun command prompt, run the following command:

```
lsusb
```

If the USB keyboard on the Yún is working, you should see the device in the list.

Type the following command and then press the Enter key:

```
ls /dev/input/
```

You should see a file called “event1”. If your keyboard contains extra buttons, such as multimedia controls (play, stop, and so on), then you may also see an additional entry called “event2”. */dev/input/event1* usually reports the key presses from the standard keys, and */dev/input/event2* reports the key presses of the additional buttons.

When you connect a USB keyboard to the Arduino Yún, OpenWrt-Yun creates virtual files in */dev/input/*. These files communicate directly with keyboards and other input devices, and you can access them using the *File* class in the Arduino’s Bridge library.

Reading from the keyboard using the Bridge library is not always reliable over a long period of time. Instead, this project includes a Python script that uses the Python module *evdev* to read from the keyboard. The script passes this information to the ATmega32u4 using the Console. For more information about passing information between the Yún’s processors, see [Making a Console Connection](#part0007_split_004.html_tc4s5).

To install *evdev*,

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    cd /usr/lib/python2.7/
    ```

2.  Type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/download/evdev.tar.gz
    ```

3.  Type the following command and then press **Enter**:

    ```
    tar -zxvf evdev.tar.gz
    ```

4.  Type the following command and then press **Enter**:

    ```
    rm evdev.tar.gz
    ```

Make a new directory on the microSD card for this project, and move inside it. For example:

```
mkdir /mnt/sda1/P6 && cd /mnt/sda1/P6
```

Start a new Python file, call it *kbd.py* and save it into the project directory. Add the following code to the file:

```
#!/usr/bin/python
import socket, struct
from evdev import InputDevice

dev = InputDevice("/dev/input/event1")
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("localhost", 6571))

for event in dev.read_loop():
    s.send(struct.pack("HHI", event.type, event.code, event.value))
```

The *socket* module makes the Console connection between the AR9331 and the ATmega32u4.

*evdev* contains methods for working with Linux input events, those sent through */dev/input/*. To use it with a keyboard, you need to create an instance of the *InputDevice* class and point it at the device’s virtual file.

The method *read_loop()* continually reads from the input device and returns an *InputEvent* object. *InputEvent* is a Python version of the Linux object *input_event*:

```
struct input_event {
    struct timeval time;
    __u16 type;
    __u16 code;
    __s32 value;
};
```

This structure contains four properties:

| Property | Size | Description |
| --- | --- | --- |
| time | 8 bytes | The date and time when the event occurs. |
| type | 2 bytes | An unsigned 16-bit number that describes the event. Events from a keyboard have the value 0x0100. |
| code | 2 bytes | For keyboard events, this is the Linux key code that describes which key is pressed or released on the keyboard. |
| value | 4 bytes | A signed 32-bit number that further describes the event. For keyboard events, this can be one of the following values: 0x00000000 – a key is released 0x01000000 – a key is pressed 0x02000000 – a key is held (repeat message) |

For this project, you need to pass the event’s *type*, *code*, and *value* properties to the Arduino sketch. To do this, you can send them to the Console as a group of bytes.

The *struct* module contains methods for working with C-style struct data types. The *pack()* method converts a sequence of variables into an array of bytes. It accepts a string that describes the format of the output, followed by as many variables as you need to send.

Each character in the format string describes the type of variable that you want to pack into the output. In the script code, “HHI” puts two unsigned 16-bit (short) numbers and one signed 32-bit number into the output.

| Format | C Type | Python Type | Size |
| --- | --- | --- | --- |
| C | char | string of length 1 | 1 byte |
| b | signed char (byte) | integer | 1 byte |
| B | unsigned char (byte) | integer | 1 byte |
| ? | _Bool | bool | 1 byte |
| h | short | integer | 2 bytes |
| H | unsigned short | integer | 2 bytes |
| i | int | integer | 4 bytes |
| I | unsigned int | integer | 4 bytes |
| l | long | integer | 4 bytes |
| L | unsigned long | integer | 4 bytes |
| q | long long | integer | 8 bytes |
| Q | unsigned long long | integer | 8 bytes |
| f | float | float | 4 bytes |
| F | double | float | 8 bytes |

The Arduino sketch can read this information into a similar structure.

### Testing the Keyboard

Start a new sketch in the Arduino IDE, and include the following two *#include* directives:

```
#include <Bridge.h>
#include <Console.h>
```

And then add the following *#define* directives:

```
#define EV_KEY      0x0100
#define EV_RELEASED 0x00000000
#define EV_PRESSED  0x01000000
#define EV_REPEAT   0x02000000
```

To receive the information that *kbd.py* sends, you can use a *struct*. Add the following code to the sketch:

```
struct input_event {
    uint16_t type;
    uint16_t code;
    int32_t value;
};
struct input_event event;
```

This defines the structure and creates an instance of it – *event*.

Now declare the *Process* object that the sketch uses to start the Python script:

```
Process p;
```

In your sketch’s *setup()* function, add the following code:

```
Bridge.begin();
p.runShellCommand(F("killall kbd.py"));
p.runShellCommandAsynchronously(F("/mnt/sda1/P6/kbd.py"));
Console.begin();
while (!Console);
```

When the *kbd.py* script starts, it continues running until the AR9331 resets. If the sketch resets but the AR9331 does not, the existing script still runs. To ensure only one copy of the script runs at a time, this code starts the Linux command *killall* to terminate any existing copies of *kbd.py*.

The code then waits for the Python script to connect to the Console.

In your sketch’s *loop()*function, you need to wait until the Python script sends an input event. Then you can read the data into the *event* object.

Add the following code to *loop()*:

```
if (Console.available() >= sizeof(event)) {
    Console.readBytes((char *)&event, sizeof(event));
}
```

The ampersand in this example is the *address of* operator. It tells the C compiler to send the memory address of a variable, not the contents of a variable.

When the Console’s buffer contains enough bytes to fill the *event* object, the code reads the bytes from the Console and overwrites the memory that contains *event*.

Now *event.type* contains the type of event, *event.value* contains whether a key is pressed or released, and *event.code* contains a Linux key code.

Before you can send this key press information to the PC, you need to convert the Linux key code in *event.code* to an ASCII character (or one of the special keys defined in the Arduino’s standard library). The key codes from */dev/input/event1* are different to the values that you send through the Arduino Yún’s *Keyboard* methods.

To convert the values, you can use a combination of a lookup table and a *switch* statement. Add the following global arrays to your sketch, below the line that reads *Process p;*:

```
const uint8_t rq[] = {'q','w','e','r','t','y','u','i','o','p','[',']'};
const uint8_t ra[] = {'a','s','d','f','g','h','j','k','l',';','\'','`'};
const uint8_t rz[] = {'z','x','c','v','b','n','m',',','.','/'};
```

Tip: If you do not use a standard US keyboard, you may have to adjust this key map.

Then add the following function to your sketch:

```
uint8_t convertKey(uint16_t k) {
    uint8_t key = (k & 0xFF00) >> 8;
    switch (key) {
        case 1:
            return KEY_ESC;
        case 11:
            return '0';
        case 12:
            return '-';
        case 13:
            return '=';
        case 14:
            return KEY_BACKSPACE;
        case 15:
            return KEY_TAB;
        case 28:
            return KEY_RETURN;
        case 29:
            return KEY_LEFT_CTRL;
        case 42:
            return KEY_LEFT_SHIFT;
        case 43:
            return '\\';
        case 54:
            return KEY_RIGHT_SHIFT;
        case 56:
            return KEY_LEFT_ALT;
        case 57:
            return ' ';
        case 58:
            return KEY_CAPS_LOCK;
        case 87:
            return KEY_F11;
        case 88:
            return KEY_F12;
        case 96:
            return KEY_RETURN;
        case 97:
            return KEY_RIGHT_CTRL;
        case 100:
            return KEY_RIGHT_ALT;
        case 102:
            return KEY_HOME;
        case 103:
            return KEY_UP_ARROW;
        case 104:
            return KEY_PAGE_UP;
        case 105:
            return KEY_LEFT_ARROW;
        case 106:
            return KEY_RIGHT_ARROW;
        case 107:
            return KEY_END;
        case 108:
            return KEY_DOWN_ARROW;
        case 109:
            return KEY_PAGE_DOWN;
        case 110:
            return KEY_INSERT;
        case 111:
            return KEY_DELETE;
        case 125:
            return KEY_LEFT_GUI;
        case 127:
            return KEY_RIGHT_GUI;
        default:
            if ( (key >= 59) && (key <= 68) ) {
                return KEY_F1 + (key - 59);
            }
            else if ( (key >= 2) && (key <= 10) ) {
                return 49 + (key - 2);
            }
            else if (key == 11) {
                return '0';
            }
            else if ( (key >= 16) && (key <= 27) ) {
                return rq[key - 16];
            }
            else if ( (key >= 30) && (key <= 41) ) {
                return ra[key - 30];
            }
            else if ( (key >= 44) && (key <= 53) ) {
                return rz[key - 44];
            }
            else {
                return 0;
            }
    } 
}
```

In your sketch’s *loop()* function, add the following code on a new line underneath the line that reads *Console.readBytes((char *)&event, sizeof(event));*:

```
if (event.type == EV_KEY) {
    uint8_t k = convertKey(event.code);
    if ( (event.value == EV_PRESSED) && (k != 0) ) {
        Keyboard.press(k);
    }
    else if ( (event.value == EV_RELEASED) && (k != 0) ) {
        Keyboard.release(k);
    }
}
```

When you compile the Arduino sketch and upload it to the ATmega32u4, the Arduino IDE combines your sketch with some standard code. On the Arduino Yún, part of this code enables you to pass key press messages to the PC, as if the Yún is a keyboard.

The methods for doing this are in the *Keyboard* class. *Keyboard* contains the following methods:

| Method | Description |
| --- | --- |
| begin() | On the Yún, this method is not required. |
| end() | On the Yún, this method is not required. |
| press() | Sends a message to press the specified key. The parameter for this method is an ASCII character. |
| print() | Sends an ASCII character or string to the PC. |
| println() | Sends an ASCII character or string to the PC, and then sends a carriage return. |
| release() | Sends a message to release the specified key. The parameter for this method is an ASCII character. |
| releaseAll() | Sends a message to tell the PC that no keys are pressed. |
| write() | Sends a raw byte to the PC. |

Tip: To keep compatibility with other keyboard libraries and example code, the Yún’s *Keyboard* class includes the methods *begin()* and *end()*. However, these methods are empty on the Yún; you do not need to use them.

The difference between *Keyboard.print()* and *Keyboard.write()* is demonstrated in the sample below:

```
Keyboard.write(65); //Sends ASCII 'A'.
Keyboard.print(65); //Sends the ASCII character sequence '6', '5'.
```

In general, the *Keyboard* class can only send key presses and messages that are made from characters that are on a standard QWERTY keyboard.

Upload the sketch to your Arduino and connect the Yún to your computer using the micro-USB cable. After OpenWrt-Yun loads, press keys on the USB keyboard and they should appear on your PC.

* * *

## Translating with Temboo and Microsoft Translator

Temboo is a web service that you can connect to using your Arduino Yún. It simplifies the code that you need to write to connect to powerful web services from companies such as Google, Microsoft, Twitter, Facebook, and others.

Temboo’s service is free for up to 250 calls per month. Or you can upgrade your account, starting at $7 per month for a “Maker” account that supports 25,000 calls per month.

The Microsoft Translator application programming interface (API) is a machine-translation service that supports multiple languages. You use it by sending words to the API over the Internet, and then receive the translation as a response. This is not a free service. However, you can translate up to two million characters per month without paying anything. If you want to translate more than this, monthly subscriptions are available.

If you are not familiar with using web services, the Translator API seems complicated. With Temboo, you can access the API from an Arduino sketch, using simple classes and methods. The Temboo library is included with the Arduino IDE, and it contains code that handles the most-complicated aspects of working with web services and APIs.

### Signing Up to Temboo and Microsoft Translator

If you are not already a Temboo user, you need to create an account on their website and then register your project.

1.  Open a web browser and visit the following website: [http://www.temboo.com](http://www.temboo.com)
2.  In the **Let’s give your account a name** box, type a username for your account.
3.  In the **Your email address** box, type your email address.
4.  In the **Password** box, set a password that you want to use for this account.
5.  In the **Confirm password** box, type the same password again.
6.  Click the **I agree to the Temboo Terms** box.
7.  Click **Sign up**.
8.  Click **ACCOUNT**, and then click **Applications**.
9.  Click **New Application**.
10.  In the **APPLICATION** box, type *YunKeyboardTranslator*.
11.  Write down the **Key**, or copy and paste it somewhere for later. You need to send this value from your sketch to use Temboo.

If you have a Microsoft Xbox, or are a Windows 8 user, you probably already have a Microsoft account. If you do not:

*   Visit [http://signup.live.com](http://signup.live.com) and complete the registration process.

To use the Microsoft Translator, you need to add it to your Microsoft account:

1.  Visit [http://datamarket.azure.com/dataset/bing/microsofttranslator/](http://datamarket.azure.com/dataset/bing/microsofttranslator/)
2.  Next to **2,000,000 Characters/month**, click **SIGN UP**.
3.  Sign in to your Microsoft account.
4.  Click the box next to **I have read and agree to the above publisher's Offer Terms and Privacy Policy**.
5.  Click **SIGN UP**.
6.  Click **My Account**.
7.  In the **my account** menu, click **DEVELOPERS**.

Before you can use the Translator from an Arduino sketch, you need to register your project as an application:

1.  Click **Register**.
2.  In the **Client ID** box, type *YunKeyboardTranslator* followed by some random characters. You need to send this value from your sketch to use the service.
3.  In the **Name** box, type *Yun Keyboard Translator*.
4.  In the **Redirect URI** box, type in any web address. For example, *https://datamarket.azure.com*.
5.  Write down the **Client secret**, or copy and paste it somewhere for later. You need to send this value from your sketch to use the service.
6.  Click **CREATE**.

The identifier that you type into the *Client ID* box has to be unique. If anyone else tries to use the same identifier, Microsoft’s system rejects the entry.

### Storing the Key Presses

So far, the sketch passes key press information to the PC. However, it also needs to store text so that it can send the information to Temboo when you press the Enter key.

Add the following global variables to the sketch:

```
char buffer[512];
int buffer_len = 0;
int ctrl_held = 0;
String language = "ro";
```

The sketch uses the *buffer* array to hold key presses. The array needs to be long enough to store a reasonable number of characters, but not too long. The ATmega32u4 does not have a huge amount of memory.

*buffer_len* points to the next free slot in the array. When the sketch starts, the *buffer* array is empty and so *buffer_len* is zero.

When you hold the Ctrl key, Windows logo key, or Apple key, and then you press another key, the keyboard sends two key presses. The key press that occurs while holding these keys is usually a command, and so you do not want to store it in *buffer*. You use the variable *ctrl_held* to keep track of whether to store the key press in *buffer*.

*language* contains the ISO language code for the language that you want to translate text into. You use this in the next section of this chapter. If the sketch sets *language* to an empty string, *loop()* should not store key presses or translate text.

In your sketch’s *loop()* function, before the line that reads *Keyboard.press(k);*, add the following code:

```
if (language != "") {
    if (k == KEY_RETURN) {
        // add code to translate text buffer here.
    }
    else if ( (k == KEY_LEFT_CTRL) || (k == KEY_RIGHT_CTRL) || (k == KEY_LEFT_GUI) ) {
        ctrl_held = 1;
    }
}
```

This sets *ctrl_held* to *1* when you press either the left Ctrl key, the right Ctrl key, the Windows logo key, or the Apple key.

After the line that reads *Keyboard.press(k);*, add the following code:

```
if (language != "") {
    if (!ctrl_held) {
        if ( (k >= 32) && (k <= 126) ) {
            if (buffer_len <= 510) {
                buffer[buffer_len] = k;
                buffer_len++;
            }
            Keyboard.release(k);
        }
        else if (k == KEY_BACKSPACE) {
            buffer[buffer_len] = 0;
            buffer_len--;
            if (buffer_len < 0) {
                buffer_len = 0;
            }
        }
    }
}
```

To detect when you release either Ctrl key, and modify the value of *ctrl_held*, add the following code after the line that reads *else if ( (event.value == EV_RELEASED) && (k = 0) ) {*:

```
if ( (language != "") && ( (k == KEY_LEFT_CTRL) || (k == KEY_RIGHT_CTRL) || (k == KEY_LEFT_GUI) ) ) {
    ctrl_held = 0;
}
```

If a Ctrl key, Windows logo key, or Apple key is not pressed, the sketch checks whether the key press refers to a text character. If it does, the code adds the character to the *buffer* array and then increments the value in *buffer_len*.

If you press the Backspace key, the sketch deletes the last character in *buffer* by setting it to null (0). It also decrements the value in *buffer_len* so that the next key press replaces the previous one.

Tip: The code has to make sure that *buffer_len* is always a value in the range 0 through 510\. *buffer* only has space for 512 items, so a value outside of this range causes an error in the sketch. The final entry (511) in the array may need to be a null character (0) so it cannot contain a key press character.

In the code above, the call to *Keyboard.release()* is important. When you hold a key on the keyboard, the device sends an *EV_REPEAT* message after a set number of milliseconds. The sketch ignores these messages. However, because the key is still down, the operating system can decide to trigger a repeat message of its own, and it may insert the same character again. If you do not stop this, the text on your PC screen can be different from the text in *buffer*, and this makes the translation function unusable.

When you press the Enter key (*KEY_RETURN*), the sketch should run the translation and replace the on-screen text with the translated version. To do this, it needs to simulate Backspace key presses to delete the existing text. Then it translates the text using Temboo, and sends the new text to the PC.

Replace the comment *// add code to translate text here* with the following code:

```
if (buffer_len > 0) {
    for (int i = 0; i < buffer_len; i++) {
        Keyboard.write(KEY_BACKSPACE);
    }
    buffer[buffer_len] = 0;
    translate();
    buffer_len = 0;
}
```

This code deletes the existing text from your PC’s screen. It then ensures that the final character after the key press information is null (0). Many of the Arduino’s string functions rely on character sequences ending with a null.

Add an empty *translate()* function to the sketch:

```
void translate() {
}
```

If you upload this sketch to your Arduino and run it, the device passes key press information to the PC. When you press the Enter key, it deletes the text. In the next section of this chapter, you expand the *translate()*function to translate the words in *buffer* to another language, and then send this information to the PC.

Although the project does not translate text yet, it is now possible to see some of its limitations.

The device assumes that you are typing continuous paragraphs – for example, in a word processor or email. If you reposition the text cursor (using the cursor keys or mouse) and continue typing, the contents of *buffer* do not match what is on the screen. This problem also occurs if you change applications, or start a new document without pressing the Enter key.

To be reliable and easy to use, a commercial device would have to use custom driver software to respond to these situations.

### Translating Text from an Arduino Sketch

The Arduino IDE comes with a library – *Temboo.h* – that you can use to work with Temboo from your Arduino sketches. One of the advantages of this library is that the code for using Temboo is similar for all of the web services that you can connect to.

Add the following *#include* directive to the sketch:

```
#include <Temboo.h>
```

When you connect to Temboo, you need to send your Temboo and Microsoft account information. Underneath the *#define* directives in your sketch, add the following statements:

```
#define TEMBOO_ACCOUNT       F("Your Temboo username")
#define TEMBOO_APP_KEY_NAME  F("YunKeyboardTranslator")
#define TEMBOO_APP_KEY       F("Your registered application key")
#define MICROSOFT_ID         F("Your Microsoft Client ID")
#define MICROSOFT_KEY        F("Your Microsoft Azure application key")
```

Replace *Your Temboo username* and *Your registered application key* with the values that you receive from the Temboo website.

Replace *Your Microsoft Client ID* and *Your Microsoft Azure application key* with the values that you set on the Microsoft Azure website.

*#define* is a compiler instruction. It tells the Arduino’s C compiler to replace every instance of the first term with the second. For example, when you hit *Verify* or *Upload*, every time the compiler sees the phrase *TEMBOO_APP_KEY_NAME* in the source code, it uses the code *F(“YunKeyboardTranslator”)* instead.

Unlike a variable, a *#define* statement can contain code. Because the sketch uses a lot of memory, the statements above define data using the *F()* function. This ensures that the Arduino reads the strings directly from the read-only, program code space, instead of creating the strings in the limited amount of variable space on the ATmega32u4.

Each web service that you can use is called a “choreo”. You can find the details of these choreos (and example code that uses them) on the Temboo website.

For the Microsoft Translator choreo:

1.  Login to [http://www.temboo.com](http://www.temboo.com)
2.  Click **LIBRARY**.
3.  Under **CHOREOS**, click the arrow next to **Microsoft**.
4.  Click **Translator**.

To use a choreo from an Arduino sketch, you need to create an instance of the *TembooChoreo* class.

Add the following code to the *translate()* function in your sketch:

```
TembooChoreo TranslateChoreo;
TranslateChoreo.begin();
TranslateChoreo.setAccountName(TEMBOO_ACCOUNT);
TranslateChoreo.setAppKeyName(TEMBOO_APP_KEY_NAME);
TranslateChoreo.setAppKey(TEMBOO_APP_KEY);
```

To use the Microsoft Translator service, you need to tell the choreo to use it and then send your input parameters. Now, add the following code directly underneath the preceding lines:

```
TranslateChoreo.setChoreo(F("/Library/Microsoft/Translator/Translate"));
TranslateChoreo.addInput(F("ClientID"), MICROSOFT_ID);
TranslateChoreo.addInput(F("ClientSecret"), MICROSOFT_KEY);
TranslateChoreo.addInput(F("From"), F("en"));
TranslateChoreo.addInput(F("To"), language);
TranslateChoreo.addInput(F("Text"), buffer);
```

In addition to your Microsoft Azure account information, you need to send three parameters to control the translation:

| Parameter | Description |
| --- | --- |
| From | An ISO-631 language code that specifies the language that your text is in. |
| To | An ISO-631 language code that specifies the language that you want to translate your text to. |
| Text | The string that you want to translate. |

The code above translates your text into Romanian. In [Setting the Language Options](#part0012_split_003.html_tp6s3s2), you can see the other languages that you can translate text into.

To run the translation, add the following line:

```
TranslateChoreo.run();
```

When the Temboo request finishes, you can read the result like you do when reading from files or network connections. However, the result of a call to the Microsoft Translator returns several lines of information. For example:

```
ExpiresIn
600
NewAccessToken
http://schemas.xmlsoap.org/ws/2005/...
TranslatedText
Salut din arduinomeetslinux
HTTP_CODE
200
```

This project only captures the line after *TranslatedText*. To do this, the following code reads characters from the *TranslateChoreo* object and stores them in a string. The string only needs to be 14 characters in length, which is enough to hold the sequence “TranslatedText”.

Each time it reads a character, the code checks whether the string is 14 characters long. If it is, it removes the first character and continues. This means that the string only holds the last 14 characters of the choreo’s response. Then, if the string has the value “TranslatedText”, the code skips the next two characters because they represent the line break. Then it extracts all of the characters on the next line, which is the translated text.

Add the following code underneath *TranslateChoreo.run();*:

```
String response;
int rLen = 0;
while (TranslateChoreo.available()) {
    response.concat((char)TranslateChoreo.read());
    rLen++;
    if (rLen == 14) {
        if (response == F("TranslatedText")) {
            TranslateChoreo.read();
            TranslateChoreo.read();
            while (TranslateChoreo.available()) {
                uint8_t c = TranslateChoreo.read();
                if ( (c == '\n') || (c == '\r') ) {
                    break;
                }
                else {
                    Keyboard.write((char)c);
                }
            }
            break;
        }
        response = response.substring(1);
        rLen = 13;
    }
}
TranslateChoreo.close();
```

Tip: uint8_t is a data type that treats all numbers as unsigned 8-bit numbers. Certain foreign characters appear as negative numbers if you use a char.

You can upload this sketch to your Arduino and test it. However, there is a problem to fix before the code is usable.

The ASCII character set uses one byte for each character, and it contains the English alphabet, numbers, and standard punctuation marks. However, many other languages use characters and symbols that are not in the ASCII character set. For these languages, the output from the Microsoft Translator tool is in Unicode not ASCII. Unicode characters are actually a sequence of values – there are multiple bytes for each character.

However, the *Keyboard* class can only send ASCII keys to the PC.

On most operating systems, you can type alternate characters by holding the *Alt* key and then pressing a combination of other keys. But when you want to type a Unicode character, the process is slightly different.

To type Unicode hex strings on Microsoft Windows, you need to make a small change to the system registry:

1.  Press the **Windows logo key + R**.
2.  Type *regedit* and then press **Enter**.
3.  On Windows 7 and 8: in the **User Account Control** box, click **Yes**.
4.  Double-click **HKEY_CURRENT_USER**.
5.  Double-click **Control Panel**.
6.  Right-click **Input Method**, point to **New**, and then click **String Value**.
7.  Type *EnableHexNumpad* and then press **Enter**.
8.  Double-click **EnableHexNumpad**.
9.  In the **Value** data box, type *1*.
10.  Click **OK**.
11.  On the **File** menu, click **Exit**.
12.  Restart your PC.

Then, to type a Unicode character:

1.  Hold **Alt**.
2.  On the numeric keypad, type **+**.
3.  Type a 4-character, hexadecimal point code. For example: *c380*.
4.  Release **Alt**.

To type Unicode hex strings on Mac OS X, you need to enable the Unicode keyboard input in the System Preferences, then change the input source selector to Unicode Hex Input whenever you want to use this project. To set all of this up:

1.  On the **Apple** menu, click **System Preferences**.
2.  Click **Language & Text**.
3.  Click **Input Sources**.
4.  Under **Select input methods to use**, click the box next to **Unicode Hex Input**.
5.  On the menu bar, click the input source selector, and then click **Unicode Hex Input**.[1](#part0012_split_005.html_fn1)

Then, to type a Unicode character:

1.  Hold **Option** (**Alt**).
2.  Type a 4-character, hexadecimal point code. For example: *c380*.
3.  Release **Option** (**Alt**).

Most Linux distributions already support entering Unicode characters from the keyboard. To type a Unicode character on Linux:

1.  Hold **Ctrl + Shift**.
2.  Type **U**.
3.  Type a 4-character, hexadecimal point code. For example: *c380*.
4.  Release **Ctrl + Shift**.

In order to send foreign characters to the PC, the Arduino sketch needs to simulate the key combinations that your operating system uses.

The first step is to determine how many bytes are in the Unicode sequence. This project only supports languages that use a 2-byte or 3-byte sequence. If the first byte of a Unicode sequence is in the range 0xC2–0xDF, it is a 2-byte sequence and so there is one more byte to read. If the first byte is 0xE0–0xEF, it is 3-byte sequence and there are two more bytes to read.

Find the line in *translate()* that reads *Keyboard.write((char)c);* and replace it with:

```
if ( (c >= 0xC2) && (c < 0xE0) ) {
    writeUTF8PointCode(c, TranslateChoreo.read(), 0);
}
else if ( (c >= 0xE0) && (c < 0xF0) ) {
    uint8_t c2 = TranslateChoreo.read();
    uint8_t c3 = TranslateChoreo.read();
    writeUTF8PointCode(c, c2, c3);
} 
else {
    Keyboard.write((char)c);
}
```

The *writeUTF8PointCode()* function does not exist yet. It accepts the two or three bytes that form the Unicode sequence, and then converts that information into a key combination.

Add a placeholder for the function to your sketch:

```
void writeUTF8PointCode(uint8_t c1, uint8_t c2, uint8_t c3) {
}
```

It can be complicated to convert Unicode sequences to point code key combinations. As a demonstration of how awkward tasks can be sent to the Atheros AR9331, this project uses an additional Python script to convert the Unicode sequences into a string that represents the ASCII key combination that you need to press.

Later, you may want to redevelop this project and convert the sequences in the Arduino sketch instead of using Python. Calling the Python script for each character slows down the speed at which the Arduino sends translated text to the PC.

To create this Python script:

1.  Login to the OpenWrt-Yun command line.
2.  Move into your project directory. For example, type the following command and then press **Enter**:

    ```
    cd /mnt/sda1/P6
    ```

3.  Type the following command and then press **Enter**:

    ```
    nano utf8.py
    ```

4.  Add the following code to the file:

    ```
    #!/usr/bin/python
    import sys
    args = []
    for a in range(1, len(sys.argv)):
        args.append(int(sys.argv[a]))
    v = unicode("".join(map(chr, args)), "utf-8")
    try:
        print format(ord(v), '04x')
    except:
        print "0000"
    ```

5.  Press **Ctrl + X**.
6.  Press **Y** and then press **Enter**.

The script reads parameters from the command line. It converts each parameter to a number, combines them into a string, and then converts the string.

The result of the *unicode()* function is another Unicode string. You have to convert this to a number before you can print the result back to the command line as a hexadecimal character sequence.

The *writeUTF8PointCode()* function in your Arduino sketch needs to:

1.  Start the *utf8.py* script and pass in a Unicode sequence as command-line arguments.
2.  Read the hexadecimal string from the script.
3.  Send a message to the PC that tells it to hold **Alt** (or the key combination required to allow users to enter Unicode hex strings).
4.  Send the hexadecimal string.
5.  Send a message to the PC to tell it to release **Alt** (and any others).

To start the *utf8.py* script, *writeUTF8PointCode()* needs a *Process* object. Add the following line to the function:

```
Process cnv;
```

The next section of code is different for each operating system.

*   If you use Microsoft Windows, add the following code underneath the line that reads *Process cnv;*:

    ```
    Keyboard.press(KEY_LEFT_ALT);
    Keyboard.press(223);
    Keyboard.release(223);
    ```

*   If you use Mac OS X, add the following code underneath the line that reads *Process cnv;*:

    ```
    Keyboard.press(KEY_LEFT_ALT);
    ```

*   If you use Linux, add the following code underneath the line that reads *Process cnv;*:

    ```
    Keyboard.press(KEY_LEFT_CTRL);
    Keyboard.press(KEY_LEFT_SHIFT);
    keyboard.write('u');
    ```

Tip: *Keyboard.write()* cannot send keys from the numeric keypad. These keys are in the range 84–99\. To send these codes through the *Keyboard* class, you need to add 136.

Add the following lines to run the *utf8.py* script:

```
cnv.begin("/mnt/sda1/P6/utf8.py");
cnv.addParameter(String(c1));
cnv.addParameter(String(c2));
if ( ( c1 >= 0xE0) && (c1 < 0xF0) ) {
    cnv.addParameter(String(c3));
}
cnv.run();
```

Because *utf8.py* sends back the result as an ASCII character string, you can read each character from the *cnv* object and then call *Keyboard.write()*. The Python script sends at least one additional character (a carriage return), but the sketch must only read the first four characters. Add these lines:

```
for (int i = 0; i < 4; i++) {
    while (!cnv.available());
    Keyboard.write(cnv.read());
}
cnv.close();
```

Finally, *writeUTF8PointCode()* needs to release the held keys. This is different for each operating system.

*   If you use Microsoft Windows, add the following code:

    ```
    Keyboard.release(KEY_LEFT_ALT);
    ```

*   If you use Mac OS X, add the following code:

    ```
    Keyboard.release(KEY_LEFT_ALT);
    ```

*   If you use Linux, add the following code:

    ```
    Keyboard.release(KEY_LEFT_SHIFT);
    Keyboard.release(KEY_LEFT_CTRL);
    ```

The source code for this sketch is in [Source Code – Sketch](#part0012_split_003.html_tp6s4). To complete the project, you can add an RGB LED (to indicate the status and activity of the device) and a rotary switch (to choose between three different languages).

* * *

## Building the Circuit and Finishing the Sketch

This project uses a 4-way rotary switch. When you turn a rotary switch, it makes a connection between a pole (a pin) and one of four other pins. You can also buy rotary switches in versions that have multiple poles.

For example: a 3-pole, 4-way rotary switch has three sets of contacts. They commonly have the poles arranged in an inner ring, and they are labelled *A*, *B*, and *C*. An outer ring has twelve pins, numbered 1 through 12\. In the first position: *A* connects to pin 1; *B* connects to pin 5; and *C* connects to pin 9\. In the second position: *A* connects to pin 2; *B* connects to pin 6; and *C* connects to pin 10.

![](images/00021.jpeg) 

Figure 20\. Connecting the switches and LED

Unplug the power from your Arduino, and then build the circuit in Figure 20\. Then reconnect the Arduino to your PC using a micro-USB cable.

| Connect Arduino Pin | To |
| --- | --- |
| Digital pin 2 | Position 1 of the rotary switch. |
| Digital pin 3 | Position 2 of the rotary switch. |
| Digital pin 4 | Position 3 of the rotary switch. |
| Digital pin 5 | Position 4 of the rotary switch. |
| Digital pin 6 | One leg of the push button. |
| Digital pin 9 | Leg B of the RGB LED. |
| Digital pin 10 | Leg G of the RGB LED. |
| Digital pin 11 | Leg R of the RGB LED. |
| GND | The ground line on the solderless breadboard. |

In this project, the first position of the rotary switch turns off the automatic translation. The three other positions select the language that you want to translate to.

Each position of the rotary switch acts like a button. To prevent a short circuit, connect a 10 kΩ resistor between the switch’s pin A and ground.

Connect another 10 kΩ resistor between the other leg of the push button and ground.

A common-cathode RGB LED contains three LEDs – one red, one green, and one blue. It usually has four legs. The longest leg is usually the second one, and this is the cathode. Each LED in a common-cathode RGB LED shares the same connection to ground.

When using RGB LEDs, you need to add a current-limiting resistor to your circuit – the same as you do with normal LEDs. Connect a 330 Ω resistor between the cathode of the RGB LED and ground.

To control the brightness and color of the LED, you can use pulse-width modulation (PWM) to set the individual LEDs in the RGB LED. Depending on how bright each LED is, your eyes see a blend of the colors.

The Arduino sketch for this project uses the RGB LED to indicate the status of the sketch:

| Color | Description |
| --- | --- |
| Off | ATmega32u4 cannot connect to the AR9331 through the Bridge. |
| Flashing red | USB keyboard not found. |
| Dim green | Translate function is switched off. |
| Bright green | Translate function is busy. |
| Purple | Language 1 selected. |
| Blue | Language 2 selected. |
| Yellow | Language 3 selected. |

Underneath the existing *#define* statements, add the following lines:

```
#define LED_R       11
#define LED_G       10
#define LED_B       9
```

At the top of your *setup()* function, add the following code to set the Arduino’s digital pins to *OUTPUT* and ensure the LED is off:

```
pinMode(LED_R, OUTPUT);
pinMode(LED_G, OUTPUT);
pinMode(LED_B, OUTPUT);
digitalWrite(LED_R, LOW);
digitalWrite(LED_G, LOW);
digitalWrite(LED_B, LOW);
```

Underneath the line that reads *Console.begin();*, change *while (!Console);* to

```
while (!Console) {
    digitalWrite(LED_R, HIGH);
    delay(200);
    digitalWrite(LED_R, LOW);
    delay(200);
}
```

This flashes the RGB LED red while the ATmega32u4 waits for the *kbd.py* script to open the Console. If the light continues to flash red for a long time, it indicates that *kbd.py* is unable to find the USB keyboard. Try pressing the 32U4 RST button and running the *lsusb* command again.

To set an LED in the RGB LED to maximum brightness, you can use *digitalWrite()*. However, when you want to blend colors and reduce the brightness of the LED, you need to use *analogWrite()*.

### Reading the Position of a Rotary Switch

The four switches of the rotary switch connect to Arduino digital pins 2–5\. Add the following *#define* statements:

```
#define TRANS_OFF   2
#define TRANS_1     3
#define TRANS_2     4
#define TRANS_3     5
```

Tip: If the switch is backwards when you test the sketch, you can reverse the pin numbers in these *#define* statements – set *TRANS_OFF* to 5, and *TRANS_3* to 2.

In your sketch’s *setup()* function, add the following code:

```
pinMode(TRANS_OFF, INPUT);
digitalWrite(TRANS_OFF, HIGH);
pinMode(TRANS_1, INPUT);
digitalWrite(TRANS_1, HIGH);
pinMode(TRANS_2, INPUT);
digitalWrite(TRANS_2, HIGH);
pinMode(TRANS_3, INPUT);
digitalWrite(TRANS_3, HIGH);
```

The wiring of the circuit (see [Building the Circuit and Finishing the Sketch](#part0012_split_002.html_tp6s3)) means that one of the digital pins connects to ground (*LOW*) when you select a position on the rotary switch. To ensure that the Arduino’s digital pins never float, you enable the internal pull-up resistors using *digitalWrite()*.

When you read the position of the rotary switch, you need to change the color of the LED and the *language* variable that the *translate()* function uses.

The *loop()* function in the sketch is quite large, so add the code that checks the rotary switch to a new function:

```
void checkSwitches() {
    if (digitalRead(TRANS_OFF) == LOW) {
        language = "";
        buffer_len = 0;
        analogWrite(LED_R, 0);
        analogWrite(LED_G, 5);
        analogWrite(LED_B, 0);
    }
    else if (digitalRead(TRANS_1) == LOW) {
        language = "fr";
        analogWrite(LED_R, 175);
        analogWrite(LED_G, 0);
        analogWrite(LED_B, 128);
    }
    else if (digitalRead(TRANS_2) == LOW) {
        language = "ko";
        analogWrite(LED_R, 0);
        analogWrite(LED_G, 0);
        analogWrite(LED_B, 255);
    }
    else if (digitalRead(TRANS_3) == LOW) {
        language = "fi";
        analogWrite(LED_R, 175);
        analogWrite(LED_G, 255);
        analogWrite(LED_B, 0);
    }
}
```

The language options for this project are described in [Setting the Language Options](#part0012_split_003.html_tp6s3s2).

The code sets the color of the RGB LED to one of four settings – depending on the position of the rotary switch. The values for each LED should be in the range 0–255.

Tip: When choosing values for the RGB LED, setting colors to maximum strength (255) can make it difficult to blend them. Experiment to find the colors that you want.

*checkSwitches()* also resets the buffer (by setting *buffer_len* to zero) when you turn the rotary switch into the off position.

Add a call to *checkSwitches()* at the start of your sketch’s *loop()* function. For example:

```
void loop() {
    checkSwitches();
    if (Console.available >= sizeof(event)) {
```

When *translate()* runs, it should change the RGB LED to green. To do this, add the following code before the *TranslateChoreo.begin();* in the *translate()* function:

```
digitalWrite(LED_R, LOW);
digitalWrite(LED_G, HIGH);
digitalWrite(LED_B, LOW);
```

The push button in this project is intended for situations where you want to translate text, but do not want to press the Enter key.

To finish the sketch, add the code to enable the button:

1.  At the top of the sketch, add:

    ```
    #define BTN_1       6
    ```

2.  In your *setup()* function, add:

    ```
    pinMode(BTN_1, INPUT);
    digitalWrite(BTN_1, HIGH);
    ```

3.  At the bottom of *checkSwitches()*, add:

    ```
    if (digitalRead(BTN_1) == LOW) {
        if (buffer_len > 0) {
            for (int i=0; i<buffer_len; i++) {
                Keyboard.press(KEY_BACKSPACE);
                Keyboard.press(KEY_BACKSPACE);
            }
            buffer[buffer_len] = 0;
            translate();
            buffer_len = 0;
        }
    }
    ```

Because the *translate()* function takes time to complete, there is no need to debounce the button.

### Setting the Language Options

The potential values for *language* are a subset of the ISO-631 language codes that the Microsoft Translator web service supports. Because this project only supports 2-byte or 3-byte Unicode sequences, it limits some of your choices. The table below shows all of the languages that you can use in this project.

| Language | ISO-631 Code |
| --- | --- |
| Arabic | ar |
| Bosnian | bs-Latn |
| Bulgarian | bg |
| Catalan | ca |
| Chinese | zh-CHS |
| Croatian | hr |
| Czech | cz |
| Danish | da |
| Dutch | nl |
| English | en |
| Estonian | et |
| Finnish | fi |
| French | fr |
| German | de |
| Greek | el |
| Haitian | ht |
| Hebrew | he |
| Hindi | hi |
| Hungarian | hu |
| Indonesian | id |
| Italian | it |
| Japanese | ja |
| Korean | ko |
| Latvian | lv |
| Lithuanian | lt |
| Maltese | mt |
| Norwegian | no |
| Polish | pl |
| Portuguese | pt |
| Romanian | ro |
| Russian | ru |
| Serbian | sr-Latn |
| Slovak | sk |
| Slovene | sl |
| Spanish | es |
| Swedish | sv |
| Thai | th |
| Turkish | tr |
| Ukrainian | uk |
| Urdu | ur |
| Vietnamese | vi |
| Welsh | cy |

* * *

## Source Code – Sketch

This code includes all of the lines that are specific to the different operating systems. At the top of the source code, there is a *#define* instruction:

```
#define WINDOWS
```

You should only define one of the following values: *WINDOWS*, *LINUX*, or *MAC_OS_X*.

In the code for the *writeUTF8PointCode()* function, there are *#ifdef* and *#endif* statements. For example:

```
#ifdef WINDOWS
    Keyboard.press(KEY_LEFT_ALT);
    Keyboard.press(223);
    Keyboard.release(223);
#endif
```

An *#ifdef* instruction tells the Arduino C compiler to check whether a value is defined using the *#define* directive. If the value is not defined, the compiler removes lines of code from the file until it sees an *#endif* instruction.

Tip: This is not the same as using an *if* statement. An *if* statement runs code if a condition is *true*. The actual code block is uploaded to the Arduino, but does not run if the condition is *false*. With an *#ifdef* statement, if the value is not defined then the C compiler does not compile that part of the code, and it does not upload it to the Arduino.

```
#include <Bridge.h>
#include <Console.h>
#include <Temboo.h>

#define WINDOWS

#define EV_KEY        0x0100
#define EV_RELEASED   0x00000000
#define EV_PRESSED    0x01000000
#define EV_REPEAT     0x02000000

#define TEMBOO_ACCOUNT       F("Your Temboo username")
#define TEMBOO_APP_KEY_NAME  F("YunKeyboardTranslator")
#define TEMBOO_APP_KEY       F("Your registered application key")
#define MICROSOFT_ID         F("Your Microsoft Client ID")
#define MICROSOFT_KEY        F("Your Microsoft Azure application key")

#define LED_R          11
#define LED_G          10
#define LED_B          9

#define TRANS_OFF      2
#define TRANS_1        3
#define TRANS_2        4
#define TRANS_3        5

#define BTN_1          6

struct input_event {
  uint16_t type;
  uint16_t code;
  int32_t value;
};
struct input_event event;

Process p;
const uint8_t rq[] = {'q','w','e','r','t','y','u','i','o','p','[',']'};
const uint8_t ra[] = {'a','s','d','f','g','h','j','k','l',';','\'','`'};
const uint8_t rz[] = {'z', 'x', 'c', 'v', 'b', 'n', 'm',',','.','/'};
char buffer[512];
int buffer_len = 0;
int ctrl_held = 0;
String language = "ro";

void checkSwitches() {
  if (digitalRead(TRANS_OFF) == LOW) {
    language = "";
    buffer_len = 0;
    analogWrite(LED_R, 0);
    analogWrite(LED_G, 5);
    analogWrite(LED_B, 0);
  }
  else if (digitalRead(TRANS_1) == LOW) {
    language = "fr";
    analogWrite(LED_R, 175);
    analogWrite(LED_G, 0);
    analogWrite(LED_B, 128);
  }
  else if (digitalRead(TRANS_2) == LOW) {
    language = "ko";
    analogWrite(LED_R, 0);
    analogWrite(LED_G, 0);
    analogWrite(LED_B, 255);
  }
  else if (digitalRead(TRANS_3) == LOW) {
    language = "fi";
    analogWrite(LED_R, 175);
    analogWrite(LED_G, 255);
    analogWrite(LED_B, 0);
  }
  if (digitalRead(BTN_1) == LOW) {
    if (buffer_len > 0) {
      for (int i=0; i<buffer_len; i++) {
        Keyboard.write(KEY_BACKSPACE);
      }
      buffer[buffer_len] = 0;
      translate();
      buffer_len = 0;
    }
  }
}

uint8_t convertKey(uint16_t k) {
  uint8_t key = (k & 0xFF00) >> 8;
  switch (key) {
    case 1:
      return KEY_ESC;
    case 12:
      return '-';
    case 13:
      return '=';
    case 14:
      return KEY_BACKSPACE;
    case 15:
      return KEY_TAB;
    case 28:
      return KEY_RETURN;
    case 29:
      return KEY_LEFT_CTRL;
    case 42:
      return KEY_LEFT_SHIFT;
    case 43:
      return '\\';
    case 54:
      return KEY_RIGHT_SHIFT;
    case 56:
      return KEY_LEFT_ALT;
    case 57:
      return ' ';
    case 58:
      return KEY_CAPS_LOCK;
    case 87:
      return KEY_F11;
    case 88:
      return KEY_F12;
    case 96:
      return KEY_RETURN;
    case 97:
      return KEY_RIGHT_CTRL;
    case 100:
      return KEY_RIGHT_ALT;
    case 102:
      return KEY_HOME;
    case 103:
      return KEY_UP_ARROW;
    case 104:
      return KEY_PAGE_UP;
    case 105:
      return KEY_LEFT_ARROW;
    case 106:
      return KEY_RIGHT_ARROW;
    case 107:
      return KEY_END;
    case 108:
      return KEY_DOWN_ARROW;
    case 109:
      return KEY_PAGE_DOWN;
    case 110:
      return KEY_INSERT;
    case 111:
      return KEY_DELETE;
    case 125:
        return KEY_LEFT_GUI;
    case 127:
        return KEY_RIGHT_GUI;
    default:
      if ( (key >= 59) && (key <= 68) ) {
        return KEY_F1 + (key - 59);
      }
      else if ( (key >= 2) && (key <= 10) ) {
        return 49 + (key - 2);
      }
      else if (key == 11) {
          return '0';
      }
      else if ( (key >= 16) && (key <= 27) ) {
        return rq[key - 16];
      }
      else if ( (key >= 30) && (key <= 41) ) {
        return ra[key - 30];
      }
      else if ( (key >= 44) && (key <= 53) ) {
        return rz[key - 44];
      }
      else {
        return 0;
      }
  }
}

void translate() {
  TembooChoreo TranslateChoreo;

  digitalWrite(LED_R, LOW);
  digitalWrite(LED_G, HIGH);
  digitalWrite(LED_B, LOW);

  TranslateChoreo.begin();
  TranslateChoreo.setAccountName(TEMBOO_ACCOUNT);
  TranslateChoreo.setAppKeyName(TEMBOO_APP_KEY_NAME);
  TranslateChoreo.setAppKey(TEMBOO_APP_KEY);

  TranslateChoreo.setChoreo(F("/Library/Microsoft/Translator/Translate"));
  TranslateChoreo.addInput(F("ClientID"), MICROSOFT_ID);
  TranslateChoreo.addInput(F("ClientSecret"), MICROSOFT_KEY);
  TranslateChoreo.addInput(F("To"), language);
  TranslateChoreo.addInput(F("From"), F("en"));
  TranslateChoreo.addInput(F("Text"), buffer);

  TranslateChoreo.run();
  String response;
  int rLen = 0;
  while (TranslateChoreo.available()) {
    response.concat((char)TranslateChoreo.read());
    rLen++;
    if (rLen == 14) {
      if (response == F("TranslatedText")) {
        TranslateChoreo.read();
        TranslateChoreo.read();
        while (TranslateChoreo.available()) {
          uint8_t c = TranslateChoreo.read();
          if ( (c == '\n') || (c == '\r') ) {
            break;
          }
          else {
            if ( (c >= 0xC2) && (c < 0xE0) ) {
              writeUTF8PointCode(c, TranslateChoreo.read(), 0);
            }
            else if ( ( c >= 0xE0) && (c < 0xF0) ) {
              uint8_t c2 = TranslateChoreo.read();
              uint8_t c3 = TranslateChoreo.read();
              writeUTF8PointCode(c, c2, c3);
            }
            else {
              Keyboard.write((char)c);
            }
          }
        }
        break;
      }
      response = response.substring(1);
      rLen = 13;
    }
  }
  TranslateChoreo.close();
}

void writeUTF8PointCode(uint8_t c1, uint8_t c2, uint8_t c3) {
  Process cnv;

  #ifdef WINDOWS
    Keyboard.press(KEY_LEFT_ALT);
    Keyboard.press(223);
    Keyboard.release(223)
  #endif
  #ifdef LINUX
    Keyboard.press(KEY_LEFT_CTRL);
    Keyboard.press(KEY_LEFT_SHIFT);
    Keyboard.write('u');
  #endif
  #ifdef MAC_OS_X
    Keyboard.press(KEY_LEFT_ALT);
  #endif

  cnv.begin("/mnt/sda1/P6/utf8.py");
  cnv.addParameter(String(c1));
  cnv.addParameter(String(c2));
  if ( (c1 >= 0xE0) && (c1 < 0xF0) ) {
    cnv.addParameter(String(c3));
  }
  cnv.run();
  for (int i=0; i<4; i++) {
    while (!cnv.available());
    Keyboard.write(cnv.read());
  }
  cnv.close();

  #ifdef WINDOWS
    Keyboard.release(KEY_LEFT_ALT);
  #endif
  #ifdef LINUX
    Keyboard.release(KEY_LEFT_SHIFT);
    Keyboard.release(KEY_LEFT_CTRL);
  #endif
  #ifdef MAC_OS_X
    Keyboard.release(KEY_LEFT_ALT);
  #endif
}

void setup() {
  pinMode(LED_R, OUTPUT);
  pinMode(LED_G, OUTPUT);
  pinMode(LED_B, OUTPUT);
  digitalWrite(LED_R, LOW);
  digitalWrite(LED_B, LOW);
  digitalWrite(LED_G, LOW);

  pinMode(TRANS_OFF, INPUT);
  digitalWrite(TRANS_OFF, HIGH);
  pinMode(TRANS_1, INPUT);
  digitalWrite(TRANS_1, HIGH);
  pinMode(TRANS_2, INPUT);
  digitalWrite(TRANS_2, HIGH);
  pinMode(TRANS_3, INPUT);
  digitalWrite(TRANS_3, HIGH);

  pinMode(BTN_1, INPUT);
  digitalWrite(BTN_1, HIGH);

  Bridge.begin();
  p.runShellCommand(F("killall kbd.py"));
  p.runShellCommandAsynchronously(F("/mnt/sda1/P6/kbd.py"));
  Console.begin();
  while (!Console) {
    digitalWrite(LED_R, HIGH);
    delay(200);
    digitalWrite(LED_R, LOW);
    delay(200);
  }
}

void loop() {
  checkSwitches();
  if (Console.available() >= sizeof(event)) {
    Console.readBytes((char *)&event, sizeof(event));
    if (event.type == EV_KEY) {
      uint8_t k = convertKey(event.code);
      if ( (event.value == EV_PRESSED) && (k != 0) ) {
        if (language != "") {
          if (k == KEY_RETURN) {
              if (buffer_len > 0) {
                for (int i=0; i<buffer_len; i++) {
                  Keyboard.write(KEY_BACKSPACE);
                }
                buffer[buffer_len] = 0;
                translate();
                buffer_len = 0;
              }
          }
          else if ( (k == KEY_LEFT_CTRL) || (k == KEY_RIGHT_CTRL) || (k == KEY_LEFT_GUI) ) {
            ctrl_held = 1;
          }
        }
        Keyboard.press(k);
        if (language != "") {
          if (!ctrl_held) {
            if ( (k >= 32) && (k <= 126) ) {
              Keyboard.release(k);
              if (buffer_len <= 510) {
                buffer[buffer_len] = k;
                buffer_len++;
              }              
            }
            else if (k == KEY_BACKSPACE) {
              buffer[buffer_len] = 0;
              buffer_len--;
              if (buffer_len < 0) {
                buffer_len = 0;
              }
            }
          }
        }
      }
      else if ( (event.value == EV_RELEASED) && (k != 0) ) {
        if ( (language != "") && 
             ( (k == KEY_LEFT_CTRL) || (k == KEY_RIGHT_CTRL) || (k == KEY_LEFT_GUI) ) 
           ) {
          ctrl_held = 0;
        } 
        Keyboard.release(k);
      }
    }
  }
}
```

* * *

## Source Code – Python

There are two Python scripts in this project. Store both of them on the microSD card. For example, in */mnt/sda1/P6*.

### kbd.py

```
#!/usr/bin/python
import socket, struct
from evdev import InputDevice

dev = InputDevice("/dev/input/event1")
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("localhost", 6571))

for event in dev.read_loop():
    s.send(struct.pack("HHI", event.type, event.code, event.value))
```

### utf8.py

```
#!/usr/bin/python
import sys

args = []
for a in range(1, len(sys.argv)):
    args.append(int(sys.argv[a]))

v = unicode("".join(map(chr, args)), "utf-8")
```

```
try:
    print format(ord(v), '04x')
except:
    print "0000"
```

* * *

[1](#part0012_split_002.html_nf1)With the default settings, the input source selector in Mac OS X shows the national flag of the current input language.

# Project 7 – Controlling your Arduino Projects with Voice Commands

Voice recognition and voice control applications are increasing in popularity. Features like Apple’s Siri, Microsoft’s Cortana, and “OK Google” are changing the way people interact with their phones, games consoles, and multimedia devices.

Where a full set of buttons and switches is not practical (or not desired), voice control often provides a solution to the problem of making a user interface. In some cases, voice control is a significant benefit to people who are unable to use regular user interfaces.

This project demonstrates the steps for adding voice control to your Arduino Yún projects. It comprises an Arduino sketch that responds to a button and handles the digital pins, and a Python script that: records speech from a microphone; sends the audio to a web service that translates the voice into text; parses the text to decide what to do; and sends commands to the Arduino sketch.

The voice control aspect of this project has the nickname “Yuri”.

To complete this project, you need:

1.  An Arduino Yún, connected to the Internet over Ethernet or Wi-Fi.
2.  A microSD card, with the OpenWrt-Yun Linux file system expanded onto it. For more information, see [Expanding the Linux File System onto the microSD Card](#part0005_split_005.html_tc2s6).
3.  A USB audio interface (see below).
4.  A pair of desktop PC speakers, with a 3.5 mm stereo jack plug and their own power supply. Or a set of headphones with a 3.5 mm stereo jack plug.
5.  A desktop PC microphone with a 3.5 mm jack plug.
6.  One 10 kΩ resistor.
7.  A momentary push button.[1](#part0013_split_006.html_fn1)
8.  A solderless breadboard and jumper wires.

This project uses the audio interface from [Project 3 – Making an MP3 Jukebox](#part0009_split_000.html_tp3). If you do not have a USB audio interface that has a 3.5 mm microphone socket, you may need to buy a different interface. You can usually use small USB audio interface, such as the one shown in Figure 21.

![](images/00013.jpeg) 

Figure 12\. A basic USB audio interface

In This Chapter

[Building the Circuit and Installing the USB Device](#part0013_split_000.html_tp7s1)

[Recording from a Microphone](#part0013_split_001.html_tp7s2)

[Translating Speech to Text](#part0013_split_002.html_tp7s3)

[Translating Text to Speech](#part0013_split_003.html_tp7s4)

[Source Code – Sketch](#part0013_split_004.html_tp7s5)

[Source Code – Python](#part0013_split_005.html_tp7s6)

* * *

## Building the Circuit and Installing the USB Device

The circuit for this project uses a push switch. When you press the switch for around 1 second, the Arduino sketch plays a sound through the speakers to tell you that it is recording from the microphone. When the project detects a period of silence, it plays another sound to tell you that it is stopping.

You may wish to add a light-emitting diode (LED) to the circuit. If you want to use an RGB LED, you can refer to the information in Project 6 – Making a Translating Keyboard. For example, [Building the Circuit and Finishing the Sketch](#part0012_split_002.html_tp6s3) includes diagrams and code for controlling an RGB LED.

To begin:

1.  Unplug the power from your Arduino.
2.  Build the circuit in Figure 22.
3.  Plug a USB audio interface into the vertically-mounted USB socket on your Arduino Yún.
4.  Connect speakers to the audio interface.
5.  Connect a microphone to the audio interface.
6.  Reconnect the Arduino to its power supply.

![](images/00022.jpeg) 

Figure 22\. Connecting a button to the Arduino

The 10 kΩ resistor protects your Arduino from accidental damage. You can connect the button directly to the Arduino’s *GND* pin. But if you do this and accidently set digital pin 8 to a *HIGH* output, then pressing the button creates a short circuit that could damage the Arduino.

In the Arduino sketch, you enable the Arduino’s internal pull-up resistors on digital pin 8\. This means that reading from the pin with *digitalRead()* returns *LOW* when you press the button, and *HIGH* at all other times.

To work with the USB audio interface, you need to install additional files if you did not complete Project 3:

1.  Login to the OpenWrt-Yun command line.
2.  Type the following command and then press **Enter**:

    ```
    opkg update
    ```

3.  Type the following command and then press **Enter**:

    ```
    opkg install kmod-usb-audio
    ```

This project uses a program called “madplay” to play sound effects. To download and install madplay,

*   Type the following command and then press **Enter**:

    ```
    opkg install madplay
    ```

To begin writing the Python script that performs most of the work in this project,

1.  Create a directory for your project files. For example:

    ```
    mkdir /mnt/sda1/P7 && cd /mnt/sda1/P7
    ```

2.  Type the following command and then press **Enter**:

    ```
    nano yuri.py
    ```

3.  Add the following code to the file:

    ```
    #!/usr/bin/python
    import os
    os.system("madplay /mnt/sda1/P7/yuri-on.mp3")
    os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
    ```

4.  Press **Ctrl + X**.
5.  Press **Y** and then press **Enter**.
6.  Type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/download/yuri-off.mp3
    ```

7.  Type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/download/yuri-ok.mp3
    ```

8.  Type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/download/yuri-on.mp3
    ```

9.  To test the script, type the following command and then press **Enter**:

    ```
    ./yuri.py
    ```

You need to specify the full file path and file names of the MP3s in the Python script. When you run the script from the Arduino sketch, the current working directory is not your project folder.

To continue, open the Arduino IDE and create a new sketch.

At the top of the sketch, add these definitions:

```
#include <Bridge.h>
#define BTN_1       8
Process p;
```

And then in your sketch’s *setup()* function, add the following code to configure the digital pin for the button and to make a connection to the Bridge library:

```
pinMode(BTN_1, INPUT);
digitalWrite(BTN_1, HIGH);
Bridge.begin();
```

In your sketch’s *loop()* function, add the following code:

```
if (digitalRead(BTN_1) == LOW) {
    delay(750);
    if (digitalRead(BTN_1) == LOW) {
        p.runShellCommand("/mnt/sda1/P7/yuri.py");
        p.close();
    }
}
```

Upload this sketch to your Arduino and then hold down the button for about 1 second. The Arduino starts the Python script and plays the sound files.

Tip: The *runShellCommand()* method waits for the Python script to finish. For more information about starting Linux commands and Python scripts from an Arduino sketch, see .

* * *

## Recording from a Microphone

For this project, you record sound from the microphone to a wave file (*.wav*). However, you also need to analyze the data as you fetch it from the microphone – to determine when the user stops speaking.

Python has a module called “PyAudio”, which contains classes and methods that you can use for controlling audio devices. PyAudio relies on a library called “PortAudio”. This library is not available on the Arduino Yún OPKG repository.

You can download a version of PyAudio that does not rely on an external PortAudio library from this book’s companion website.

1.  At the command prompt, type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/download/pyaudio_0.2.8_ar71xx.ipk
    ```

2.  Type the following command and then press **Enter**:

    ```
    opkg install pyaudio_0.2.8_ar71xx.ipk
    ```

3.  Type the following command and then press **Enter**:

    ```
    rm pyaudio_0.2.8._ar71xx.ipk
    ```

### Recording to a Wave File

In this section, you can see how to record sound from the microphone and then save the information to a wave file. The wave file format usually has the file extension *.wav*. It is an audio file format created by Microsoft, and most operating systems and music players can play these files.

In the next section of this chapter, you will see how to send this audio information to a web service. The web service that you use in this project to convert speech to text, supports the following audio formats:

*   16-bit PCM WAV, single channel, 8 kHz sampling
*   16-bit PCM WAV, single channel, 16 kHz sampling
*   AMR (narrowband), 12.2 kb/s, 8 kHz sampling
*   AMR-WB (wideband), 12.65 kb/s, 16 kHz sampling
*   OGG, speex encoding, 8 kHz sampling
*   OGG, speex encoding, 16 kHz sampling
*   Raw, linear coding, 8kHz sampling
*   Raw, ulaw coding, 8kHz sampling
*   Raw, linear coding, 16 kHz sampling
*   Raw, ulaw coding, 16 kHz sampling

You do not need a high-quality, stereo signal to record voices. A mono (single-channel) recording with an 8 kHz sample rate is good enough.

Open the *yuri.py* script and add the following *import* directives:

```
import pyaudio
import wave
```

And then underneath these *import* directives, add:

```
audio = pyaudio.PyAudio()
```

To read audio data from the microphone, you need to open the device and specify the format in which you want to receive sound.

After the line that reads *os.system("madplay /mnt/sda1/P7/yuri-on.mp3")*, add the following code:

```
mic = audio.open(format=pyaudio.paInt16, channels=1, rate=8000, input=True, frames_per_buffer=1024)
frames = []
for i in range(0, int(8000 / 1024 * 5)):
    data = mic.read(512)
    frames.append(data)
```

The *open()* method opens the input stream of the audio device. Its parameters are described in the table below:

| Parameter | Description |
| --- | --- |
| format | To create a digital version of a sound wave, PyAudio reads the voltage level of the microphone many times per second. The *format* parameter sets the type of number to use. This can be *paInt8*, *paInt16*, *paInt32*, or *paInt64* for 8-bit, 16-bit, 32-bit, and 64-bit numbers. Larger numbers give higher quality, but create larger files. |
| channels | A mono sound file has one channel. A stereo signal has two channels. |
| rate | When you play a file, you convert the sampled numbers to a voltage and this moves a speaker. By quickly switching between these samples, you vibrate the air and recreate the sound. The more samples you take, the more accurate the recreation of the sound. *rate* is the number of samples per second. 8000 (8 kHz) is sufficient for voice, but you can use higher numbers to increase the quality of the recording. |
| frames_per_buffer | Reading from the microphone takes time. To help you make high-quality recordings, audio interfaces and software libraries use buffers. These buffers hold multiple frames (or samples) and only return data to your Python program when the buffer is full. This is much faster than trying to read each sample yourself. |

The *frames* list holds the sound data from the microphone. To fill this list, a *for* loop reads from the microphone a set number of times. If the sample rate is 8 kHz, the loop needs to read 8000 samples for each second of audio. The number of times the loop runs is the sample rate divided by the buffer size (since the buffer holds multiple samples), and then multiplied by the number of seconds of audio that you want to record.

To read from the microphone, the code uses the *read()* method and passes in the size of the buffer. It then adds the data to the *frames* list.

After the line that reads *os.system("madplay /mnt/sda1/P7/yuri-off.mp3")*, add the following code:

```
mic.stop_stream()
mic.close()
audio.terminate()
```

This code closes the microphone input and the audio interface.

The *wave* module contains classes and methods for reading and writing *.wav* files. After *audio.terminate()*, add the following lines:

```
wf = wave.open("/mnt/sda1/P7/data.wav", 'wb')
wf.setnchannels(1)
wf.setsampwidth(audio.get_sample_size(pyaudio.paInt16))
wf.setframerate(8000)
wf.writeframes(b''.join(frames))
wf.close()
```

You can find the documentation for the wave module at [http://docs.python.org/2/library/wave.html](http://docs.python.org/2/library/wave.html)

This code open a new *.wav* file and then sets the format to match the format of the audio data from the microphone. The *writeframes()* method stores data in the file, and the call to *join()* is just to convert the *frames* list into a binary array.

To test the code and record an audio file:

1.  Save the file and quit nano.
2.  Either press the button on the breadboard, or type the following command and then press **Enter**:

    ```
    ./yuri.py
    ```

3.  After the ‘on’ tone, speak into the microphone until the script plays the ‘off’ tone.

If you want to play the *data.wav* file, you need to install *aplay* from the *alsa-utils* package.

1.  Type the following command and then press **Enter**:

    ```
    opkg install alsa-utils
    ```

2.  Type the following command and then press **Enter**:

    ```
    aplay /mnt/sda1/P7/data.wav
    ```

If aplay is noisy or crackles, run the command again. aplay’s limitations and bugs are not a problem in the next stages of this project.

### Detecting when you Stop Speaking

5 seconds is not long enough to contain enough words for this project. To extend the script to record up to 1 minute of audio,

*   Replace the line that reads *for i in range(0, int(8000 / 1024 * 5)):* with the following code:

    ```
    for i in range(0, int(8000 / 1024 * 60)):
    ```

There are many ways to detect when a user stops speaking. This project uses a very basic method. This technique is not perfect, but it is a starting point from which you can develop more effective ways of detecting the end of the user’s speech.

The approach works by checking the volume level of the sound samples. If the volume level falls below a set level, there is silence and the script should break out of the loop.

Add a variable to the script, on a new line before *frames = []*:

```
threshold = 1000
```

Tip: Depending on the sensitivity of your microphone and the amount of background noise around you, you may have to adjust the value of this variable.

The Python module *audioop* contains methods that you can use to perform calculations on sound samples. Add it to the script:

```
import audioop
```

And add the *deque* collection:

```
from collections import deque
```

A *deque* collection is a type of list. When it reaches full capacity, if you add a new item to the end of the list then it removes the first item to make space. You can use this structure to store information about the last few seconds (or milliseconds) of audio from the microphone.

Below the line that reads *frames = []*, add the following code:

```
q = deque(maxlen=int(8000 / 1024))
```

This creates a *deque* that holds enough data for the last 1 second of audio.

Then, underneath the line that reads *frames.append(data)*, add the following code and indent it:

```
q.append(audioop.rms(data, 2))
if i > int(8000 / 1024 * 2):
    if sum([x > threshold for x in q]) <= 0:
        break
```

The *append()* method of a *deque* collection adds an item to the list (and removes the first item, if needed). In this example, you add the result of a call to *audioop.rms()* to the collection.

The *rms()* method calculates the root mean square (RMS) of the audio fragment. When working with audio and speakers, RMS is a measure of the signal’s overall strength or volume. The second argument, *2*, specifies that each sample in *data* is 2-bytes long (a 16-bit number).

You can find the full documentation for the audioop module at [http://docs.python.org/2/library/audioop.html](http://docs.python.org/2/library/audioop.html)

The code adds together every value in *q* that is greater than *threshold*. If the result is less than or equal to zero, then the script detects the silence and breaks out of the loop. This is one way of checking that every value in the last second of audio is above the threshold.

Tip: To prevent the script detecting silence when it first starts, the code checks that it records at least 2 seconds of audio before checking for silence.

Your Python script now records from the microphone until you stop speaking, or until the *.wav* file is 60-seconds long.

* * *

## Translating Speech to Text

To translate the audio information into a string of text, you can use a web service from AT&T. The AT&T Speech API includes methods for converting voice recordings into text strings, and also methods for converting a text string into a voice recording.

The AT&T APIs are not free. However, you can build this project with “Sandbox Access” and not pay anything. This plan allows you to build a device for your own testing, but you may not use for devices that are in production.

To sign up for the AT&T developer program and use the Speech API:

1.  Open a web browser and visit [http://developer.att.com/](http://developer.att.com/)
2.  Click **Get Started Free**.
3.  Click **Close**.
4.  Complete the form under **Account Information**, and then click **Join Program**.
5.  Check your email and follow the instructions to verify your account.
6.  On the **My Apps** page, click **Set Up New App**.
7.  In the **App Name** box, type a name for your application. For example, type *Yuri*.
8.  In the **Description** box, type a description for your project.
9.  Under **Select which APIs you want to enable for this App**, click the box next to **Speech – Speech To Text**.
10.  Click **Submit App**.
11.  Make a note of the **App Key**, and **App Secret**. You can copy and paste these values into a text document (or similar) for use in your Python script.

### Getting an OAuth Access Token

Before your script can send audio data to the API and receive a text response, the script needs to login to the AT&T API and collect an access token. The script then sends this token with all other calls to the API.

OAuth access tokens expire, and so this script fetches a new one every time that it runs.

To communicate with the AT&T server, your script needs to use secure sockets layer (SSL). To do this, install the Python SSL module.

1.  At the OpenWrt-Yun command prompt, type the following command and then press **Enter**:

    ```
    opkg update
    ```

2.  Type the following command and then press **Enter**:

    ```
    opkg install python-openssl
    ```

The AT&T Speech API returns information in JavaScript object notation (JSON) format. JSON is a technique for structuring your data into collections and objects and sending this information over the Internet. The Python *json* module contains methods for converting a JSON object into a Python object.

To continue the script:

1.  Open *yuri.py* in nano.
2.  Remove the line that reads *os.system("madplay /mnt/sda1/P7/yuri-off.mp3")*.
3.  Add the following *import* statements to the list at the beginning of the script:

    ```
    import urllib
    import urllib2
    import json
    ```

The *urllib2* module contains methods for fetching information from the web over hypertext transfer protocol (HTTP). However, there are a few useful methods in an older version of *urllib*, so you need to import that one too.

Underneath the *import* statements in your script, add:

```
APP_KEY = ""
APP_SECRET = ""
```

In the *APP_KEY* string, type (or paste) in your “App Key” from the AT&T website. In the *APP_SECRET* string, type (or paste) in your “App Secret” from the website.

To get an access token from the AT&T Speech API, you need to send your *App Key* and *App Secret* to the API method */oauth/v4/token*.

After the line *wf.close()*, add the following code:

```
token = {}
params = {"client_id" : APP_KEY,
          "client_secret" : APP_SECRET,
          "grant_type" : "client_credentials",
          "scope" : "SPEECH"}
tReq = urllib2.Request("https://api.att.com/oauth/v4/token", urllib.urlencode(params))
tReq.add_header("Accept", "application/json")
tReq.add_header("Content-Type", "application/x-www-form-urlencoded")
```

To use *urllib2*, you can create a *Request* object. This way, you can set all of the options and additional HTTP header information before you call *urlopen()* to send the request to the web server.

Most of the options for this are set by AT&T. The *add_header()* method adds an HTTP header with the specified name and value. In the next section, you can see an alternative way of adding some HTTP headers to your *Request* object.

You must convert the *params* dictionary into a format that you can send over HTTP. The *urlencode()* method converts a Python object to a “percent-encoded” string.

Starting on the next line, add the following code:

```
try:
    response = urllib2.urlopen(tReq)
    token = json.loads(response.read())
except:
    os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
    pass
```

When you send information over local networks and the Internet, there are many reasons why the request can fail. If one of these errors occurs, *urlopen()* throws an error message and this ends the Python script.

To stop the script from ending, you can use *try* and *except* statements. If the code indented underneath *try* generates an error, then the Python interpreter runs the code indented underneath *except*. If there is no error, the *except* code does not run.

In this project, if you cannot fetch the access token then the script plays a sound file and then does nothing until the script ends.

To convert the JSON string from the AT&T API into a dictionary, use the method *json.loads()*. The result is an dictionary that usually has the following items:

| Item | Description |
| --- | --- |
| access_token | An access code that you can use to call methods from the AT&T APIs. |
| expires_in | The number of seconds until *access_token* expires. This project does not reuse access tokens and so you can ignore this item. |
| refresh_token | Specifies an additional access code that you can use to refresh the *access_token*. This project does not reuse access tokens. |
| token_type | Always “bearer”. |

You can access these items as you do with any Python dictionary. For example, to print the *access_token*:

```
print token["access_token"]
```

On an un-indented line underneath the *pass* statement, add the following code:

```
if "access_token" in token:
    print token["access_token"]
    os.system("madplay /mnt/sda1/P7/yuri-ok.mp3")
```

If the previous code fails to retrieve an access token from the AT&T API then *token* is empty and does not have an item named “access_token”. If it does have an item named “access_token”, the script plays another MP3 to signal to the user that it is now processing the audio.

Before testing the script, you may want to add the following line to the end of the file:

```
os.remove("/mnt/sda1/P7/data.wav")
```

When the script ends, this deletes the audio file that you recorded.

Your script should now look like this:

```
#!/usr/bin/python
import audioop
import json
import os
import pyaudio
import urllib
import urllib2
import wave
from collections import deque

APP_KEY = "<<Your app key>>"
APP_SECRET = "<<Your app secret>>"

audio = pyaudio.PyAudio()

os.system("madplay /mnt/sda1/P7/yuri-on.mp3")

mic = audio.open(format=pyaudio.paInt16, channels=1, rate=8000, input=True, frames_per_buffer=1024)
threshold = 1000
frames = []
q = deque(maxlen=int(8000 / 1024))
for i in range(0, int(8000 / 1024 * 60)):
    data = mic.read(512)
    frames.append(data)
    q.append(audioop.rms(data, 2))
    if i > int(8000 / 1024 * 2):
        if sum([x > threshold for x in q]) <= 0:
            break

mic.stop_stream()
mic.close()
audio.terminate()

wf = wave.open("/mnt/sda1/P7/data.wav", 'wb')
wf.setnchannels(1)
wf.setsampwidth(audio.get_sample_size(pyaudio.paInt16))
wf.setframerate(8000)
wf.writeframes(b''.join(frames))
wf.close()

token = {}
params = {"client_id" : APP_KEY,
          "client_secret" : APP_SECRET,
          "grant_type" : "client_credentials",
          "scope" : "SPEECH"}
tReq = urllib2.Request("https://api.att.com/oauth/v4/token", urllib.urlencode(params))
tReq.add_header("Accept", "application/json")
tReq.add_header("Content-Type", "application/x-www-form-urlencoded")
try:
    response = urllib2.urlopen(tReq)
    token = json.loads(response.read())
except:
    os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
    pass

if "access_token" in token:
    print token["access_token"]
    os.system("madplay /mnt/sda1/P7/yuri-ok.mp3")

os.remove("/mnt/sda1/P7/data.wav")
```

Test the script to make sure that it receives and prints an access token, and that it plays the appropriate sound files.

### Sending the Wave File to AT&T and Reading the Response

To send the audio information to the AT&T Speech API, you need to:

1.  Define the HTTP headers.
2.  Read the *data.wav* file into a variable.
3.  Prepare a *Request* object.
4.  Send the request to the web server.
5.  Read the response.

Underneath the line that reads *os.system("madplay /mnt/sda1/P7/yuri-ok.mp3")*, add the following code and indent it so that it only runs if you have a valid access token.

```
hdrs = {"Authorization" : "Bearer " + token["access_token"],
        "Accept" : "application/json",
        "Content-Type" : "audio/wav"}
f = open("/mnt/sda1/P7/data.wav")
wav = f.read()
f.close()
sReq = urllib2.Request("https://api.att.com/speech/v3/speechToText",
                       data=wav,
                       headers=hdrs)
try:
    response = urllib2.urlopen(sReq)
    print response.read()
except:
    os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
```

In this code, you first define the HTTP headers in a Python dictionary. Then you read the entire contents of the *.wav* file into a variable. When you create the *Request* object, you can pass in both of these Python variables in and set up the request with one call.

Save the script and run it from the OpenWrt-Yun command line:

```
./yuri.py
```

Speak into the microphone and then stop. After a short delay, you should see the response text.

Replace the line *print response.read()* with:

```
vData = json.loads(response.read())
```

This converts the JSON response into a Python dictionary. The only item is “Recognition”. This too is a Python dictionary and there are lot of values in the *Recognition* dictionary. The table below shows the first level of objects inside the *Recognition* dictionary. Some of these items contain another dictionary or list.

| Item | Description |
| --- | --- |
| Status | Usually “OK” if the voice recognition is successful, or “Speech Not Recognized” if the API could not translate the *.wav* file to text. |
| Info | A Python dictionary that contains information about the conversion from speech to text, and about the audio file that you send to the API. |
| NBest | Contains information about the API’s best guess at the words that are spoken in the audio file. |
| ResponseId | An identifier that uniquely identifies this call to the API. |

You can access these items using the syntax shown below:

```
print vData["Recognition"]["Status"]
```

For information about all of the values and other dictionaries in a *Recognition* dictionary, see the AT&T Speech API documentation at [http://developer.att.com/apis/speech/docs#resources-speech-to-text](http://developer.att.com/apis/speech/docs#resources-speech-to-text)

To extract the text version of the audio file, you need to process the *NBest* dictionary. Because of the format of the JSON response, *NBest* is a list that contains only one item – another dictionary. This contains:

| Item | Description |
| --- | --- |
| Grade | A string that indicates how confident the AT&T API is that it accurately translated the speech to text. Can be: *accept* – the *Hypothesis* value is probably ok; *confirm* – the *Hypothesis* value may not be accurate; *reject* – the *Hypothesis* value is not accurate. This project ignores the *Grade* value. |
| Hypothesis | A string containing the transcription of the audio. |
| LanguageId | The ISO 639 language code and ISO 3166 country code that the API used to translate the spoken words to text. |
| ResultText | A version of *Hypothesis* that is adjusted for capitalization and some grammar issues. Can sometimes be more useful than *Hypothesis*. |
| Words | A list of each word in *ResultText*. |
| WordScores | A list of values that indicates how confident the AT&T API is in the accuracy of each word. |

To access the *Words* list, you can use the syntax:

```
print vData["Recognition"]["NBest"][0]["Words"]
```

Tip: While you write the code in the next section of this chapter, it can be useful to add *print vData["Recognition"]["NBest"][0]["ResultText"]* to your script. Then you can run the *yuri.py* script from the command line and see what the AT&T Speech API thinks that you say.

### Responding to Voice Commands

To build voice control into your project, you can process the response that you receive from the AT&T Speech API and then pass this information to your Arduino sketch.

This short example accepts the following commands:

*   Turn on <pin number>; or
*   Turn off <pin number>.

When the script receives one of these voice commands, it sends a message to the ATmega32u4 through the Mailbox. For example, when it receives “turn on thirteen” then it sends the Mailbox message “n13”. When it receives “turn off three” then it sends the Mailbox message “f3”.

Depending on your accent, the basic Speech API is often unable to work out the difference between words like “eight” and “ate”, or “two” and “too”. To implement voice control, you may have to convert common inaccuracies.

Tip: To improve the quality of the Speech API’s transcription, you can use the Speech To Text Custom methods of the API. Because of its complexity, this is not covered in this project. The Custom methods accept a file that describes grammar suggestions and other parameters that can resolve problems identifying the differences between words.

Add the following dictionary to the *yuri.py* script, underneath the *APP_SECRET*.

```
pins = {"one" : "1",
        "two" : "2",
        "to" : "2",
        "too" : "2",
        "three" : "3",
        "four" : "4",
        "for" : "4",
        "five" : "5",
        "six" : "6",
        "sex" : "6",
        "seven" : "7",
        "eight" : "8",
        "ate" : "8",
        "nine" : "9",
        "ten" : "10",
        "tan" : "10",
        "teen" : "10",
        "eleven" : "11",
        "twelve" : "12",
        "thirteen" : "13"}
```

Then define the following function:

```
def processCommand(words):
    processed = False
    if len(words) == 3:
        if words[0] == "turn":
            if words[1] == "on":
                client.mailbox("n" + pins[words[2]])
                processed = True
            elif words[1] == "off":
                client.mailbox("f" + pins[words[2]])
                processed = True
    if processed == False:
        os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
```

To use the Mailbox from Python, you need to import the *BridgeClient* module into your script. Underneath the line that reads *import wave*, add the following code:

```
import sys
sys.path.insert(0, "/usr/lib/python2.7/bridge/")
from bridgeclient import BridgeClient
```

And then add this line above *audio = pyaudio.PyAudio()*:

```
client = BridgeClient()
```

For more information about exchanging information between the Atheros AR9331 and the ATmega32u4 using the Mailbox, see [Using Mailbox and Sending Messages](#part0007_split_005.html_tc4s6).

Underneath the line that reads *vData = json.loads(response.read())*, add the following code:

```
if vData["Recognition"]["Status"] == "OK":
    processCommand(vData["Recognition"]["NBest"][0]["Hypothesis"].split(' '))
else:
    os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
```

Make sure you indent this code so that it is inside the *try* block.

Although *Words* is a list of the words in the response from the Speech API, it may also include punctuation marks and capital letters that you do not want for this project. Instead, the code splits *Hypothesis* into a list so that each word after a space is a new entry.

Save the script file.

To make the voice control work, your Arduino sketch needs to read the messages from the Mailbox, and then change a digital pin depending on the content of the message.

In the Arduino IDE, underneath the line that reads *#include <Bridge.h>*, add:

```
#include <Mailbox.h>
```

And then underneath the line that reads *Bridge.begin();*, add:

```
Mailbox.begin();
```

In your sketch’s *loop()* function, add the following code to the end of the loop:

```
if (Mailbox.messageAvailable()) {
    String message;
    Mailbox.readMessage(message);
    if (message.length() >= 2) {
        int pin = atoi(&message[1]);
        pinMode(pin, OUTPUT);
        if (message[0] == 'n') {
            digitalWrite(pin, HIGH);
        }
        else if (message[0] == 'f') {
            digitalWrite(pin, LOW);
        }
    }
}
```

Tip: *atoi()* is a C function that converts a string to an integer. The string must contain a number represented by ASCII characters. For example, “123”. Because the first character in *message* is either ‘n’ or ‘f’, you pass in the memory address of the second character in *message*, so that *atoi()* does not see the first character.

Upload the sketch to your Arduino and then press (and hold) the button. After the sound effect, say “turn on thirteen”. If the Speech API and Python script file recognize your command, the sketch turns on the Arduino Yún’s built-in LED. If the Speech API and Python script do not recognize your command, the script plays another sound.

To extend this project, you have to write code into *yuri.py* to understand new commands and pass these to the ATmega32u4\. Then modify your sketch to respond to the new commands.

* * *

## Translating Text to Speech

Because the project only supports turning Arduino digital pins on or off, the results are easy to see. For more complicated voice control, it can be useful to make the script speak back to the user.

The AT&T Speech API has a method for doing this. However, you can also do this using a Linux program that performs the translation without sending information across the Internet. The program that you need to install is called “espeak”.

If you have not installed the GCC compiler, you need to do so now.

1.  At the OpenWrt-Yun command prompt, type the following command and then press Enter:

    ```
    opkg update
    ```

2.  Type the following command and then press Enter:

    ```
    opkg install binutils
    ```

3.  Type the following command and then press Enter:

    ```
    opkg -t /root install yun-gcc
    ```

To install espeak,

1.  Type the following command and then press **Enter**:

    ```
    wget http://www.arduinomeetslinux.com/download/espeak_1.48.04_ar71xx.ipk
    ```

2.  Type the following command and then press **Enter**:

    ```
    opkg install espeak_1.48.04_ar71xx.ipk
    ```

3.  Type the following command and then press **Enter**:

    ```
    rm espeak_1.48.04_ar71xx.ipk
    ```

To test espeak from the command line,

*   Type the following command and then press **Enter**:

    ```
    espeak "Hello from Arduino Meets Linux."
    ```

The espeak program accepts command-line parameters that you can use to change how the program speaks your text. The following table shows a few of the most common options that you may need to use.

| Parameter | Description |
| --- | --- |
| a | Sets the volume. This is a number in the range 0 through 200\. The default setting is 100. |
| p | Sets the pitch. This is a number in the range 0 through 99\. The default setting is 50. |
| s | Sets the speed in words per minute. The default setting is 175\. There is no upper limit, but the lowest setting that you can use is 80. |
| m | Specifies that the text contains speech synthesis markup language (SSML). You can use SSML for more precise control of espeak’s pronunciation. |
| w | Writes the speech output to a wave file. |
| v | Selects a language and voice. The available English languages are:[2](#part0013_split_006.html_fn2)*en* – standard English *en-us* – American English *en-sc* – English with a Scottish accent *en-n* – English with a northern accent *en-rp* – Received Pronunciation (“BBC English”) *en-wm* – English with an accent from the West Midlands |

For a full description of all of the available options, see [http://espeak.sourceforge.net/commands.html](http://espeak.sourceforge.net/commands.html)

To set an option: put a dash before the parameter name, then a space, and then type the value for the option. To set more than option, separate each with a space. For example:

```
espeak -a 50 -v en -w /mnt/sda1/P7/test.wav "Hello"
```

There are an additional seven male voice variants, and five female voice variants. To use these, specify *+m1*, *+m2*, *+m3*, *+m4*, *+m5*, *+m6*, *+m7*, *+f1*, *+f2*, *+f3*, *+f4*, or +*f5* after the language.

```
espeak -v en-n+m3 "Hello"
```

Calling espeak directly can sometimes cause crackles and noise through the speakers. To ensure reliable audio, this project tells espeak to save the speech to a *.wav* file, and then the script plays the file through PyAudio.

In your Python script, above the line that declares *APP_KEY*, add the following Python class:

```
class AudioPlay:
    chunk = 1024

    def __init__(self, file):
        self.wf = wave.open(file, 'rb')
        self.p = pyaudio.PyAudio()
        self.stream = self.p.open(
            format =  self.p.get_format_from_width(self.wf.getsampwidth()),
            channels = self.wf.getnchannels(),
            rate = self.wf.getframerate(),
            output = True
            )

    def play(self):
        data = self.wf.readframes(self.chunk)
        while data != '':
            self.stream.write(data)
            data = self.wf.readframes(self.chunk)

    def close(self):
        self.stream.close()
        self.p.terminate()
```

You create an *AudioPlay* object by passing in the file name of the wave file that you want to play. The *play()* method plays the audio through your speakers or headphones, and the *close()* method closes the file and releases the audio device.

In your script, find the code that reads:

```
if vData["Recognition"]["Status"] == "OK":
    processCommand(vData["Recognition"]["NBest"][0]["Hypothesis"].split(' '))
else:
    os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
```

And change it to:

```
if vData["Recognition"]["Status"] == "OK":
    processCommand(vData["Recognition"]["NBest"][0]["Hypothesis"].split(' '))
else:
    os.system('espeak -w /mnt/sda1/P7/tmp.wav "Sorry. I do not understand."')
    spk = AudioPlay("/mnt/sda1/P7/tmp.wav")
    spk.play()
    spk.close()
    os.remove("/mnt/sda1/P7/tmp.wav")
    os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
```

Then change the end of the *processCommand()* function so that it reads:

```
if processed == False:
    os.system('espeak -w /mnt/sda1/P7/tmp.wav "Sorry. I do not understand."')
    spk = AudioPlay("/mnt/sda1/P7/tmp.wav")
    spk.play()
    spk.close()
    os.remove("/mnt/sda1/P7/tmp.wav")
    os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
```

Save the file.

To run this code, press and hold the button on the circuit. Then, after the tone, either:

*   Stay silent; or
*   Say something that the *processCommand()* function does not understand.

### Reading from Sensors and Speaking the Result

Using speech to tell the user the value of an input can be very useful, particularly in projects that do not have a display. The process for doing this is:

1.  In your Arduino sketch, read the value of a sensor or input.
2.  Send this data to a Python script on the Atheros AR9331\. For more information about exchanging information between the ATmega32u4 and the Atheros AR9331, see [Using the Bridge Library](#part0007_split_000.html_tc4).
3.  Process the data and create a string of words.
4.  Convert the string to a *.wav* file, and then play it.

The following example uses the Adafruit MCP9808 temperature sensor from [Project 1 – Building a Web-Based Temperature Monitor](#part0008_split_002.html_tc5s3). If you have not completed that project, it is recommended that you do so now.

In particular, make sure you install the *SoftI2CMaster* library in your Arduino IDE. Then unplug the power from your Arduino and connect the Adafruit MCP9808 as shown in [Connecting the Adafruit MCP9808 Temperature Sensor to the Arduino](#part0008_split_003.html_tc5s3s1).

When you speak the command “tell me the temperature”, the example responds.

To modify your current Arduino sketch to support this,

1.  Add the following *#include* statement to the top of the sketch:

    ```
    #include <SoftI2CMaster.h>
    ```

2.  Create an instance of the *SoftI2CMaster* class as a global variable:

    ```
    SoftI2CMaster i2c = SoftI2CMaster(A3, A2);
    ```

3.  In your sketch’s *setup()* function, before the call to *Bridge.begin()*, add the following code:

    ```
    pinMode(A0, OUTPUT);
    digitalWrite(A0, HIGH);
    pinMode(A1, OUTPUT);
    digitalWrite(A1, LOW);
    ```

4.  Copy the *getTemperature()* function from [Source Code – Sketch](#part0008_split_003.html_tc5s3s4), and then paste it into your current sketch.
5.  In your sketch’s *loop()* function, add the following code to the end:

    ```
    Bridge.put("MCP9808_Temperature", String(getTemperature()));
    ```

These changes update the variable *MCP9808_Temperature* in the shared-storage memory that both the ATmega32u4 and the Atheros AR9331 can use.

In the *yuri.py* script, find the *processCommand()* function. Then add the following code after the second *processed = True* statement. Indent this code with four spaces, so that it joins onto the first *if* statement in the function.

```
elif len(words) == 4:
    if words[0] == "tell" and words[1] == "me" and words[2] == "the":
        if words[3] == "temperature":
            temp = (float(client.get("MCP9808_Temperature")) * 1.5) + 32
            speech = "The temperature is {0:.1f} degrees fahrenheit.".format(temp)
            os.system('espeak -w /mnt/sda1/P7/tmp.wav "' + speech + '"')
            spk = AudioPlay("/mnt/sda1/P7/tmp.wav")
            spk.play()
            spk.close()
            os.remove("/mnt/sda1/P7/tmp.wav")
            processed = True
```

To extend this example so that the Python script speaks the time when you say “tell me the time”, add the following code underneath the *processed = True* statement in the code above. Indent this code with 12 spaces, so that it joins onto the *if words[3] == "temperature"* statement.

```
elif words[3] == "time":
    speech = "The time is " + strftime("%I %M %p", gmtime())
    os.system('espeak -w /mnt/sda1/P7/tmp.wav "' + speech + '"')
    spk = AudioPlay("/mnt/sda1/P7/tmp.wav")
    spk.play()
    spk.close()
    os.remove("/mnt/sda1/P7/tmp.wav")
    processed = True
```

And add the following *import* statement to the list at the top of the script:

```
from time import gmtime, strftime
```

Save the file and then exit nano. You have reached the end of this project.

This project is only an example of how you can add voice control to your Arduino projects, but the steps for building a more complicated system are the same. As your code for handling the different voice commands grows larger, you may want to research how compilers and interpreters work. The techniques involved in writing compilers can help you process natural language.

* * *

## Source Code – Sketch

```
#include <Bridge.h>
#include <Mailbox.h>
#include <SoftI2CMaster.h>

#define BTN_1  8
Process p;
SoftI2CMaster i2c = SoftI2CMaster(A3, A2);

float getTemperature() {
    i2c.beginTransmission(0x18);
    i2c.send(0x05);
    i2c.endTransmission();

    i2c.requestFrom(0x18);
    uint16_t v = i2c.receive();
    v <<= 8;
    v |= i2c.receive();

    float temp = v & 0x0FFF;
    temp /= 16.0;
    if (v & 0x1000) {
        temp -= 256;
    }
    return temp;
}

void setup() {
    pinMode(BTN_1, INPUT);
    digitalWrite(BTN_1, HIGH);

    pinMode(A0, OUTPUT);
    digitalWrite(A0, HIGH);
    pinMode(A1, OUTPUT);
    digitalWrite(A1, LOW);

    Bridge.begin();
    Mailbox.begin();
}

void loop() {
    if (digitalRead(BTN_1) == LOW) {
        delay(750);
        if (digitalRead(BTN_1) == LOW) {
            p.runShellCommand("/mnt/sda1/P7/yuri.py");
        }
    }
```

```
 if (Mailbox.messageAvailable()) {
        String message;
        Mailbox.readMessage(message);
        if (message.length() >= 2) {
            int pin = atoi(&message[1]);
            pinMode(pin, OUTPUT);
            if (message[0] == 'n') {
              digitalWrite(pin, HIGH);
            }
            else if (message[0] == 'f') {
                 digitalWrite(pin, LOW);
            }
        }
    }
```

```
 Bridge.put("MCP9808_Temperature", String(getTemperature()));
}
```

* * *

## Source Code – Python

```
#!/usr/bin/python
import audioop
import json
import os
import pyaudio
import urllib
import urllib2
import wave
from collections import deque
from time import gmtime, strftime
import sys
sys.path.insert(0, "/usr/lib/python2.7/bridge/")
from bridgeclient import BridgeClient

class AudioPlay:
    chunk = 1024

    def __init__(self, file):
        self.wf = wave.open(file, 'rb')
        self.p = pyaudio.PyAudio()
        self.stream = self.p.open(
                      format = self.p.get_format_from_width(self.wf.getsampwidth()),
                      channels = self.wf.getnchannels(),
                      rate = self.wf.getframerate(),
                      output = True
                      )

    def play(self):
        data = self.wf.readframes(self.chunk)
        while data != '':
            self.stream.write(data)
            data = self.wf.readframes(self.chunk)

    def close(self):
        self.stream.close()
        self.p.terminate()

APP_KEY = "<<Your app key>>"
APP_SECRET = "<<Your app secret>>"

pins = {"one" : "1",
        "two" : "2",
        "to" : "2",
        "too" : "2",
        "three" : "3",
        "four" : "4",
        "for" : "4",
        "five" : "5",
        "six" : "6",
        "sex" : "6",
        "seven" : "7",
        "eight" : "8",
        "ate" : "8",
        "nine" : "9",
        "ten" : "10",
        "tan" : "10",
        "teen" : "10",
        "eleven" : "11",
        "twelve" : "12",
        "thirteen" : "13"}

def processCommand(words):
    processed = False
    if len(words) == 3:
        if words[0] == "turn":
            if words[1] == "on":
                client.mailbox("n" + pins[words[2]])
                processed = True
            elif words[1] == "off":
                client.mailbox("f" + pins[words[2]])
                processed = True
    elif len(words) == 4:
        if words[0] == "tell" and words[1] == "me" and words[2] == "the":
            if words[3] == "temperature":
                temp = (float(client.get("MCP9808_Temperature")) * 1.5) + 32
                speech = "The temperature is {0:.1f} degrees fahrenheit.".format(temp)
                os.system('espeak -w /mnt/sda1/P7/tmp.wav "' + speech + '"')
                spk = AudioPlay("/mnt/sda1/P7/tmp.wav")
                spk.play()
                spk.close()
                os.remove("/mnt/sda1/P7/tmp.wav")
                processed = True
            elif words[3] == "time":
                speech = "The time is " + strftime("%I %M %p", gmtime())
                os.system('espeak -w /mnt/sda1/P7/tmp.wav "' + speech + '"')
                spk = AudioPlay("/mnt/sda1/P7/tmp.wav")
                spk.play()
                spk.close()
                os.remove("/mnt/sda1/P7/tmp.wav")
                processed = True
    if processed == False:
        os.system('espeak -w /mnt/sda1/P7/tmp.wav "Sorry. I do not understand."')
        spk = AudioPlay("/mnt/sda1/P7/tmp.wav")
        spk.play()
        spk.close()
        os.remove("/mnt/sda1/P7/tmp.wav")
        os.system("madplay /mnt/sda1/P7/yuri-off.mp3")

client = BridgeClient()
audio = pyaudio.PyAudio()

os.system("madplay /mnt/sda1/P7/yuri-on.mp3")

mic = audio.open(format=pyaudio.paInt16, channels=1, rate=8000, input=True, frames_per_buffer=1024)
threshold = 1000
frames = []
q = deque(maxlen=int(8000 / 1024))
for i in range(0, int(8000 / 1024 * 60)):
    data = mic.read(512)
    frames.append(data)
    q.append(audioop.rms(data, 2))
    if i > int(8000 / 1024 * 2):
        if sum([x > threshold for x in q]) <= 0:
            break

mic.stop_stream()
mic.close()
audio.terminate()

wf = wave.open("/mnt/sda1/P7/data.wav", 'wb')
wf.setnchannels(1)
wf.setsampwidth(audio.get_sample_size(pyaudio.paInt16))
wf.setframerate(8000)
wf.writeframes(b''.join(frames))
wf.close()

token = {}
params = {"client_id" : APP_KEY,
          "client_secret" : APP_SECRET,
          "grant_type" : "client_credentials",
          "scope" : "SPEECH"}
tReq = urllib2.Request("https://api.att.com/oauth/v4/token",
                       urllib.urlencode(params))
tReq.add_header("Accept", "application/json")
tReq.add_header("Content-Type", "application/x-www-form-urlencoded")
try:
    response = urllib2.urlopen(tReq)
    token = json.loads(response.read())
except:
    os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
    pass

if "access_token" in token:
    print token["access_token"]
    os.system("madplay /mnt/sda1/P7/yuri-ok.mp3")
    hdrs = {"Authorization" : "Bearer " + token["access_token"],
            "Accept" : "application/json",
            "Content-Type" : "audio/wav"}
    f = open("/mnt/sda1/P7/data.wav")
    wav = f.read()
    f.close()
    sReq = urllib2.Request("https://api.att.com/speech/v3/speechToText",
                           data=wav,
                           headers=hdrs)
    try:
        response = urllib2.urlopen(sReq)
        vData = json.loads(response.read())
        if vData["Recognition"]["Status"] == "OK":
            processCommand(vData["Recognition"]["NBest"][0]["Hypothesis"].split(' '))
        else:
            os.system('espeak -w /mnt/sda1/P7/tmp.wav "Sorry. I do not understand."')
            spk = AudioPlay("/mnt/sda1/P7/tmp.wav")
            spk.play()
            spk.close()
            os.remove("/mnt/sda1/P7/tmp.wav")
            os.system("madplay /mnt/sda1/P7/yuri-off.mp3")
    except:
        os.system("madplay /mnt/sda1/P7/yuri-off.mp3")

os.remove("/mnt/sda1/P7/data.wav")
```

* * *

[1](#part0013_split_000.html_nf1)Or “tactile switch”.[2](#part0013_split_004.html_nf2)For more information about the languages that espeak supports, see http://espeak.sourceforge.net/languages.html

# Other Books by Bob Hammell

![](images/00023.jpeg)

The Arduino Ethernet Shield is a powerful device for connecting Arduinos to local area networks and to the Internet. But despite its popularity, few authors have attempted to explain how to use this shield to its full potential – leaving new users and less-experienced programmers to piece together fragments of information.

In Connecting Arduino: Programming and Networking with the Ethernet Shield, Bob Hammell guides the reader through the processes and key concepts involved in writing projects that use the Ethernet Shield. More than just a recipe book, this in-depth series of tutorials explores all aspects of the Ethernet library, and discusses how to work with Internet protocols such as HTTP and DNS. You don’t need a computer science degree to understand it, only a basic knowledge of how to write Arduino sketches.

For more information, see [www.connectingarduino.com](http://www.connectingarduino.com/)