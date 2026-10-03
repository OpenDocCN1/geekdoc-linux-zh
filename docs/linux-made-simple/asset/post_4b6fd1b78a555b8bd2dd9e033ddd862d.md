
Overclocking opinions are divided; it does give better performance but at the cost of possibly shortened component life and unreliability if you push it too far, plus more heat to get rid of. Some CPUs are locked at a particular speed, so you need to make sure the processor you choose is able to be overclocked. You also need a suitable motherboard. They all offer some control over frequencies and voltages, but some motherboards are intended for overclockers and offer far more control – you’ll need to do your research carefully.

Building your own laptop is not a reasonable proposition, but you can still research the components to make sure you get what you need.

They have more fan connectors and some speed control for them. When choosing cooling fans, go for the largest you can fit. A larger fan shifts more air; fast spinning fans create more noise.

If noise is an issue, consider water cooling.

Overclocking used to be a specialist field that required you to buy and assemble various components then spend ages bleeding the system and performing leak tests (it may surprise you, but water and electronics do not mix well). Nowadays pre-built units are available where you bolt the radiator assembly to a suitable point on the case and clip the heat sink in place of the CPU fan. Some kits also include GPU coolers; as mentioned, gaming works them hard too. Water cooling is not only for gamers and overclockers, it can be used on a standard desktop system to reduce the noise. The loudest noise from such a setup comes from the hard drive stepper motors.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_53_0.png)

## Sealed systems

Assembling a desktop or server computer is a fairly straightforward task, creating your own laptop isn’t. While it’s possible to buy laptops piecemeal, it’s not the usual way of doing things. Still, much of what we have covered in this feature still applies. It is just as important to choose suitable components for a laptop; even more so really because you cannot simply swap them out if you don't like them. So it is a matter of finding a pre-built laptop within your budget that meets your requirements and then checking that everything will do what you want it to. The same applies if you are looking for a nettop to act as a media player.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_53_1.png)

Even with this four-year-old system, the CPU spends a lot of time doing nothing, but it’s nice to have the capacity.

## Installing an operating system

Once you have built your computer, you will need to install an operating system. We will not look at that here, the distro installers are well enough documented, but there are a couple of points to consider. New motherboards will use UEFI rather than the older BIOS. They may also have Secure Boot enabled. You will almost certainly need to turn this off in the firmware. Press the relevant key at boot to configure the firmware, the motherboard’s manual will tell you which it is (one of the joys of building your own computer is that you get a manual for your motherboard). You should be able to use UEFI to boot the computer, most distros now work with it, and it’s nicer to work with than the old MBR system. If you need to use MBR booting, there will be an option for this in the firmware menu. Some have a UEFI boot option that you can turn off, others have the cryptically named CSM (Compatibility Support Module) that has to be enabled for MBR booting. If you are building a Linux-only system, you can just boot from your favourite DVD and install. If you want to dual boot with Windows, you should install Windows first and then Linux. The Linux installer will pick up the Windows installation and set up a dual-boot menu, whereas the Windows installer would just trample over the Linux bootloader if you did things the other way round.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_53_2.png)

### 7 Graphic card

Fit your graphics card into the PCI-E x16 slot. Check its documentation to see if it needs an external power feed or whether it gets all the power it needs from the PCI slot. Fit any other PCI cards you may be using at the same time. Many new power supplies (PSU) offer modular cable systems, else adapters are available if your PSU is missing suitable connectors, but ensure it’s powerful enough.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_53_3.png)

### 8 Tidy cables, tidy mind

Keep your cables tidy, even if you don’t have a window in the case. Untidy cables will disrupt airflow and make life harder the next time you try to add or replace a component. If your case doesn’t have clips to hold cables out of the way, small cable ties do a very good job of it. You can also often feed cables behind the motherboard tray or inside the hard drive fixtures.

The same rules apply for choosing a suitable processor, graphic card, sound card and so on (although the use of the word 'card' here is not strictly correct, almost everything is on the motherboard). There are a couple of important differences: laptop hard drives tend to be slower than their desktop counterparts, making the speed advantage of an SSD even greater. Memory upgrade options are limited, so choose a device with plenty to start with and make sure that it has at least one free slot for expansion. Some laptops have only one slot so upgrading memory means throwing away what you have rather than adding to it.

If you have the option, try booting the laptop from a recent live CD, or a live distro on USB. System Rescue CD with the Alt kernel option gives a very recent kernel with the most up to date hardware support. Run $ ifconfig -a to see that both wired and wireless interfaces show up and use $ aplay to make sure the sound system works all the way from the given file to the speakers. Wireless interfaces can still be a problem with some laptops, but most have a mini-PCI slot these days, in which case you can try another card.

While the Intel vs AMD CPU war and the Nvidia vs AMD graphics war will continue to rage on, Intel provides excellent support for its components. If your laptop has both Intel graphics and wireless cards, it won't go far wrong and everything should just work with no need to install extra drivers. Now grab your favourite distro and enjoy the speed and freedom of Linux!

## Careful now

Building a PC isn't difficult, but some care is needed when working with electronic components. Prepare a large working area, clear of any clutter and with a non-conductive surface. Static electricity can kill electronic components, and it can build up on your body without you noticing, until you pick up a component and zap it. You can avoid this by earthing yourself to discharge and static build up. The simplest way to do this is to touch a grounded object, such as a central heating radiator or the kitchen sink before touching a component. You can also buy anti-static wrist straps that connect to a grounded point by flexible cable to keep you static free during your build. The computer you build will not have a warranty, but the individual components will. As long as the fault wasn't caused by damage while fitting them, any reputable vendor will replace them.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_54_0.png)

### 8 Testing, testing

Connect a monitor and keyboard and power up the computer. Hold down the relevant key that loads the BIOS/firmware menu and go straight to the system health page to make sure your CPU is running cool enough. Only then should you check that all of your memory and drives are recognised. Some motherboards may need a setting changed to make all memory visible, but your new PC is now built!

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_54_1.png)

## Install Linux on your new Chromebook

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_55_0.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_55_1.png)

For those who’ve bought a Chromebook and miss a full operating system, we’ll show you how to get an assortment of Linux distros up and running.

Chrome OS is brilliant – for the type of user the Chromebooks are generally aimed at, it does exactly what it needs to do. It is fast and easy to use – what more could you ask for? Well, after a while, you may find yourself missing some of the features associated with more traditional operating systems. But don’t fret, because help is at hand, in the form of Crouton.

Crouton is a set of programs that set up a chroot environment within Chrome OS, from which you can run a Linux OS, with Debian and Ubuntu currently supported. A chroot is not the same as a virtual machine – you are still running on the standard operating system, but within a new environment. This method has several key advantages: for example, it does not touch the existing OS installation, making reversal easy; it uses the Chrome OS drivers for video, wireless and other devices, so there are no compatibility issues; and it is written by the Chrome OS authors, so it should remain compatible with future updates.

> Jargon buster!

apt-get
The program used to install software packages on Debian, Ubuntu and other Linux distros.

The only real disadvantage of using Crouton is that there may be a slight performance hit, but you didn’t buy a Chromebook for its blazing speed anyway. Oh, and in case you’re interested, the name Crouton is a convoluted acronym (standing for ChRromium Os Universal chrooT EnvirONment) that was clearly thought up after the name.

Before you start installing other distros, it’s a good idea to create a rescue disk to restore your Chromebook should anything go awry. Even if you’re not installing another OS, this is a wise step, especially as it’s so simple – all you need is a USB stick or SD card of at least 2GB in capacity. Because of the cloud-based nature of Chrome OS, 2GB is enough, as you only need to back up the operating system – your data and settings are safe on Google’s servers. (See the ‘Recovery disks’ walkthrough on page 59 for details.)

## Shell shocked

When you’re ready, start downloading Crouton from http://goo.gl/fd3zc. This is a script that downloads and installs everything you need. You run it from a shell – yes, Chromebooks come with a shell. Press [Ctrl]+[Alt]+[T] to open the Crosh shell in a browser tab. This is a limited shell, but run shell to start a proper Bash shell. Crouton needs to know which distro you want to install; it calls these releases and selects them with the -r option. Then it needs to know the target environment you want to install. A target is a collection of software packages, such as a particular desktop. These two commands will list the options:

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_55_2.png)

LXDE running on a Chromebook, but Chrome OS is still there.
