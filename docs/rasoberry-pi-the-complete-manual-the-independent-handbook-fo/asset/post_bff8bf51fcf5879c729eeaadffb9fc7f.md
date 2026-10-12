
## Set up your Raspberry Pi

Learn what goes where in your brand new Raspberry Pi with our easy-to-follow guide

While it looks daunting, setting up the Raspberry Pi for day-to-day use is actually very simple. Like a TV or a normal computer, only certain cables will fit into the specific slots, and the main job really is making sure you've got plugged in what you need at any one time. The Raspberry Pi itself doesn't label much of the board. However, most good cases will do that for you anyway – if you decide to invest in one.

### Power adapter

The Raspberry Pi is powered using a micro USB cable much like a lot of modern Android phones. It can be powered off a laptop or computer. But to make the most out of it, a proper mains adapter – like this one – is ideal

### Monitor

The Raspberry Pi is capable of displaying a 1920 × 1080 output, otherwise known as 1080p. Some monitors missing an extra-way output to plug HDMI straight into them, just like TVs do. However you may need an adapter in some cases

### USB hub

There are only a limited number of USB ports on a Raspberry Pi (just one). If you have Model A, to get around this you will need a USB hub. It's important to get a powered one, as the Pi cannot supply enough juice on its own

### Case and accessories

A case is not necessary to use the Pi correctly, but a decent one can keep it well protected from dust, and make it easier to move while in operation. You will need an SD card, however, as a case-4GB

### Keyboard and mouse

Like any computer, you'll need a keyboard and mouse for any standard Pi. Right, regardless you do with the Raspberry Pi. The most basic the keyboard, the better, some with the mouse as some special ones need additional software.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_13_0.png)

## Getting started

### Set up your Raspberry Pi

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_14_0.png)

### Analogue output

For people that don’t (yet) have a 3.5mm jack: you can buy a small black 3.5mm (or 6.5mm) cable to pipe out the audio.

### USB

All the peripherals you want to connect via USB—USB hubs, keyboards, mouse, USB storage etc.—plug in here. If your hub has an external power for the USB hub you have to use one though.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_14_1.png)

### SD card

The SD card goes in underneath the Raspberry Pi board. This will hold your operating system that runs the Raspberry Pi. The Pi does not need to be set up from another computer before using it, though.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_14_2.png)

### Digital output

The HDMI port is the main video (and audio) output of the Raspberry Pi, allowing you to display videos on the TV/desktop at a resolution of up to 1080p. The Pi’s support for 3D will also appear in the audio out automatically through it.

### Networking

The Raspberry Pi does not come with wireless Internet, and while you can add a USB adapter, it’s usually easier to plug in an Ethernet cable. This will plug into the back of your router on the other end and give you internet and access to your home network.

### Cabling

Make sure you have the right selection of cables, such as an Ethernet cable for networking and a TV adapter, and an HDMI or Video cable for video out. The HDMI or Video cable is not included, and the video out will require an additional auxiliary cable.

## Getting started

### What you'll need...

- Raspberry Pi Zero
- Micro USB power supply
- Soldering iron and solder
- Pi Zero adapter bundle
  - Monitor, mouse and keyboard
  - USB Wi-Fi or USB Ethernet adaptor
- Optional
- USB hub
- Optional

### Set up your Pi Zero

Get to grips with your Raspberry Pi Zero, either as a headless device or for use together with a screen and keyboard.

So you've picked up one of the tiny yet powerful Zeros, but before the coding fun can begin you need to get more familiar with it. Don't worry; we'll walk you through the Raspberry Pi Zero, the required cables, how to prepare a NOOBS SD card, and how to solder the GPIO header onto the Pi. Once the Pi is working and booted we'll show you how to get it working on Wi-Fi through the Raspberry user interface. You'll need a USB hub for this, or even just use a keyboard and mouse together. We'll also show you how to prepare a Raspberry SD card for headless use (either VNC or SSH) with only a Wi-Fi adapter or USB-to-Ethernet adaptor.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_15_0.png)

#### Raspberry Pi Zero Cable Overview

**01** The Raspberry Pi Zero is very small, and as such cannot fit normal-sized USB and HDMI connectors to it. To use it you therefore need adaptors that break out micro USB into full-size USB and mini HDMI to full-size HDMI. You also need to be very careful when connecting the micro USB cables as the micro USB power cable will fit into the connector meant for USB data. It's easy to tell them apart though, as they're clearly labelled, and the USB data connector can be found between the HDMI and power connectors.

### Set up your Pi Zero

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_16_0.png)

Fig 1: Once you've soldered the header into place, your Pi Zero should resemble any other Raspberry Pi

#### GPIO header

- **02** Soldering your brand new Raspberry Pi Zero might seem like a scary prospect, at first, but it's not that difficult! What is difficult, however, is snapping off the correct number of GPIO header pins (40), as the kit supplies more than 40. It's also well worth noting at this point that it doesn't matter too much if you mess up and end up missing a couple of the bottom pins.

The kit we used with a soldering iron, stand, solder, sucker and some lead-free solder was £8 on Amazon. We managed to solder the GPIO pins using this kit no problem.

#### Soldering kits

- **03** Soldering irons are very cheap these days. If you are going to do a lot of soldering then it's probably worth getting a temperature-controlled one where you can change the tip. However,

#### Holding the GPIO headers in place

- **04** Before you can solder the GPIO headers, you need to be able to hold them in place. We recommend putting some blu-tack on either side of the pins for this. This also has the advantage that you can flip the Pi over and then use the blu-tack to keep it in place on a table while you are soldering. The blu-tack should just easily peel off once you are done.

#### Solder the GPIO headers

- **05** Here comes the bit you might have been dreading, but, don't worry! Make sure you have wet the sponge in the soldering iron holder, as you will need to wipe the iron on the sponge to keep the tip clean. If this is the first time your iron has been used, the heating element will probably give off a lot of smoke for the first few minutes, so don't worry if that happens. Still, be mindful of your safety and make sure you're not in a poorly-ventilated area - try not to breathe in any fumes. Once the iron is hot, apply some solder to the tip and wipe any excess solder on the sponge. Then start to solder the pins. For each pin, touch the tip of the iron on the bottom of the GPIO header and the metal contact on the Pi, then apply a very small amount of solder. Once the solder has flowed onto the pin and the metal contact, then you can remove the iron. If there is too much solder then you can reheat the solder and use the solder sucker to remove it. Take breaks when soldering the GPIO headers for a couple of reasons: 1) you don't want to overheat any components on the Pi, and 2) you can melt the plastic of the GPIO headers and that will allow the pin to fall through. Keep wiping the tip of the iron on the sponge to keep it clean throughout the soldering process. Make sure you unplug the iron and put it somewhere safe to cool down when you are finished.

### Getting started

#### GPIO

Desv you’ve soldered on a 2x20s male header, your GPIOs will work as usual. To the right, you can see the four unpopulated pins for video output and a reset switch

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_17_0.png)

#### Video

You’ll need a mini-HDMI-to-HDMI adaptor to use this audio/video port, although you can also use the RCA composite video output via the unpopulated pin

#### Data

The power port, on the right, is micro USB as usual. The data port beside it is now micro USB as well, however, so you’ll likely need a micro USB-to-USB adaptor.

### Prepare NOOBS SD Card

- **06** See www.raspberrypi.org/help/noobs-setup for more details. NOOBS requires an SD card formatted as FAT32. You then need to download the latest NOOBS image from https://downloads.raspberrypi.org/NOOBS_latest and then unzip it to the SD card. On Linux, the steps are as follows:
  - `sudo parted /dev/mmcblk0(parted)  mklabel msdos(parted)  mkpart primaryfat32  0% 100%(parted)  mkb1kp1  /dev/mmcblk0p1  cd /mntsudo mkfs.vfat /dev/mmcblk0p1cd /mntsudo mkdfsr pi cd pi sudo  unzip /dev/mmcblk0p1/piNOOBS_v_1_5_2.zip`
  - `sync`
  - `cd ..sudo umount pi`

### Boot NOOBS and install Raspbian

- **07** Connect your Pi Zero up as shown in the first step. The minimum you need connected for a NOOBS install is a monitor and a keyboard. However, a mouse and either an Ethernet adaptor or Wi-Fi adaptor are also very useful. Press Enter to select Raspiian and then press 1 to install. Then press Enter to agree. Once it’s finished it will say 'OS installed successfully'. Press OK and your Pi will reboot into Raspbian. Alternatively, if you don’t want to use NOOBS, you can flash Raspbian to an SD card in the usual manner. Raspbian will boot into a desktop environment by default

### Configure Wi-Fi

- **08** If you are using a USB-to-Ethernet adaptor then the Pi should already be connected to the internet. If you are using a Wi-Fi adaptor then you will need to configure it to connect to your wireless network. We are using an Edimax EW-7811UN, which works

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_17_1.png)

Perfectly with the Pi out of the box. Once at the Raspbian desktop in order to see the available wireless networks. Once you click on one it will ask you for the password. After that it should be associated. You can hover your mouse over the icon and see the networks that you are connected to

### Configure Wi-Fi from another machine

- **09** If you want to use the Pi Zero as a headless device with Wi-Fi then you can prepare an SD card using another Linux machine that will already be configured to connect to the correct Wi-Fi network. You have to mount the SD card and edit /etc/wpa_supplicant/wpa_supplicant.conf, which is the same file that is configured by the
