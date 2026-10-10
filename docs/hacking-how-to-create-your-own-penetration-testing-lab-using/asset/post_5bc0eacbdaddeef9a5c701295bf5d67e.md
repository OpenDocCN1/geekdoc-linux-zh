
# HACKING:

*How to Create Your Own Penetration Testing Lab Using Kali Linux 2016 for Beginners*

**Gary Mitnick**

© 2016

No part of this book may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or by any information storage or retrieval system without prior written permission from the author or copyright holder except in the case of brief quotations embodied in reviews.

Although the author has exhaustively researched all sources to ensure the accuracy and completeness of the information contained in this book, we assume no responsibility for errors, inaccuracies, omissions, or any inconsistency herein. Any slights of people or organizations are unintentional. Reader should use their own judgment and/or consult a programming expert for specific applications to their individual needs.

## Table of Contents

- Introduction
- Pre-Flight check List
- BIOS Enable Virtualization
- Virtual Box + Extensions
- Building your Kali Virtual Machine
- Install Kali ISO
- Tweak your Kali VM
- Install Guest Additions
- Resources
- More Course Books

## Introduction

This guidebook is to help you get going with the “The Complete Ethical Hacking Series for beginners” by Gary Mitnick without buying any specialized equipment for penetration testing. As an introduction to penetration testing this will be all you need to get started. As you leave the beginner stages you will probably not be using a Virtual Machine (VM) for your testing purposes. It does not matter what the operating system of your host machine is, if you can get a Virtual Box up and running the steps are all the same. The reason I suggest a Virtual Machine for beginners is that if something goes awry you won’t lose your entire system. (This is safe)

> *This document was done independently with no connections to anyone. The intent is to speed up the Kali installation process in a Virtual Machine.*

Currently there are only 2 ways of obtaining this manuscript – through amazon and through our mailing list (for free). Regardless of how you obtained this copy I want to thank you and congratulate you for investing in yourself and your computer knowledge.

## Before you begin:

Working with what you already have is fine for the course, however not for real world pen testing outside of it. Most things will work, and by the way some things just WILL NOT.

*Note:* Does internal wireless meet the chip requirements? **STOP Warning:** A VM will show up in Kali as an Ethernet adapter eth0. You can’t do the wireless lectures without an external USB wireless card when using a Virtual Machine. To be redundant I did not say use the internal wireless card in a Virtual Machine. To be able to do the wireless lectures in a VM, do a search for USB wireless adapters for Kali Linux. Here are a couple of sites that talk about what to use:

- http://www.blackmoreops.com/2014/01/08/recommended-usb-wireless-cards-kali-linux/
- http://www.aircrack-ng.org/doku.php?id=compatibility_drivers
- http://www.wirelesshack.org/top-kali-linux-compatible-usb-adapters-dongles-2015.html

## More Course Books

![](img/5481504809e843668406e46c502c72ab_4_0.png)
https://www.amazon.com/dp/B013JB351K/

![](img/5481504809e843668406e46c502c72ab_4_1.png)
https://www.amazon.com/dp/B01M15T2GG/

## Pre-Flight check List

- Check for and update your BIOS, then Enable Virtualization in your BIOS.
- Check your disk space on your current operating system. You need 15% free for your system and then you need additional space for Virtual Box and Kali.

*This is important to CHECK before you begin.*

- Hyper-V *cannot* be used for this course. VMware can, but you should know how to use it.

*Note:* If you have enabled Hyper-V, you will have issues when trying to install Kali in Virtual Box and will not be able to see the 64Bit versions of Linux for Virtual Machines you can disable Hyper-V in Windows Features just uncheck anything Hyper-V and reboot your system.

- Check the version of your operating system. Is it 64 Bit or 32 Bit? All your downloads should match your system. *(64-bit program is not going to work on a 32-bit machines and vice-versa)*
- Download Virtual Box & Virtual Box extension - install both before creating your Kali Virtual Machine.

https://www.virtualbox.org/wiki/Downloads

- Download the Kali 2016 ISO from https://www.kali.org/downloads/ be sure you have a complete download (some security suites will block this) Before attaching your USB external Wireless card, be sure to get Kali up and working with Virtual Box extensions, guest additions and updates installed.

## BIOS Enable Virtualization

Enable Virtualization in the BIOS (if you do not you will not be able to see 64-bit editions and the installation may fail). Enter the BIOS during startup of your physical system. Each system is different so the key to press may be different for your system. I used a Dell laptop so I had to hit F2 on boot up to get into my BIOS. (google search for your system)

![](img/5481504809e843668406e46c502c72ab_6_0.png)

In this case Virtualization was under the Advanced Tab, you want to make sure that it is enabled **(MOST of the trouble with setting up a VM have been caused by skipping or not doing this part)** Once you have enabled Virtualization you want to save your changes and exit the BIOS. In some systems, it may not say Virtualization but instead say “VT-x”

![](img/5481504809e843668406e46c502c72ab_6_1.png)

Some systems may need to be powered down completely then restarted for this to take effect. You can check with your system manufacturer or google how to get into your BIOS. You can read about what the BIOS is at https://en.wikipedia.org/wiki/BIOS

## Virtual Box + Extensions

Install the Virtual Box and then install the Virtual Box Extensions. These are basic Windows programs just take the defaults for both Virtual Box & Virtual Box Extensions. If your host system is OS X or Linux, you need to do the same installs but with the Virtual Box editions that match your system. The steps for creating a Virtual Machine are the same.

To avoid any problems when in Windows choose right click & Run as Administrator option (even if you have administrative rights). Be sure you have the version that matches your system OS if you are not in Windows. All downloads can be found at [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

You also need to download Kali Linux 2016 ISO file from [https://www.kali.org/downloads/](https://www.kali.org/downloads/) pick the version that matches your system. Install based on your operating system. If you have a 64-bit system, then download the 64-bit versions & 32 bit just use the 32-bit options. If you do not have virtualization available only use the 32-bit downloads for your install.

![](img/5481504809e843668406e46c502c72ab_7_0.png)

In Windows Run as administrator when finished close and install VBox extensions.

![](img/5481504809e843668406e46c502c72ab_8_0.png)

![](img/5481504809e843668406e46c502c72ab_8_1.png)

## Building your Kali Virtual Machine

Start Virtual Box (I already have Kali installed here in another VM that’s why you see that icon there we will make a new VM here)

![](img/5481504809e843668406e46c502c72ab_9_0.png)

Click on “New”. This Starts the Creation of a new VM.

![](img/5481504809e843668406e46c502c72ab_10_0.png)

Give it a name like “Kali” or whatever you want it to be. Then click the drop-down menu by “type” and choose “Linux”

Then choose the “Debian 64bit” (if you have a 64-bit system, and virtualization is on in the BIOS (if you have 32bit system then Debian 32bit option) PRESS next

![](img/5481504809e843668406e46c502c72ab_11_0.png)

![](img/5481504809e843668406e46c502c72ab_11_1.png)

Set your memory size, my machine has 8gig available so I am giving the VM 2 gig. You can type in how much you want to give the VM. I chose 2048. This can be changed later if needed. (Don’t give it too little or it will be slow and too much your host system will be slow)
