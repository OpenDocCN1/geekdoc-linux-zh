![](images/cover.jpg)

![image](images/cover.jpg)

![image](images/IFC.jpg)

![image](images/title.jpg)

In easy steps is an imprint of In Easy Steps Limited

16 Hamilton Terrace **·** Holly Walk **·** Leamington Spa
Warwickshire **·** United Kingdom **·** CV32 4LY

[www.ineasysteps.com](http://www.ineasysteps.com)

Seventh Edition

Copyright © 2021 by In Easy Steps Limited. All rights reserved. No part of this book may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or by any information storage or retrieval system, without prior written permission from the publisher.

Notice of Liability

Every effort has been made to ensure that this book contains accurate and current information. However, In Easy Steps Limited and the author shall not be liable for any loss or damage suffered by readers as a result of any information contained herein.

Trademarks

All trademarks are acknowledged as belonging to their respective companies.

**contents**

[1 **Getting Started**](#chapter01.xhtml)

[Introducing Linux](#chapter01.xhtml_sec1)

[Choosing a Distro](#chapter01.xhtml_sec2)

[Providing Disk Space](#chapter01.xhtml_sec3)

[Creating Boot Media](#chapter01.xhtml_sec4)

[Starting a Live Session](#chapter01.xhtml_sec5)

[Beginning Installation](#chapter01.xhtml_sec6)

[Completing Installation](#chapter01.xhtml_sec7)

[Enabling Backups](#chapter01.xhtml_sec8)

[Summary](#chapter01.xhtml_sec9)

[2 **Exploring the Desktop**](#chapter02.xhtml)

[Meeting the Interface](#chapter02.xhtml_sec10)

[Configuring the Desktop](#chapter02.xhtml_sec11)

[Adding Desklets](#chapter02.xhtml_sec12)

[Adjusting the Taskbar](#chapter02.xhtml_sec13)

[Launching Apps](#chapter02.xhtml_sec14)

[Editing the Menu](#chapter02.xhtml_sec15)

[Installing Updates](#chapter02.xhtml_sec16)

[Closing the Desktop](#chapter02.xhtml_sec17)

[Summary](#chapter02.xhtml_sec18)

[3 **Setting Preferences**](#chapter03.xhtml)

[Configuring the Screensaver](#chapter03.xhtml_sec19)

[Managing Windows](#chapter03.xhtml_sec20)

[Personalizing Options](#chapter03.xhtml_sec21)

[Controlling Connections](#chapter03.xhtml_sec22)

[Adding Printers](#chapter03.xhtml_sec23)

[Pairing via Bluetooth](#chapter03.xhtml_sec24)

[Summary](#chapter03.xhtml_sec25)

[4 **Touring the File System**](#chapter04.xhtml)

[Meeting the Directory Tree](#chapter04.xhtml_sec26)

[Recognizing Directories](#chapter04.xhtml_sec27)

[Navigating with Nemo](#chapter04.xhtml_sec28)

[Handling Files](#chapter04.xhtml_sec29)

[Creating Shortcuts](#chapter04.xhtml_sec30)

[Locating Files](#chapter04.xhtml_sec31)

[Understanding Permissions](#chapter04.xhtml_sec32)

[Summary](#chapter04.xhtml_sec33)

[5 **Engaging the Internet**](#chapter05.xhtml)

[Browsing the Web](#chapter05.xhtml_sec34)

[Customizing Firefox](#chapter05.xhtml_sec35)

[Exchanging Email](#chapter05.xhtml_sec36)

[Chatting Online](#chapter05.xhtml_sec37)

[Downloading Content](#chapter05.xhtml_sec38)

[Getting More Apps](#chapter05.xhtml_sec39)

[Summary](#chapter05.xhtml_sec40)

[6 **Producing with Office**](#chapter06.xhtml)

[Creating Documents](#chapter06.xhtml_sec41)

[Exporting Documents](#chapter06.xhtml_sec42)

[Creating Spreadsheets](#chapter06.xhtml_sec43)

[Creating Presentations](#chapter06.xhtml_sec44)

[Creating Visualizations](#chapter06.xhtml_sec45)

[Running Macros](#chapter06.xhtml_sec46)

[Adding Interaction](#chapter06.xhtml_sec47)

[Handling Data](#chapter06.xhtml_sec48)

[Summary](#chapter06.xhtml_sec49)

[7 **Enjoying Media**](#chapter07.xhtml)

[Viewing Images](#chapter07.xhtml_sec50)

[Managing Photos](#chapter07.xhtml_sec51)

[Scanning Images](#chapter07.xhtml_sec52)

[Editing Images](#chapter07.xhtml_sec53)

[Watching Movies](#chapter07.xhtml_sec54)

[Playing Music](#chapter07.xhtml_sec55)

[Streaming TV](#chapter07.xhtml_sec56)

[Sharing Content](#chapter07.xhtml_sec57)

[Summary](#chapter07.xhtml_sec58)

[8 **Using Accessories**](#chapter08.xhtml)

[Writing Text](#chapter08.xhtml_sec59)

[Doing Calculations](#chapter08.xhtml_sec60)

[Managing Archives](#chapter08.xhtml_sec61)

[Taking Notes](#chapter08.xhtml_sec62)

[Grabbing Screenshots](#chapter08.xhtml_sec63)

[Reading Documents](#chapter08.xhtml_sec64)

[Summary](#chapter08.xhtml_sec65)

[9 **Commanding the Terminal**](#chapter09.xhtml)

[Invoking the Terminal](#chapter09.xhtml_sec66)

[Navigating at the Prompt](#chapter09.xhtml_sec67)

[Operating on Directories](#chapter09.xhtml_sec68)

[Managing Files](#chapter09.xhtml_sec69)

[Examining File Properties](#chapter09.xhtml_sec70)

[Comparing Files](#chapter09.xhtml_sec71)

[Finding Files](#chapter09.xhtml_sec72)

[Reading Text Files](#chapter09.xhtml_sec73)

[Writing Text Files](#chapter09.xhtml_sec74)

[Manipulating Text Content](#chapter09.xhtml_sec75)

[Matching Text Patterns](#chapter09.xhtml_sec76)

[Summary](#chapter09.xhtml_sec77)

[10 **Performing Operations**](#chapter10.xhtml)

[Becoming the Superuser](#chapter10.xhtml_sec78)

[Installing Packages](#chapter10.xhtml_sec79)

[Handling Archives](#chapter10.xhtml_sec80)

[Examining File Systems](#chapter10.xhtml_sec81)

[Working with Accounts](#chapter10.xhtml_sec82)

[Setting Access Permissions](#chapter10.xhtml_sec83)

[Controlling Processes](#chapter10.xhtml_sec84)

[Exploring the Network](#chapter10.xhtml_sec85)

[Printing from the Shell](#chapter10.xhtml_sec86)

[Evaluating Expressions](#chapter10.xhtml_sec87)

[Scripting the Shell](#chapter10.xhtml_sec88)

[Summary](#chapter10.xhtml_sec89)

![image](images/pg6_1.jpg)

Guess what? Wheels have been round for a really long time, and anybody who “reinvents” the new wheel is generally considered a crackpot. It turns out that “round” is simply a good form for a wheel to have. It may be boring, but it just tends to roll better than a square, and “hipness” has nothing what-so-ever to do with it.

**Linus Torvalds, creator of the Linux kernel**

1

**Getting Started**

***This chapter introduces the Linux operating system and describes a typical installation procedure.***

[**Introducing Linux**](#chapter01.xhtml_sec1)

[**Choosing a Distro**](#chapter01.xhtml_sec2)

[**Providing Disk Space**](#chapter01.xhtml_sec3)

[**Creating Boot Media**](#chapter01.xhtml_sec4)

[**Starting a Live Session**](#chapter01.xhtml_sec5)

[**Beginning Installation**](#chapter01.xhtml_sec6)

[**Completing Installation**](#chapter01.xhtml_sec7)

[**Enabling Backups**](#chapter01.xhtml_sec8)

[**Summary**](#chapter01.xhtml_sec9)

**Introducing Linux**

![image](images/pg8_1.jpg)

Linux is a computer operating system that can run on a variety of hardware including the popular Intel system found on most desktop computers. It is a modern derivation of the powerful Unix operating system that was introduced way back in 1969. In recent years, the popularity of Linux has increased dramatically as computer users have discovered its many benefits:

•Linux is released under the GNU Public License that ensures it can remain free to all users. It’s available as a free download on the internet, but you may have to pay a distribution charge if you prefer a copy on CD/DVD.

•Access to the source code of Linux is unrestricted and it may be changed. This has allowed thousands of programmers around the world to refine the code to improve performance.

•Linux is truly a multi-user, multi-tasking operating system that allows multiple users to simultaneously work with multiple applications without experiencing any traffic problems. Many of the world’s web servers run on Linux for this very reason.

•Linux is an extremely stable operating system – continuous uptimes of more than a year are not uncommon. It can be upgraded on the “fly” so it seldom needs a reboot.

•There are a large number of quality applications available to run on the Linux platform. These are comparable to commercial applications that run on other operating systems but, like Linux, these too are free of charge. For instance, the free LibreOffice suite offers similar functionality to the commercial Microsoft Office suite.

•With open-source software, an administrator can know exactly what a program can do and the security dangers it presents. An open-source application cannot secretly gather information about the user or send confidential information to third parties.

![image](images/hot.jpg)

Pronounce the name Linux with a short “i” – so it’s “li-nucks”, not “lie-nucks”.

![image](images/forget.jpg)

Many web servers are said to have a “LAMP” configuration – an acronym for **L**inux, **A**pache, **M**ySQL, **P**HP, which combines operating system, web server, database, and server-side scripting.

**The Evolution of Linux**

In 1983, a visionary programmer named Richard Stallman began a movement called the GNU Project. Its philosophy was that software should be free from restrictions against copying or modification in order to make better and more efficient programs. This inspired programmers around the world to create programs driven by efficiency rather than by financial incentive.

By 1991, the GNU Project had created a lot of software tools including the GNU C Compiler written by Stallman himself. At that time many of these tools were incorporated into a Unix-compatible operating system by a 21-year old student at the University of Helsinki. His name was Linus Torvalds and he named the operating system Linux (**Linu**s – Uni**x**).

Linux was made available for download on the internet so other programmers could test and tweak the source code, then return it to Linus Torvalds. After a period of enthusiastic development, Linux 1.0 was made available globally under the GNU General Public License, which ensured it would remain free.

Programmers were keen to explore Linux and soon found some amazing uses for it. In April 1996, researchers at Los Alamos National Laboratory used Linux to run 68 PCs as a single parallel processing machine to simulate atomic shock waves. At $150,000 this supercomputer cost just one-tenth the price of a comparable commercial machine. It reached a peak speed of 19 billion calculations per second, making it the 315th most powerful supercomputer in the world. It proved to be robust too – three months later it still didn’t have to be rebooted.

Linux continued to grow in popularity as a text-based operating system, while Windows became the dominant graphical desktop operating system. Recognizing that most PC users want the point-and-click convenience of a graphical environment, the Linux camp began to develop a system comparable to the Windows desktop.

From a handful of enthusiasts in 1991 to millions of users now – Linux has come of age. Today’s sleek K Desktop Environment (KDE) and the Gnome desktop environment now offer a user-friendly alternative for Windows users – Linux for the desktop!

![image](images/pg9_1.jpg)

This penguin is “Tux” – the happy Linux mascot.

![image](images/pg9_2.jpg)

The term “GNU” is a recursive acronym for **G**NU’s **N**ot **U**nix. Discover more about the GNU General Public License online at [gnu.org/licenses/gpl.html](http://www.gnu.org/licenses/gpl.html)

![image](images/pg9_3.jpg)

Discover more about the Gnome graphical desktop online at [gnome.org](http://www.gnome.org)

**Choosing a Distro**

At the very heart of Linux is a bunch of tried-and-tested compiled code called the “kernel”. The kernel provides the operating system with its core functionality, much like the engine in a car. It takes care of the basics, such as helping other programs access hardware and sharing your computer’s processor among various programs.

![image](images/pg10_1.jpg)

In addition to the kernel, Linux contains a number of system-level programs, such as the services to handle your email, web connection and bootloader. Consider these as a car’s transmission, gears, and chassis – without these, the engine is not much use.

Linux distributions generally also include a large number of user-level programs – the applications for daily use: for instance, web browsers, word processors, text editors, graphics editors, media players, and so on. These are the finishing touches to the car that ensure a great ride – whitewall tires and soft leather upholstery.

All of these components are bundled together in a wide variety of Linux distribution packages, commonly referred to as “distros” – just as all the components of a car are bundled together to make a complete car.

![image](images/hot.jpg)

Most Linux distros are available as a “live” version that lets you run Linux from a disk – so you can try it out without installing Linux onto your hard drive.

In the same way that there are many makes and models of cars, there are many Linux distros to choose from. Some of the best known distros are RedHat Fedora, SUSE, Ubuntu, and Mint. Each distro has its own installer and unique default configuration according to what the distributor considers to be the best arrangement. The ideal one for you will depend on your own personal preferences and how you want to use Linux. The most popular distros are described below to help you choose:

**RedHat Fedora**

One of the most publicized Linux distros, comprising the commercial RedHat Enterprise Linux product line and the free Fedora distro that is developed by the Fedora Project community. There are several editions of the Fedora distro – “Workstation” for PCs, “Server” for servers, and “IoT” for cloud-based ecosystems.

**Pros**: Widely used, excellent community support, innovative.

**Cons**: Limited product life-span of Fedora editions, poor multimedia support.

Free download from **[getfedora.org](http://getfedora.org)**

![image](images/pg10_2.jpg)

“Choose Freedom. Choose Fedora.”

**openSUSE**

The community-based “openSUSE” distro has received positive reviews for its installer and YaST configuration tools. The documentation, which comes with the boxed product, has been labeled as the most complete by far. The fixed release “Leap” distro is the base for the openSUSE award-winning SUSE Linux Enterprise (SLE) products, and the rolling release “Tumbleweed” distro provides the very latest stable versions of all software.

**Pros**: Attention to detail, easy-to-use YaST configuration tools.

**Cons**: Huge distro – including over 1,500 bundled packages.

Free download from **[opensuse.org](http://opensuse.org)**

![image](images/pg11_1.jpg)

“The makers’ choice for sysadmins, developers and desktop users.”

**Ubuntu**

This sophisticated community distro typically employs the popular Gnome GUI desktop manager. It has the advantage of a fixed six-month release cycle, and every two years there is an LTS (**L**ong **T**erm **S**upport) release that is supported for five years. There are several editions of the Ubuntu distro – “Desktop” for PCs, “Server” for servers, “IoT ” for Internet of Things devices, and “Cloud” for cloud computing. The default interface of the Ubuntu Desktop edition is quite different to that of the Windows desktop.

**Pros**: Great community, and fixed release cycle.

**Cons**: The interface will seem unfamiliar to Windows users.

Free download from **[ubuntu.com](http://ubuntu.com)**

![image](images/pg11_2.jpg)

“Fast, secure and simple, Ubuntu powers millions of PCs worldwide.”

**Linux Mint**

A modern, elegant operating system that is easy to use. It is based on the Ubuntu operating system and works straight out of the box, with full multimedia support. All Linux Mint distros are LTS releases that appear shortly after each Ubuntu LTS release, and are supported for five years. Users are encouraged to send feedback so their ideas can be used to improve Linux Mint. This operating system typically employs the Cinnamon GUI desktop manager, which will feel familiar to those moving from the Windows operating system. For that reason, Mint is used throughout this book to demonstrate the features of a Linux operating system.

**Pros**: Great community, and the interface will seem familiar to Windows users – the best distro for beginners.

**Cons**: Ubuntu has a larger community of users than Mint.

Free download from **[linuxmint.com](http://linuxmint.com)**

![image](images/pg11_3.jpg)

“Linux Mint. From freedom came elegance”.

**Providing Disk Space**

![image](images/pg12_1.jpg)

An operating system is installed on an area of the hard disk drive called a “partition”. When Windows is the only installed operating system, its partition will normally occupy the entire hard drive. To install Linux in this situation there are three possible options:

•**Delete the Windows partition** – replacing it with Linux partitions that occupy the entire drive. This option will delete the Windows operating system along with all the applications and data files. It creates a dedicated Linux computer that will immediately start Linux when the PC gets switched on.

•**Reduce the Windows partition size** – so that it no longer occupies the entire drive, then create Linux partitions in the resulting free space. This option will retain the Windows operating system, applications and data files. It creates a “dual-boot” computer that allows the user to choose whether to start Linux or Windows whenever the PC gets switched on.

•**Add a second hard drive to the system** – this allows Linux partitions to occupy the entire second drive and retains the Windows operating system, applications and data files on the first drive. It too creates a dual-boot computer that allows the user to choose whether to start Linux or Windows whenever the PC gets switched on.

![image](images/hot.jpg)

A **H**ard **D**isk **D**rive (HDD or simply “hard drive”) can be partitioned into one or more regions so that the operating system can manage each region separately.

The option to install an additional hard drive for Linux is a popular choice for many people as they have often upgraded their original hard drive to a larger one, and so have their original drive spare. It also has several benefits over the other options:

•The free space on the Windows drive is not reduced.

•It removes the risk of data loss through partition resizing.

•The familiar Windows operating system is retained.

•It distinctly separates the two operating systems.

•Drive failure would only disrupt one operating system.

![image](images/snake.jpg)

Resizing partitions is a scary process where data loss can, and does, occur – even in expert hands. All contents of the partition must be backed up before attempting this operation.

**Adding a Second Hard Drive**

Older IDE (Integrated Drive Electronics) hard drives need to be configured as a master/slave relationship by setting “jumpers” on the hard drive. The drives can then be connected in tandem by a single ribbon cable.

![image](images/pg13_1.jpg)

Most modern PCs now have SATA hard drives that do not need a master/slave configuration. Providing you have a Windows drive installed, your PC will automatically recognize an additional drive as secondary:

![image](images/1b.jpg)Turn off your PC, open up the case and find the existing hard drive – located in a cage

![image](images/2b.jpg)Install an additional SATA drive in the cage, then follow the cable of the first drive to identify where it plugs into the motherboard – usually a connector marked “SATA”

![image](images/3b.jpg)Plug your new drive’s SATA cable into an adjacent SATA connector on the motherboard, and plug the other end into the new SATA drive itself

![image](images/4b.jpg)Attach a power cable from the PC’s power unit to the SATA drive, then close the case and turn on your PC

![image](images/5b.jpg)Right-click the Start button and choose **Disk** **Management** to see an “Initialize Disk” dialog appear

![image](images/6b.jpg)Click **OK** to initialize the new hard drive, then back in Disk Management, right-click on the new drive and choose **New Simple Volume** from the context menu

![image](images/7b.jpg)Repeatedly click **Next** in the “New Simple Volume Wizard” to format the drive and allocate it a drive letter

![image](images/hot.jpg)

If you are not comfortable working inside your PC case, a computer store should be pleased to undertake the fitting of a second drive for a modest fee.

![image](images/pg13_2.jpg)

SATA (**S**erial **A**dvanced **T**echnology **A**ttachment) is the standard for connecting devices to the PC’s motherboard.

**Creating Boot Media**

![image](images/pg14_1.jpg)

The Linux Mint distro is available in three editions, with desktop environments called “Cinnamon”, “MATE”, and “Xfce” respectively. The most popular version is the Cinnamon edition that will be used throughout this book. It can be downloaded onto a USB flash drive to create “boot media”. This lets you try out Linux without making changes to your system, and lets you install Linux onto your system if desired. But first you will need to ensure your system meets these minimum requirements:

•**1GB of RAM** (2GB preferred)

•**15GB of disk space** (20GB preferred)

•**1024 x 768 screen resolution**

Like other Linux distros, the Linux Mint download is an ISO image file whose content must be “burnt” onto the USB flash drive (not merely copied onto it) to create the boot media:

![image](images/1b.jpg)Launch a web browser, then navigate to the download page **[linuxmint.com/download.php](http://www.linuxmint.com/download.php)**

![image](images/2b.jpg)Next, click on the **Cinnamon** link

![image](images/pg14_2.jpg)

![image](images/3b.jpg)Now, click a **Download mirror** link for your country from the list that appears

![image](images/4b.jpg)Choose to save the ISO image file in a preferred location on your system to begin the download

![image](images/pg14_3.jpg)

linuxmint.iso

![image](images/5b.jpg)When the download completes, you now need an app to burn the image onto the USB flash drive. Linux Mint recommends the **Etcher** app. Navigate your web browser to **balena.io/etcher** and download the installer for your system, such as “Download for Windows (x86/x64)”

![image](images/hot.jpg)

USB Flash Drive – also variously known as Thumb Drive, Pen Drive, Disk Key, Gig Stick, or Memory Stick.

![image](images/6b.jpg)When the installer download has completed, run its **Setup** wizard to install Etcher on your system

![image](images/7b.jpg)Next, connect a USB flash drive to your computer

![image](images/8b.jpg)Now, start the Etcher app and click the **Flash from file** button, then select the ISO image file you downloaded

![image](images/pg15_1.jpg)

![image](images/pg15_2.jpg)

![image](images/9b.jpg)Click the **Select target** button, then select the USB flash drive you connected to your computer

![image](images/10b.jpg)Click the **Flash!** button to burn the contents of the ISO onto the USB flash drive – creating the Linux boot media

![image](images/pg15_3.jpg)

![image](images/pg15_4.jpg)

![image](images/hot.jpg)

If you wish to verify the ISO image file (recommended) you can find instructions on how to do so at [linuxmint-installation-guide.readthedocs.io/en/latest/verify.html](http://linuxmint-installation-guide.readthedocs.io/en/latest/verify.html)

**Starting a Live Session**

Having created the boot media by following the steps [here](#chapter01.xhtml_sec4), you now have the ability to run Linux Mint in a “Live Session”. This means you can safely explore the Linux operating system on a PC where Windows is already installed on the hard drive as its operating system.

![image](images/pg16_1.jpg)

In order to begin a Linux Live Session your PC must be able to boot up from the USB flash drive containing the boot media. This requires the PC’s boot settings to seek instructions from the USB flash drive before seeking instructions on the hard drive. If your PC looks to boot from the hard drive first, you will need to change the settings:

![image](images/1b.jpg)Consult your PC’s documentation to discover how to access its **Setup** utility. This often requires you to press the F2 key while starting the PC – but it does vary

![image](images/2b.jpg)Connect the USB flash drive boot media to your PC

![image](images/3b.jpg)Start up your PC and enter the Setup utility

![image](images/4b.jpg)Select the section relating to the PC’s **Boot** process

![image](images/pg16_2.jpg)

![image](images/5b.jpg)Make the flash drive (USB HDD) the first boot device by following the Setup utility’s **Help** instructions

![image](images/hot.jpg)

The UEFI (**U**nified **E**xtensible **F**irmware **I**nterface) in modern PCs replaces the BIOS (**B**asic **I**nput/**O**utput **S**ystem) firmware interface in earlier PCs. These control how your PC boots up.

![image](images/forget.jpg)

The Setup utility is unique to your PC, so its appearance will probably differ from the one shown here. Most PCs will, however, provide a way to change the Boot Priority Order so you can boot the PC from the USB flash drive.

![image](images/6b.jpg)Save the new settings and exit the Setup utility – typically by pressing the F10 key

![image](images/7b.jpg)If your PC is configured to boot in legacy BIOS mode, Linux Mint will now automatically start a Live Session

![image](images/pg17_1.jpg)

If your PC is configured to boot in UEFI mode, you will be presented with a menu. Select the “Start Linux Mint” option, then hit the **Enter** key to start a Live Session.

![image](images/pg17_2.jpg)

![image](images/hot.jpg)

When there is an option to choose between UEFI boot mode and legacy BIOS mode, UEFI offers several advantages – UEFI supports large hard drive partitions, has secure booting, and provides efficient system management.

![image](images/hot.jpg)

You may also see “UEFI” referred to as “EFI” – UEFI is simply EFI 2.0.

**Beginning Installation**

![image](images/pg18_1.jpg)

Having started a Live Session by following the steps [here](#chapter01.xhtml_sec5), you can try out the Linux Mint operating system. It will perform in a similar manner to when it is permanently installed on the hard drive, but with these notable exceptions:

•**The Live Session is slower** – it is loaded from the USB flash drive, rather than quickly from a hard drive.

•**Changes are not permanent** – they are not saved on the USB flash drive, or written anywhere on your PC.

•**Some apps behave differently** – system utilities, such as the Update Manager, cannot be used effectively.

The user name in a Live Session is “mint”. If asked for a password you can simply hit the Enter key to proceed.

Live Session provides an installer icon on the Desktop that can be used to begin permanent installation of Linux Mint:

![image](images/pg18_2.jpg)

![image](images/1b.jpg)Double-click on the “Install Linux Mint” icon to launch the Linux Mint installer wizard

![image](images/2b.jpg)On the “Welcome” screen, select your preferred language, then click the **Continue** button

![image](images/pg19_1.jpg)

![image](images/3b.jpg)On the “Keyboard layout” screen, select your layout, then click the **Continue** button

![image](images/pg19_2.jpg)

![image](images/hot.jpg)

If you are unsure of the keyboard layout you can type into this box and let the installer figure it out.

![image](images/4b.jpg)Choose your wireless connection when asked, then check the box to install codecs and click the **Continue** button

![image](images/pg19_3.jpg)

![image](images/forget.jpg)

This book features Linux Mint version 20 (Ulyssa) Cinnamon throughout. This version has Long Term Support until 2025.

![image](images/snake.jpg)

Third-party codecs are required for multimedia support in certain apps. You are almost certainly going to want them.

**Completing Installation**

![image](images/5b.jpg)On the “Installation type” screen...

![image](images/pg20_1.jpg)

If you want only the Linux operating system on your PC (recommended), select **Erase disk and install Linux Mint**.

![image](images/pg20_2.jpg)

Or, if Windows is installed and you also want to keep that on your PC, select the option to **Install Linux Mint alongside Windows Boot Manager**.

![image](images/pg20_3.jpg)

![image](images/hot.jpg)

Advanced users can choose to manage disk partitions by choosing the **Something else** option here. Linux Mint requires one partition to be mounted on the root/directory. Although the operating system occupies around 15GB, this partition should ideally be 100GB+.

If you retain Windows, the installer will resize the Windows operating system and install Linux in the free space created. A boot menu should appear so you can choose between operating systems whenever you start your PC – a “dual-boot” setup.

![image](images/6b.jpg)After choosing the installation type in either case, adjust the space suggested for each operating system if desired, then click the **Install Now** button to proceed

![image](images/snake.jpg)

Attempting to create a dual-boot setup can be problematic on some PCs – erase the entire disk and install Linux Mint.

![image](images/7b.jpg)On the “Where are you?” screen, select your timezone then click the **Continue** button

![image](images/pg21_1.jpg)

![image](images/hot.jpg)

Simply click your approximate location on the global map to select your timezone.

![image](images/8b.jpg)On the “Who are you?” screen, enter your details then click the **Continue** button to install system files

![image](images/pg21_2.jpg)

![image](images/hot.jpg)

If you are the only user of the PC you can select the option to **Log in automatically** so you will not be asked for your password whenever you start Linux Mint. You may also select the **Encrypt my home folder** option if you are concerned about security.

![image](images/9b.jpg)Enjoy the slideshow while Linux Mint gets installed, then upon completion click the **Restart Now** button

![image](images/pg21_3.jpg)

![image](images/pg21_4.jpg)

![image](images/hot.jpg)

For help with installation refer to the online Linux Mint forums at **[forums.linuxmint.com](http://forums.linuxmint.com)**

**Enabling Backups**

![image](images/pg22_1.jpg)

Having completed the installation process by following the steps [here](#chapter01.xhtml_sec6), Linux Mint will launch to your Desktop. Before you start using the operating system it is recommended you enable the “Timeshift” backup utility. This is like “System Restore” on Windows and will allow you to restore the operating system to an earlier backup should any problems arise:

![image](images/1b.jpg)Click on **Menu** (“Start” button), **Administration**, **Timeshift**

![image](images/pg22_2.jpg)

![image](images/2b.jpg)Next, enter the password you chose in the “Who are you?” dialog during the installation process, then click the **Authenticate** button

![image](images/pg22_3.jpg)

![image](images/3b.jpg)Now, select the “RSYNC” option, then click the **Next** button

![image](images/pg22_4.jpg)

![image](images/hot.jpg)

“RSYNC” is a disk-based backup system that only backs up what has changed since the previous backup.

![image](images/4b.jpg)Select the device on which you want the system backup snapshots to be saved, then click the **Next** button. (Here, the chosen device is an external hard drive that is connected, but you could alternatively connect a USB flash drive and choose that device for backups

![image](images/pg23_1.jpg)

![image](images/5b.jpg)Select the monthly, weekly, daily and hourly frequency for when you would like system backup snapshots to be saved on your chosen device, then click the **Finish** button

![image](images/pg23_2.jpg)

![image](images/6b.jpg)Re-open Timeshift in the future and select a saved backup snapshot, then click the **Restore** button to restore your Linux Mint system

![image](images/pg23_3.jpg)

![image](images/forget.jpg)

Do not choose your main hard drive as the location at which to save backup snapshots – this would not help you if your hard drive fails.

![image](images/snake.jpg)

Backup snapshots are saved in a newly-created **timeshift** directory at the root level on the chosen device. Boot snapshots are performed in the background so do not affect the speed at which the system boots.

**Summary**

•**Linux** is a free, stable multi-user operating system that is derived from the powerful Unix operating system.

•The name “Linux” combines letters from the first name of its originator, **Linu**s Torvalds, with the final letter of Uni**x**.

•Both **KDE** and the **Gnome** desktop are user-friendly graphical user interfaces, providing the same point-and-click convenience of the Windows desktop.

•The **kernel** provides the core functionality of Linux.

•Linux **distros** bundle the kernel, system-level programs, and free user-level programs in a variety of combinations.

•The most popular Linux Mint distro employs the **Cinnamon** desktop manager, and is the best distro for beginners.

•Minimum hardware **requirements** to run Linux Mint are 1GB of RAM, 15GB of disk space, and a screen resolution of 1024 x 768 – but higher specifications will perform better.

•A second **hard drive** can easily be added to a PC so it can dual-boot to Linux or Windows.

•A Linux distro can be downloaded and burned as a file system image onto a USB flash drive to create **boot media**.

•In order to boot from a USB flash drive it may be necessary to change the boot device order using the boot **Setup utility**.

•A **Live Session** lets you try out most features of Linux Mint before installation, and also provides an installer.

•The Linux Mint **installer** allows you to install Linux as the sole operating system, or install it alongside Windows.

•Before you start using the Linux Mint operating system it is recommended you enable the **Timeshift** backup utility so you can restore your system should problems arise.

2

**Exploring the Desktop**

***This chapter describes the Linux Mint interface, explains how to use it, and demonstrates how to customize it.***

[**Meeting the Interface**](#chapter02.xhtml_sec10)

[**Configuring the Desktop**](#chapter02.xhtml_sec11)

[**Adding Desklets**](#chapter02.xhtml_sec12)

[**Adjusting the Taskbar**](#chapter02.xhtml_sec13)

[**Launching Apps**](#chapter02.xhtml_sec14)

[**Editing the Menu**](#chapter02.xhtml_sec15)

[**Installing Updates**](#chapter02.xhtml_sec16)

[**Closing the Desktop**](#chapter02.xhtml_sec17)

[**Summary**](#chapter02.xhtml_sec18)

**Meeting the Interface**

![image](images/pg28_1.jpg)

When you start up the Linux Mint operating system, the first thing you see while the system begins loading is a black screen displaying only the Linux Mint logo:

![image](images/pg26_2.jpg)

![image](images/forget.jpg)

The distro featured throughout this book is Linux Mint 20 (Ulyssa).

Unless you selected the option to “Log in automatically” during the installation process (as described [here](#chapter01.xhtml_timezone)), the next thing you see is the **Log in** screen shown below:

![image](images/pg26_3.jpg)

You can now enter the password you chose, then click the arrow button that appears in the password box (or hit the **Enter** key) to log in to the Linux Mint operating system.

![image](images/hot.jpg)

The current time is also shown at the top right of the **Log in** screen. Hover your mouse cursor above the time to see the current date appear in a pop-up **Tooltip** box.

After you log into Linux Mint, whether via the **Log in** screen or by choosing the automatic option, the GUI (**G**raphical **U**ser **I**nterface) Desktop and Taskbar will appear, as shown below:

![image](images/pg27_1.jpg)

![image](images/hot.jpg)

The **Welcome** dialog provides helpful information for new users. Uncheck this option if you don’t want to see this dialog again. Click the **X** button in the top right of any window to close that window.

If you have experience of the Windows operating system, the Linux Mint Desktop will seem familiar – as is the intention.

**System Tray**

The System Tray contains, by default, five icons that provide access to useful features when you click on the icon:

![image](images/pg27_2.jpg)

![image](images/hot.jpg)

Hover your mouse cursor above any System Tray icon to see information appear in a pop-up **Tooltip** box.

**Configuring the Desktop**

![image](images/pg28_1.jpg)

One of the first changes many people want to make to their Linux Desktop is to the background “wallpaper” of the Desktop:

![image](images/1r.jpg)Right-click anywhere on the Desktop wallpaper – to open a context menu

![image](images/pg28_2.jpg)

![image](images/2r.jpg)Select the **Change Desktop Background** option – to open a “Backgrounds” settings window

![image](images/3r.jpg)Choose **Ulyssa** in the left-hand pane – to see a selection of wallpaper images appear in the right-hand pane

![image](images/pg28_3.jpg)

![image](images/hot.jpg)

You can click the **Settings** button to adjust how the image fits your Desktop, or to choose a background color instead of an image.

![image](images/hot.jpg)

You can also click on the **Pictures** folder to choose one of your own images.

![image](images/4r.jpg)Scroll down and click on any image – to see it instantly applied as background wallpaper on your Desktop

![image](images/pg28_4.jpg)

If you are used to seeing the “Recycle Bin” icon on the Windows Desktop, or would simply like to restore deleted files easily, you will want to see the “Trash” icon on Linux Mint’s Desktop:

![image](images/1r.jpg)Right-click anywhere on the Desktop wallpaper to open the context menu and select **Customize** – to open a “Current Monitor Layout” window

![image](images/pg29_1.jpg)

![image](images/pg29_2.jpg)

![image](images/hot.jpg)

You can select options from this window to change the size of all Desktop icons and change how they are arranged.

![image](images/2r.jpg)Next, click the **Desktop Settings** link – to open a “Desktop” window

![image](images/pg29_3.jpg)

![image](images/3r.jpg)See that the toggle switch for the **Trash** icon is in the “Off ” position

![image](images/4r.jpg)Slide the toggle switch to the ![image](images/pg29_4.jpg) “On” position to see the Trash icon now appear on the Desktop

![image](images/pg29_5.jpg)

**Adding Desklets**

![image](images/pg30_1.jpg)

Linux Mint offers a number of small apps (“applets”) that run on the Desktop. These are similar to the Desktop widgets you may have seen in Windows, but are called “Desklets” (**Desk**top app**lets**) in Linux Mint. Some desklets are installed as standard, and you can download many more:

![image](images/1r.jpg)Right-click anywhere on the Desktop wallpaper to open the context menu, then select **Add Desklets** – to open a “Desklets” settings window

![image](images/pg30_2.jpg)

![image](images/2r.jpg)Next, select an installed desklet, such as the **Clock desklet**

![image](images/pg30_3.jpg)

![image](images/3r.jpg)Now, click the **+ Add** button to instantly add the desklet to your Desktop

![image](images/pg30_4.jpg)

![image](images/hot.jpg)

You can click the **General Settings** button in the Desklets window to modify width and decoration aspects of your desklets.

![image](images/forget.jpg)

You can drag desklets around the Desktop to arrange them to your preference.

![image](images/4r.jpg)Click the **Download** button, then choose a desklet and click the Down arrow button to install it on your PC

![image](images/pg31_1.jpg)

![image](images/5r.jpg)Click the **Manage** button to see your chosen desklet has been added to the list of installed desklets

![image](images/pg31_2.jpg)

![image](images/hot.jpg)

Click the **-** button to remove a selected desklet from the Desktop, or click the **x** button to uninstall a selected desklet.

![image](images/6r.jpg)Select the newly-installed desklet, then click the **+ Add** button to instantly add it to your Desktop

![image](images/pg31_3.jpg)

![image](images/hot.jpg)

When you select the **Download** button a dialog might advise you that “Your cache is out of date”. Click the **Yes** button on the dialog to update it now.

![image](images/hot.jpg)

Right-click on a desklet to see a context menu that offers configuration options and an option to remove the desklet from the Desktop.

**Adjusting the Taskbar**

![image](images/pg32_1.jpg)

The Taskbar panel contains an icon for each running app window that you can click to restore a minimized window to its original size. Usefully, you can hover the mouse cursor over the icon of a minimized app to see a thumbnail preview of that window:

![image](images/pg32_2.jpg)

Additionally, you can add useful applets to the Taskbar panel:

![image](images/1r.jpg)Right-click on the **Taskbar** to open a context menu

![image](images/pg32_3.jpg)

![image](images/2r.jpg)Select the **Applets** option – to open an “Applets” settings window

![image](images/pg32_4.jpg)

![image](images/hot.jpg)

You can click the **Panel settings** item on this context menu for options to automatically hide the Taskbar panel, add more panels, and edit panels.

![image](images/hot.jpg)

Notice that the **Applets** settings window functions much like the **Desklets** settings window described [here](#chapter02.xhtml_sec12).

![image](images/3r.jpg)Click the **Manage** button to select from a list of installed applets, or click the **Download** button to install another applet – for example, download the “Weather” applet

![image](images/4r.jpg)Click the **Manage** button and select the Weather applet, then click the **+ Add** button to add it to the Taskbar panel

![image](images/5r.jpg)The weather app should detect your location, but also allows you to choose a location. Right-click on the applet then choose the **Configure** option

![image](images/pg33_1.jpg)

![image](images/6r.jpg)In the Weather settings window, click the **Location** button then slide the **Manual Location** button to “On”

![image](images/pg33_2.jpg)

![image](images/7r.jpg)Next, type a preferred city name into the **Location** box, then close the window

![image](images/8r.jpg)Now, click the Taskbar applet to see the weather for your chosen location

![image](images/pg33_3.jpg)

![image](images/hot.jpg)

Right-click on an applet to see a context menu that offers configuration options and an option to remove the applet from the Desktop.

**Launching Apps**

![image](images/pg34_1.jpg)

Apps can be launched in Linux Mint from the (Start) Menu and additional launchers can easily be added to the Taskbar, or on the Desktop, for frequently-used applications:

![image](images/1r.jpg)Click the ![image](images/pg34_2.jpg) **Menu** button, at the far left of the Taskbar, then position the mouse pointer over the **Accessories** category to see that category’s list of apps

![image](images/2r.jpg)On the Accessories menu list, click the **Text Editor** item to launch the Text Editor app

![image](images/pg34_3.jpg)

![image](images/hot.jpg)

You can also type the name of an app into this **Search** box to find it.

![image](images/hot.jpg)

The launchers in the sidebar are “Favorites”. You can choose **Add to favorites** on the context menu to add a launcher in the sidebar.

![image](images/3r.jpg)Right-click on the Text Editor item in the Accessories menu, then choose **Add to panel** from the context menu to create a launcher button on the Taskbar

![image](images/pg34_4.jpg)

![image](images/4r.jpg)Click the new launcher that has been added to the Taskbar to launch the Text Editor

![image](images/pg35_1.jpg)

![image](images/5r.jpg)Right-click on the Text Editor item in the Accessories menu, then choose **Add to desktop** from the context menu to create a launcher icon on the Desktop

![image](images/6r.jpg)Click the shortcut launcher icon that has been added to the Desktop, to launch the Text Editor

![image](images/pg35_2.jpg)

![image](images/hot.jpg)

To delete a launcher from the Taskbar, right-click on it and choose **Remove**. To remove a launcher from the Desktop, right-click on it and choose **Delete**.

You can also create a Desktop launcher icon for any application if you know its precise command name. In this instance, the Text Editor for the Cinnamon Desktop is named “xed”.

![image](images/7r.jpg)Right-click on the Desktop, then choose **Create a new launcher here** from the context menu that appears

![image](images/pg35_3.jpg)

![image](images/8r.jpg)Type a name and the **xed** command name into the appropriate input fields in the “Launcher Properties” dialog, then click its **OK** button to create the Desktop launcher

![image](images/pg35_4.jpg)

![image](images/pg35_5.jpg)

![image](images/hot.jpg)

You can also launch apps from a command prompt in a Terminal window. Simply type the app’s command (**xed** in this case) then hit the **Enter** key to launch the app.

**Editing the Menu**

![image](images/pg36_1.jpg)

Like many things in the Linux Mint operating system, the (Start) Menu can be customized to suit your personal taste:

![image](images/1r.jpg)Right-click on the **Menu** button, at the far left of the Taskbar, then select the **Configure** option

![image](images/pg36_2.jpg)

![image](images/2r.jpg)Click the **Panel** button and slide the **Use a custom icon and label** toggle button to “On”

![image](images/3r.jpg)Select from options to adjust **Appearance** and **Behavior**. For example, change the Menu button’s **Text** value

![image](images/pg36_3.jpg)

![image](images/4r.jpg)See that your selected options are instantly applied to the Menu

![image](images/pg36_4.jpg)

![image](images/5r.jpg)Click the **Menu** button in the “Menu” window, then click the **Open the menu editor** button

![image](images/pg37_1.jpg)

![image](images/hot.jpg)

You can click the hamburger button and save your Menu settings as a file, which can be imported later to resume those settings.

![image](images/pg37_4.jpg)

![image](images/hot.jpg)

The “Super” key refers to the special key on your keyboard. Typically, this is the Windows Key. Press it once to open the Menu, then press it again to close the Menu.

![image](images/pg36_5.jpg)

![image](images/6r.jpg)Slide all toggle switches to the “Off ” position to simplify the Menu

![image](images/pg37_2.jpg)

![image](images/7r.jpg)Now, click the **Open the menu editor** button

![image](images/8r.jpg)Click any category in the left-hand pane, then select Menu items in the right-hand pane

![image](images/pg37_3.jpg)

![image](images/forget.jpg)

You can uncheck the individual items to remove them from the Menu and click the **Restore System** **Configuration** button to resume its default appearance.

**Installing Updates**

![image](images/pg38_1.jpg)

Having set up Timeshift to make regular backups of your Linux Mint operating system (see [here](#chapter01.xhtml_sec8)), it is recommended that you regularly apply all updates available for your system:

![image](images/1r.jpg)Connect your PC to the internet then click **Menu**, **Administration**, **Update Manager**, or click the ![image](images/pg38_2.jpg) Update Manager icon on the system tray to open an “Update Manager” window

![image](images/2r.jpg)If the Update Manager suggests you switch to a local mirror server, click this **Yes** button

![image](images/pg38_3.jpg)

![image](images/3r.jpg)Enter your password, then click the **Authenticate** button – to open a “Software Sources” dialog

![image](images/pg38_4.jpg)

![image](images/4r.jpg)Double-click in the **Main (ulyssa)** box and select a local mirror from the list that appears, then click **Apply**

![image](images/pg38_5.jpg)

![image](images/pg38_6.jpg)

![image](images/5r.jpg)Now, select a local mirror for the **Base (focal)** box, then click **OK** to close the “Software Sources” dialog

![image](images/hot.jpg)

A “Welcome” screen may appear when you first open the Update Manager. Click its **OK** button to proceed.

![image](images/6r.jpg)Wait while the software list gets updated, then return to the “Update Manager” window

![image](images/pg39_1.jpg)

![image](images/7r.jpg)Click the **Select All** button, then click **Install Updates**

![image](images/pg39_2.jpg)

![image](images/8r.jpg)If advised additional packages are required, click **OK**

![image](images/pg39_3.jpg)

![image](images/9r.jpg)Enter your password, then click the **Authenticate** button – Linux Mint will now download and install available updates

![image](images/pg39_4.jpg)

![image](images/pg39_5.jpg)

![image](images/pg39_6.jpg)

![image](images/snake.jpg)

It can take a little time to update the cache and download updates, so it is important to choose a fast local mirror server.

![image](images/hot.jpg)

Notice that in Linux Mint the updates are referred to as “packages”. These are managed by the **Synaptic Package Manager**, which can be found in the Administration category on the Menu.

**Closing the Desktop**

![image](images/pg40_1.jpg)

If your Linux Mint operating system is left unused it will, by default, automatically replace the Desktop with a screensaver and lock the screen. This means you will need to enter your password to get back to the Desktop. If you wish to leave your PC, you can immediately lock the screen for security purposes:

![image](images/1r.jpg)Click the **Menu button**, then click the “Lock screen” button to instantly close the Desktop

![image](images/pg40_2.jpg)

![image](images/2r.jpg)See the screensaver now fills the screen so your PC cannot be used

![image](images/pg40_3.jpg)

![image](images/3r.jpg)Move your mouse when you want to unlock your PC, and you will be presented with a password request – enter your password to return to the Desktop

![image](images/pg40_4.jpg)

![image](images/hot.jpg)

You can also lock the screen using the **Ctrl** + **Alt** + **L** keyboard shortcut. To discover more Linux Mint shortcuts, click **Menu**, **Preferences**, **Keyboard** to open the “Keyboard” window, then click the **Shortcuts** button. Select a category, such as **System**, in the left-hand pane to see available shortcuts in the right-hand pane.

![image](images/hot.jpg)

You can click the ![image](images/pg40_5.jpg) **Switch User** button to log out – you will then see the **Log in** screen illustrated [here](#chapter02.xhtml_sec10).

You may sometimes want to log out of the Linux Mint operating system for security purposes or to switch users:

![image](images/1r.jpg)Click **Menu**, then click the “Log Out” button to see a “Session” options dialog appear

![image](images/pg41_2.jpg)

![image](images/pg41_1.jpg)

![image](images/2r.jpg)Click the **Log Out** option button, or the **Switch** **User** option button, to see the **Log in** screen appear

![image](images/pg41_3.jpg)

![image](images/hot.jpg)

The **Switch User** option saves your session state to allow someone else to log in. When they log out and you log back in, you will be back where you left off – your open apps will still be running. The **Log Out** option, on the other hand, ends the session and closes your open apps – when you log back in they will not be running.

When you are going to be away from your PC for a long time you will probably want to shut down the operating system:

![image](images/1r.jpg)Click **Menu**, then click the “Quit” button to see a “Shut down this system now?” options dialog appear

![image](images/pg41_4.jpg)

![image](images/2r.jpg)Click the **Shut Down** option button to exit Linux Mint and power off your PC

![image](images/pg41_5.jpg)

![image](images/hot.jpg)

The **Suspend** option stops all apps, and the system state is saved in RAM as your PC goes into low-power mode. Hit any key to awaken the PC exactly where you left off.

**Summary**

•Unless the “Log in automatically” option was selected during installation, the **Log in** screen will request your password whenever you start the Linux Mint operating system.

•The Linux Mint GUI comprises a **Desktop** and **Taskbar**.

•The **Desktop** contains shortcuts and background wallpaper.

•The **Taskbar** panel contains a Menu button, Show Desktop button, app launchers, and the System Tray.

•The **System Tray** gives access to Update Manager, Network Status, Battery Status, Time & Date, and Volume Control.

•The Desktop can be configured to have different background **Wallpaper** and to contain different **Shortcut** icons.

•**Desklets** are small apps that run on the Desktop.

•Hovering the mouse cursor over the Taskbar icon of a running app will display a **Thumbnail Preview** of that app.

•Useful **applets** can be added to the Taskbar panel.

•App launchers are grouped by **category** on the Menu.

•App launchers can be added to the **Taskbar** and **Desktop**.

•The Menu can be configured to customize its **Appearance** and its **Behavior**.

•With the Timeshift backup utility enabled, all updates can be regularly applied with the **Update Manager** app.

•Selecting local mirrors as **Software Sources** usually allows updates to be downloaded faster.

•The Desktop can be closed by switching to the **Lock screen** for security.

•The **Log Out** option and **Switch User** option closes the Desktop and opens the **Log in** screen.

•The **Shut Down** option closes the Desktop and powers off the PC.

3

**Setting Preferences**

***This chapter describes some useful ways you can set up your Linux Mint system to suit your preferences.***

[**Configuring the Screensaver**](#chapter03.xhtml_sec19)

[**Managing Windows**](#chapter03.xhtml_sec20)

[**Personalizing Options**](#chapter03.xhtml_sec21)

[**Controlling Connections**](#chapter03.xhtml_sec22)

[**Adding Printers**](#chapter03.xhtml_sec23)

[**Pairing via Bluetooth**](#chapter03.xhtml_sec24)

[**Summary**](#chapter03.xhtml_sec25)

**Configuring the Screensaver**

By default, your Linux Mint Desktop will automatically switch to the screensaver if you do not interact with your PC for a while. This means you may frequently have to enter your password to return to the Desktop and is unnecessary if your PC is located in an environment where security is not a concern. Fortunately, you can disable this behavior so the Desktop will always be visible unless you choose to explicitly lock the PC.

![image](images/pg44_1.jpg)

You may also choose how the screen appears by selecting a custom screensaver, and you can add a message to the Lock screen:

![image](images/1g.jpg)Click **Menu**, **Preferences**, **Screensaver** to open a “Screensaver” window

![image](images/pg44_2.jpg)

![image](images/2g.jpg)Next, click the **Settings** button

![image](images/pg44_3.jpg)

![image](images/3g.jpg)Now, open the drop-down menu for “Screensaver settings” and select the **Never** option – to stop your PC automatically switching to the Lock screen

![image](images/4g.jpg)Choose preferences from the **Lock settings** section

![image](images/hot.jpg)

Notice that you can choose to extend the delay before the screensaver will appear if you don’t want to totally disable the screensaver.

![image](images/5g.jpg)Next, click the **Customize** button

![image](images/6g.jpg)Type a custom **Away message** to be displayed on the Lock screen

![image](images/pg45_1.jpg)

![image](images/7g.jpg)Close the dialog to save your custom message

![image](images/8g.jpg)Click the **Menu button**, then the ![image](images/pg45_2.jpg) “Lock screen button” to see your screensaver, and see your message on the Lock screen

![image](images/pg45_3.jpg)

![image](images/hot.jpg)

There is also a Customize option to “Ask for a custom message when locking the screen from the menu” – so you can add a unique message when you leave your PC.

![image](images/forget.jpg)

There are no animated screensavers included by default with this edition of Linux Mint.

**Managing Windows**

![image](images/pg46_1.jpg)

The control buttons on the Linux Mint window title bars perform the same actions as those in the Windows operating system:

![image](images/pg46_2.jpg)

You can also snap windows to the screen edges, tile windows to the corners of the screen, and move windows between workspaces:

![image](images/1g.jpg)Click **Menu**, **Accessories**, **Text Editor** to open the Text Editor app

![image](images/2g.jpg)Click the window’s ![image](images/pg46_3.jpg) control button to reduce it from full-screen size

![image](images/3g.jpg)Next, click on the window’s title bar and hold down the mouse button, then drag the window to any screen edge

![image](images/4g.jpg)When you see a zone preview, release the mouse button to snap the window to that edge – filling half of your screen

![image](images/pg46_4.jpg)

![image](images/5g.jpg)Now, click on the window’s title bar and hold down the mouse button, then drag the window to any screen corner

![image](images/hot.jpg)

Windows that are not full-size snapped or tiled can be resized by dragging their edges or corners.

![image](images/hot.jpg)

You can ignore the on-screen instruction to **Hold <Ctrl>**. Simply snap two apps to the left and right sides of your screen to work on two documents at the same time.

![image](images/6g.jpg)When you see a zone preview, release the mouse button to snap the window to that corner – filling a quarter of your screen

![image](images/pg47_1.jpg)

![image](images/7g.jpg)Click **Menu**, **Preferences**, **Hot Corners** to open a “Hot Corners” window

![image](images/8g.jpg)Enable the top left-hand corner to show workspaces, then move the mouse cursor to that corner to see the workspaces

![image](images/pg47_2.jpg)

![image](images/pg47_3.jpg)

![image](images/forget.jpg)

You can tile up to four apps. Also, you can snap and tile. For example, tile two apps at the top corners and snap another app across the bottom half of the screen to work on three documents at the same time.

![image](images/hot.jpg)

You can drag apps from one workspace to another and click any workspace to begin working there in full screen. The apps remain running on the hidden workspaces so you can switch back to them.

**Personalizing Options**

![image](images/pg48_1.jpg)

You can personalize the behavior and appearance of windows by specifying preferences on your Linux Mint operating system. For example, many people prefer to change the default light gray windows to dark gray:

![image](images/1g.jpg)Click **Menu**, **Preferences**, **Window Tiling** to open a “Window Tiling” window – here you can disable Tiling and Snapping or modify its behavior

![image](images/pg48_2.jpg)

![image](images/hot.jpg)

Slide this toggle switch to the “Off” position to disable the **Hold <Ctrl>** message when snapping or tiling your windows.

![image](images/2g.jpg)Click **Menu**, **Preferences**, **Windows** to open a “Windows” window – here you can modify title bar actions and window actions

![image](images/pg48_3.jpg)

![image](images/hot.jpg)

Click the **Alt-Tab** button at the top of the dialog and explore switcher style options. To use the window switcher hold down the **Alt** key then jab the **Tab** key to select a window. Release the **Alt** key to give that window focus.

![image](images/pg48_4.jpg)

![image](images/3g.jpg)Click **Menu**, **Preferences**, **Themes** to open a “Themes” window, then click the **Themes** button to see the current appearance settings

![image](images/pg49_1.jpg)

![image](images/hot.jpg)

Click the **Add/Remove** button to see a list of themes you can download and install. These provide additional options on the fly-out menu for the Desktop.

![image](images/4g.jpg)Click the current **Mint-Y** setting for “Window borders” to open a fly-out menu, then select the **Mint-Y-Dark** option to instantly change the border appearance

![image](images/5g.jpg)Similarly, click the current **Mint-Y** setting for “Controls”, then select **Mint-Y-Dark** on the fly-out menu to instantly change the appearance of window controls

![image](images/pg49_2.jpg)

![image](images/hot.jpg)

Click the **Settings** button to see options to show or hide icons on window buttons and menus.

**Controlling Connections**

![image](images/pg50_1.jpg)

Linux Mint allows you to easily control how you connect to the internet via wireless Wi-Fi or wired Ethernet connections. You can also mask your presence via a proxy server or through a Virtual Private Network (VPN) connection:

![image](images/1g.jpg)Click **Menu**, **Preferences**, **Network** to open a “Network” window, then click **Wi-Fi** in the left-hand pane – to see available wireless connections in the right-hand pane

![image](images/pg50_2.jpg)

![image](images/2g.jpg)Similarly, click **Wired** to see available wired connections

![image](images/pg50_3.jpg)

![image](images/3g.jpg)Click **Network proxy** to see or add details for a proxy server with which you could mask your presence

![image](images/pg50_4.jpg)

![image](images/forget.jpg)

You can also click the “Wireless connection” icon on the **System Tray** to view network status.

![image](images/pg50_5.jpg)

![image](images/hot.jpg)

Proxy servers and VPNs both hide your IP address but, unlike VPNs, proxies do not encrypt your connection – it is safer to use a VPN to mask your presence.

![image](images/4g.jpg)Click the + **Add** button to open an “Add VPN” dialog, then choose the **Point-to-Point Tunneling Protocol (PPTP)** option

![image](images/pg51_1.jpg)

![image](images/5g.jpg)Next, enter the Name, URL, and User details of your VPN service, then click the **Advanced** button

![image](images/pg51_2.jpg)

![image](images/snake.jpg)

You will need to click this icon and choose whether to store the password before you can enter a password.

![image](images/6g.jpg)Select authentication and security options and click OK, then click the + **Add** button on the “Add VPN” dialog

![image](images/pg51_3.jpg)

![image](images/7g.jpg)Click the newly-added VPN entry in the “Network” window, then slide the toggle switch to the “On” position to connect

![image](images/pg51_4.jpg)

![image](images/snake.jpg)

The **W-Fi P2P** network connection item is not enabled by default.

**Adding Printers**

![image](images/pg52_1.jpg)

Linux Mint provides drivers for a wide range of printers, so adding a printer is often simply a matter of connecting the printer to a USB port on your PC and turning the printer on. The operating system should recognize the printer and display a notification that it has been automatically added to your system:

![image](images/pg52_2.jpg)

The properties and options of added printers can be found in the “Printers” app, which can also be used to add network printers:

![image](images/1g.jpg)Click **Menu**, **Administration**, **Printers** to open a “Printers” window

![image](images/pg52_3.jpg)

![image](images/pg52_4.jpg)

![image](images/2g.jpg)Double-click on an installed printer to open its “Properties” dialog

![image](images/3g.jpg)Next, turn on a network printer and press its Wi-Fi button to make it visible to the network

![image](images/4g.jpg)Now, click the + **Add** button on the “Printers” window – to open a “New Printers” dialog, listing available printers

![image](images/pg52_5.jpg)

![image](images/forget.jpg)

You can click the **Print Test Page** button on the “Properties” dialog to test your printer.

![image](images/pg52_6.jpg)

![image](images/hot.jpg)

Click the **Printer** menu and select the **View Print Queue** option to open a “Document Print Status” dialog where you can control print jobs.

![image](images/pg52_7.jpg)

![image](images/5g.jpg)Expand the **Network Printer** category, then select your printer and click the **Forward** button

![image](images/pg53_1.jpg)

![image](images/hot.jpg)

If your printer is not immediately listed you can click the **Find Network Printer** option to seek your printer.

![image](images/6g.jpg)Enter a name and description of the printer, then click the **Apply** button

![image](images/pg53_2.jpg)

![image](images/7g.jpg)See that the network printer is now added to the “Printers” window and is ready to print

![image](images/pg53_3.jpg)

![image](images/hot.jpg)

The printer icon marked with a check mark denotes the system-wide default printer. You can change the default printer from its right-click context menu.

![image](images/pg53_4.jpg)

**Pairing via Bluetooth**

![image](images/pg54_1.jpg)

Linux Mint allows you to connect an external device that supports Bluetooth wireless technology, such as a wireless Bluetooth speaker, using a USB dongle and the Bluetooth device manager:

![image](images/1g.jpg)Connect a Bluetooth dongle to a USB port on your PC, or enable Bluetooth if it’s already present on your system

![image](images/pg54_2.jpg)

![image](images/2g.jpg)Turn on the wireless Bluetooth speaker

![image](images/pg54_3.jpg)

![image](images/3g.jpg)Press and hold the speaker’s “pairing” button to switch the speaker into pairing mode

![image](images/4g.jpg)On your PC, click **Menu**, **Preferences**, **Bluetooth** to open the Bluetooth device manager

![image](images/5g.jpg)To search for nearby Bluetooth devices, slide the toggle switch to the “On” position

![image](images/pg54_4.jpg)

![image](images/forget.jpg)

You only need to connect a dongle if your PC does not have a built-in Bluetooth adapter.

![image](images/pg54_5.jpg)

![image](images/hot.jpg)

Slide the toggle switch on the Bluetooth device manager to enable or disable Bluetooth.

![image](images/6g.jpg)When the speaker is found, click on the wireless speaker item in the “Devices” list to pair it with your PC

![image](images/pg55_1.jpg)

![image](images/7g.jpg)When the speaker is connected, the “Not Set Up” message changes to “Connected”

![image](images/pg55_2.jpg)

![image](images/8g.jpg)Click on the wireless speaker item in the “Devices” list to see its status dialog

![image](images/pg55_3.jpg)

![image](images/9g.jpg)Place the cursor over the Bluetooth icon that has been automatically added to the System Tray to see the connection details

![image](images/pg55_4.jpg)

![image](images/hot.jpg)

For security reasons the Bluetooth device manager may sometimes require you to confirm a device’s PIN in order to establish a connection.

![image](images/pg55_5.jpg)

![image](images/snake.jpg)

Once paired, you can disconnect and reconnect to the device, but if you remove it you will need to pair it again to re-establish a connection.

**Summary**

•The **Screensaver** app can be used to disable the screensaver or to choose an animated screensaver.

•The **Lock screen** can be customized to display an “Away message” for times when the user is absent.

•The window title bars in Linux Mint contain familiar **Minimize**, **Maximize/Reduce**, and **Close** buttons.

•Windows can be **Snapped** to the screen edges and **Tiled** to the screen corners.

•The **Hot Corner** feature can be enabled to display workspaces.

•Windows can be dragged from one **Workspace** to another and the apps will remain running on hidden workspaces.

•The **Window Tiling** app can be used to disable Tiling and Snapping or to modify their behavior.

•The **Windows** app can be used to modify title bar actions and to modify window actions.

•A window can be selected with the **Window Switcher** feature by pressing the Alt and Tab keyboard keys.

•The **Themes** app can be used to change the look of Window Borders, Icons, Controls, Mouse Pointer, and Desktop.

•Wi-Fi connections, wired connections, and proxy connections can be controlled with the **Network** app.

•The Network app can also be used to add a **VPN** connection to mask your presence when online.

•Linux Mint should automatically detect and add a **Printer** when it is directly connected to the PC.

•The **Printers** app can be used to add a network printer to the system to enable printing via a Wi-Fi connection.

•The **Bluetooth** app can be used to pair the PC with a nearby Bluetooth device.

4

**Touring the File System**

***This chapter describes the Linux file system and explains its directory structure.***

[**Meeting the Directory Tree**](#chapter04.xhtml_sec26)

[**Recognizing Directories**](#chapter04.xhtml_sec27)

[**Navigating with Nemo**](#chapter04.xhtml_sec28)

[**Handling Files**](#chapter04.xhtml_sec29)

[**Creating Shortcuts**](#chapter04.xhtml_sec30)

[**Locating Files**](#chapter04.xhtml_sec31)

[**Understanding Permissions**](#chapter04.xhtml_sec32)

[**Summary**](#chapter04.xhtml_sec33)

**Meeting the Directory Tree**

![image](images/pg58_1.jpg)

When moving from Windows, the new Linux user needs to be aware of some differences between the two operating systems:

•Linux is case-sensitive – Windows is not. For instance, files named “readme.txt” and “README.txt” are seen as two different files in Linux, but there is no distinction in Windows.

•Linux directories and files have ownership permissions that can restrict accessibility to the owner or group – Windows directories and files are generally universally accessible.

•Linux was developed as a multi-user network operating system – Windows evolved from MS-DOS (**M**icro**s**oft **D**isk **O**perating **S**ystem) as a single-user home operating system.

•Linux desktop users cannot change system settings; only the “root” superuser may do so – Windows desktop users have free reign to wreak havoc.

•Linux partitions are created using the Ext4 file system – Windows partitions use FAT, FAT32 or NTFS file systems.

•Linux path names contain forward slash characters – Windows path names contain backslash characters: for instance, a Linux path /home/mike and a Windows path C:\Users\mike.

•Linux does not have any drive letters – Windows typically uses C: for the hard disk drive, D: for the optical drive, E: for an external drive, and so on.

![image](images/hot.jpg)

See [here](#chapter04.xhtml_sec32) and [here](#chapter10.xhtml_sec83) for more on access permissions.

![image](images/hot.jpg)

See [here](#chapter10.xhtml_sec81) for more on the Linux file system.

The lack of drive letters in Linux indicates what is, probably, the biggest difference between Linux and Windows – the way their directory structures are arranged. In Linux, everything is contained within a single unified hierarchical system – beginning with the “root” directory, symbolized by a single forward slash “/”.

The Linux installation creates a number of standard sub-directories within the root directory. Each one of these, in turn, houses its own sub-directory structure, thereby creating a directory “tree” – the “root” directory of / is the root of the tree.

Contents of peripheral drives appear in the tree in the directory at which they are “mounted” by Linux, creating a unified structure. The table below lists the directory structure of the Linux Mint file system. All are sub-directories of the basic root directory “/”.

![image](images/pg59_1.jpg)

The purpose of each standard Linux directory is described in more detail on the ensuing pages of this chapter.

![image](images/snake.jpg)

Do not confuse the **/root** directory (the home directory of the root superuser) with the **/** root of the file system.

**Recognizing Directories**

/bin

Contains small executable programs (binaries) that are required when your PC boots up, and programs that execute basic commands. This directory is roughly equivalent to the C:\Windows directory in Windows.

![image](images/pg60_1.jpg)

/boot

Contains important files required when your PC boots up and also the Linux kernel itself – the heart of the operating system. The kernel controls access to all the hardware devices your computer supports, and allows multiple programs to run concurrently and share that hardware.

![image](images/pg60_2.jpg)

/cdrom

This is historically a directory in which CD-ROMs inserted into the system were mounted – the standard location is now /media.

![image](images/pg60_3.jpg)

/dev

Contains special file system entries that represent devices that are attached to the system. These allow programs access to the device drivers that are essential for the system to function properly – although the actual driver files are located elsewhere. The entry / dev/sda represents the first hard drive on your PC.

![image](images/pg60_4.jpg)

/etc

Contains system configuration files storing information about everything from user passwords and system initialization to screen resolution settings. These are plain text files that can be viewed in a text editor. The files in this directory are roughly equivalent to the combination of .ini files and the Registry entries found in the Windows operating system.

![image](images/pg60_5.jpg)

/home

Contains a sub-directory for each user account to store personal data files. If there is a user account named “mike” there will be a /home/mike directory where that user can store personal files – other users cannot save files there. This directory is where you store all your working documents, images, and media files.

![image](images/pg61_1.jpg)

/lib

Contains 32-bit library files that are used by the executable programs in the /bin and /sbin directories. These shared libraries are particularly important for booting the system and executing commands within the root file system. They are roughly equivalent to the .dll (**D**ynamic **L**ink **L**ibraries) in Windows.

![image](images/pg61_2.jpg)

/lib64

Contains 64-bit library files that are used by the executable programs in the /bin and /sbin directories.

![image](images/pg61_3.jpg)

/lost+found

Contains misplaced files that may be corrupted, but from which data can still be recovered.

![image](images/pg61_4.jpg)

/media

This is a directory in which removable media inserted into the system gets mounted. When you connect a USB flash drive to your PC, a sub-directory, such as /media/flash-drive, is created.

![image](images/pg61_5.jpg)

/mnt

This is a directory in which the system administrator can temporarily mount an additional file system.

![image](images/pg61_6.jpg)

/opt

Contains nothing initially, but this directory provides a special area where optional add-on application software packages can be installed. If “example” is the name of a particular software package in the /opt directory, then all its files could be placed within sub-directories of an /opt/example directory.

![image](images/pg62_1.jpg)

/proc

Contains special files that relay information to and from the kernel. The hierarchy of “virtual” files within this directory represents the current state of the kernel. Unlike binary and text files, most virtual files are listed as zero bytes in size and are time-stamped with the current date and time. This reflects the notion that they are constantly updating.

![image](images/pg62_2.jpg)

/root

This is the home directory of the root account superuser – for security reasons, regular users cannot access this directory.

![image](images/pg62_3.jpg)

/run

Contains transient files required by applications at runtime to supply data such as process IDs.

![image](images/pg62_4.jpg)

/sbin

Contains executable system programs (binaries) that are only used by the root superuser and by Linux when the system is booting up or performing system recovery operations. For instance, the clock program that maintains the system time when Linux is running is located in the /sbin directory. This directory is roughly equivalent to the C:\Windows\system directory in Windows.

![image](images/pg62_5.jpg)

/srv

Contains files that supply data for services provided by the system.

![image](images/pg63_1.jpg)

/sys

This is a virtual file system that stores the kernel’s view of the system and of the devices connected to the system.

![image](images/pg63_2.jpg)

/timeshift

Contains backup snapshots of the system taken at intervals specified by the Timeshift app.

![image](images/pg63_3.jpg)

/tmp

Contains temporary files that have been created by running programs. Mostly these are deleted when the program gets closed, but some do get left behind – periodically these should be deleted. This directory is roughly equivalent to the C:\Windows\Temp directory in Windows.

![image](images/pg63_4.jpg)

/usr

Contains applications and files used by users, as opposed to applications and files used by the system. For example, non-essential applications are located inside the /usr/bin directory instead of the /bin directory.

![image](images/pg63_5.jpg)

/var

Contains variable data files that store information about ongoing system status, particularly logs of system activity. To see recent logged event messages, enter tail /var/log/syslog at a prompt.

![image](images/pg63_6.jpg)

**Navigating with Nemo**

The standard Linux sub-directories can be viewed graphically by opening the Nemo file browser app in the / system root location. In Linux Mint, Nemo can be launched by clicking the ![image](images/pg64_2.jpg) “Files” button on the Taskbar or by selecting “Files” on the Menu.

![image](images/pg64_1.jpg)

![image](images/1p.jpg)Click **Menu**, **Accessories**, **Files** to open the file browser – see the sub-directories within your home directory

![image](images/2p.jpg)Expand the **My Computer list** in the left-hand sidebar

![image](images/3p.jpg)Click the **File System** item – to see all the system’s standard sub-directories within the / system root directory

![image](images/pg64_3.jpg)

![image](images/hot.jpg)

Notice that when you click on a folder icon, information about its contents appears at the bottom of the window – see how many folders are empty.

![image](images/hot.jpg)

You can click these buttons to change the sidebar view and to show/hide the sidebar.

![image](images/4p.jpg)Click any directory folder to explore the system’s standard sub-directories

![image](images/5p.jpg)Click the ![image](images/pg64_4.jpg) back button above the sidebar to go to the previously-visited location

![image](images/hot.jpg)

If you cannot see the sidebar when you open Nemo, hit the F9 key to show the sidebar.

You can navigate through the file system with Nemo by clicking on a folder or by clicking on a location in the sidebar. Also, you can click the ![image](images/pg65_1.jpg) button on the toolbar to open a location field, then type in a directory address and hit the **Enter** key.

![image](images/6p.jpg)Click the folder icon of the /home directory (“home”) – there will be a folder there bearing your username

![image](images/7p.jpg)Click on the folder bearing your username to see the contents of your home directory

![image](images/pg65_2.jpg)

![image](images/hot.jpg)

Notice that Nemo displays the name of the currently-displayed directory on its title bar.

![image](images/hot.jpg)

You can click these buttons to change how the folders are viewed.

![image](images/hot.jpg)

You can drag this slider to adjust the zoom level.

![image](images/8p.jpg)On the Nemo file browser toolbar, click the ![image](images/pg65_3.jpg) up button twice to navigate back up to the / root location

![image](images/9p.jpg)Click the **Home** item in the sidebar to navigate to the user’s home directory once more – then return to / again

![image](images/10p.jpg)Click the ![image](images/pg65_4.jpg) button on Nemo’s toolbar to reveal the location field, and type the address of the user’s home directory (in this case /home/mike), then), then hit **Enter** to navigate to the home directory one more time

![image](images/pg65_5.jpg)

**Handling Files**

![image](images/pg66_1.jpg)

All data files you create in Linux should only be saved in your home directory, or a sub-directory (“folder”). They can be revisited at any time using the Nemo file browser and can be easily copied, moved, renamed, or deleted:

![image](images/1p.jpg)Click on **Menu**, **Accessories**, **Text Editor** to launch a plain text editor, then type in some text and click ![image](images/pg66_2.jpg) the Save button on the toolbar (or click the File, Save menu)

![image](images/2p.jpg)In the “Save As” dialog, double-click your **Documents** folder to open it, then type a name for the text document (say, sample.txt) and click the ![image](images/pg66_2.jpg) Save button

![image](images/3p.jpg)Launch the Nemo file browser, then open the **Documents** folder that is located in your home directory and find the saved text file

![image](images/4p.jpg)Right-click on the file’s icon and choose **Copy** from the context menu – to copy that file to the “clipboard”

![image](images/pg66_4.jpg)

![image](images/5p.jpg)Next, right-click on the **Public** folder within your home directory, then choose **Paste Into Folder** from the context menu – to deposit a copy of the file

![image](images/forget.jpg)

The **clipboard** is a memory buffer provided by the operating system and is used for short-term data transfer.

![image](images/hot.jpg)

Directories may contain hidden files – click the **View**, **Show Hidden Files** menu in the Nemo file browser to also show hidden files.

![image](images/6p.jpg)Open the Public folder, then right-click on the copied file and choose **Rename** from the context menu to see the file name get highlighted – ready to be changed

![image](images/pg67_1.jpg)

![image](images/7p.jpg)Now, type a new file name (“copy”, for instance), then hit **Return** to rename the file as copy.txt – the file extension .txt remains

![image](images/8p.jpg)Right-click on the renamed file and choose **Cut** from the context menu

![image](images/9p.jpg)Navigate back into the Documents folder, then right-click on the file browser window and choose **Paste** from the context menu – depositing the renamed file

![image](images/10p.jpg)Drag the mouse pointer across both files, then right-click and choose **Move to Trash** to delete the files

![image](images/pg67_2.jpg)

![image](images/pg67_3.jpg)

![image](images/hot.jpg)

You can right-click in the file browser and choose **Create New Folder** from the context menu to add a new directory – but remember that this should be within your home directory hierarchy.

![image](images/hot.jpg)

To recover a trashed file, click the **Trash** icon on the file browser’s sidebar (or the one on the Desktop), right-click the file icon, then choose the **Restore** option from the context menu.

**Creating Shortcuts**

![image](images/pg68_1.jpg)

It is often convenient to create Desktop shortcuts to the apps and files you access most frequently. Shortcuts for apps can be created from options on the Menu, or from the Desktop context menu. Shortcuts for files can be created as links using the file browser:

![image](images/1p.jpg)Right-click an app icon on the Menu, then click the **Add to desktop** option to place a shortcut on the Desktop

![image](images/pg68_2.jpg)

![image](images/pg68_3.jpg)

![image](images/2p.jpg)Right-click anywhere on the Desktop, then choose **Create a new launcher here** from the context menu – to open a “Launcher Properties” dialog box

![image](images/3p.jpg)Enter a shortcut Name, then click the **Browse** button to open a “Choose a command” dialog

![image](images/4p.jpg)Navigate to the /usr/bin directory and select the app for which you want to create a shortcut – to add its path in the Command field

![image](images/pg68_4.jpg)

![image](images/pg68_5.jpg)

![image](images/5p.jpg)Click the icon button to open a “Choose an icon” dialog

![image](images/hot.jpg)

A shortcut or a link can be deleted in the same way as a file – select its icon then hit the **Delete** key. Alternatively, right-click on the icon then choose **Delete** or choose **Move to Trash**.

![image](images/forget.jpg)

The /**usr** directory contains sub-directories storing programs that can be run by any user.

![image](images/6p.jpg)Next, enter **gnome-character-map** in the Search box, then choose an appropriate shortcut icon in the right pane

![image](images/pg69_1.jpg)

![image](images/7p.jpg)Click the **Select** button to close the dialog and see the icon appear in the “Launcher Properties” dialog

![image](images/8p.jpg)Click the **OK** button to place a shortcut on the Desktop

![image](images/pg69_2.jpg)

![image](images/pg69_3.jpg)

![image](images/9p.jpg)Open the file browser in your home Documents directory, then right-click on a text file and choose the **Edit**, **Make Link** menu – a shortcut icon now appears in that directory and has an arrow denoting it to be a link

![image](images/pg69_4.jpg)

![image](images/10p.jpg)Drag the link icon from the file browser and drop it onto the Desktop to create a shortcut that can be clicked to launch a Text Editor displaying the target file

![image](images/pg69_5.jpg)

![image](images/forget.jpg)

If a selected icon does not appear in the **Launcher Properties** dialog it will not appear on the shortcut – a default icon will appear.

![image](images/snake.jpg)

Care must be taken to maintain links, as changes to the target file, such as renaming or moving it, will leave the links “orphaned” – no longer pointing correctly at the target file.

**Locating Files**

It is important to recognize that many directories in Linux contain hidden sub-directories and hidden files containing configuration data. These are like the “System” files that are hidden by default in the Windows operating system. In Linux, the name of each hidden directory and file always begins with a dot.

![image](images/pg70_1.jpg)

![image](images/pg70_2.jpg)

![image](images/1p.jpg)Open the file browser in your home directory

![image](images/2p.jpg)Now, click **View**, **Show Hidden Files** to see all contents

![image](images/pg70_3.jpg)

![image](images/hot.jpg)

Right-click on the file browser window then select **Arrange Items** from the context menu to choose how you would like the contents arranged.

![image](images/pg70_4.jpg)

The easiest way to find a file on your system is with the “Search” box in the Nemo file browser. You can find all files of a particular file type by entering a file extension into the Search box. For example, enter txt to find all files with a “.txt” file extension.

Conversely, you can find all files of a known name regardless of the file extension by entering a name into the Search box. The file browser begins searching as soon as you enter three characters into the Search box, so you don’t need to know the full name, and the letters need not be the first three letters of the name – just three consecutive letters within the name. You can substitute the * wildcard character for unknown letters too. The search is not case-sensitive, so the results will include uppercase and lowercase matches to the name (or part-name) that you enter:

![image](images/1p.jpg)Open the file browser in your home directory

![image](images/2p.jpg)Click the ![image](images/pg71_1.jpg)Search button on the toolbar

![image](images/3p.jpg)Type three characters into the Search box to match a file name or sub-directory within your home directory

![image](images/pg71_2.jpg)

![image](images/hot.jpg)

You can click the **Favorites** button to save or forget searches, and right-click it to display saved favorites to quickly make a search again.

![image](images/pg71_4.jpg)

![image](images/4p.jpg)Type three characters in the Search box to match any file type whose file extension ends with “pg”

![image](images/pg71_3.jpg)

![image](images/forget.jpg)

The Search results will not include hidden files.

**Understanding Permissions**

In Linux, each file and directory has an “Owner” – generally, this is the user who created it. The Owner has full permission to read the file, write to the file, and to execute the file (if it’s executable).

![image](images/pg72_1.jpg)

The Owner may also set permissions to specify if other users can read, write, and execute the file. The file’s accessibility can be restricted to the Owner, or to a “Group” of which the owner is a member, or to any user of the system (“Others”).

Permission settings of a file can be found on the Permissions tab of its Properties dialog:

![image](images/1p.jpg)Right-click on a file, then choose the **Properties** item from the context menu – to launch the “Properties” dialog

![image](images/pg72_2.jpg)

![image](images/hot.jpg)

You can select the **Emblems** tab to add a symbol to the file icon – for example, denoting the file as important.

![image](images/2p.jpg)Click on the **Permissions** tab to view the current settings

![image](images/pg72_3.jpg)

![image](images/hot.jpg)

Here, the **Owner** and **Group** have “Read and write” permission, but **Others** have “Read-only” permission.

![image](images/hot.jpg)

When a user account is created, a **Group** of the same name is also created – of which that user is a member.

Usually the Owner, Group and Others will have permission to at least read the file. If you are the owner of the file, the Owner will have permission to write – and to execute the file if it’s executable.

As the owner of the file you can use the arrowed buttons to change the access permissions of this file:

![image](images/3p.jpg)Click the arrowed button in the “Others” field, then choose **None** from the drop-down menu to restrict access to the Owner and Group members

![image](images/pg73_1.jpg)

![image](images/hot.jpg)

Checking this option makes the file executable for those users who have permission to access it.

![image](images/4p.jpg)Click on the **Open With** tab if you would also like to change the default app that opens this file

![image](images/pg73_2.jpg)

![image](images/forget.jpg)

Changing the default app is applied to all files of this file type, whereas changing permissions is applied to this file only. Here, the change will make LibreOffice Writer the default app to open all plain text files instead of the Text Editor app.

![image](images/forget.jpg)

If you need to change permissions on files where you are not the owner, you need root superuser status – see [here](#chapter10.xhtml_sec78) for details.

**Summary**

•The Linux **file system** comprises a number of standard directories arranged hierarchically beneath the **/** system root.

•Data files created by a user should only be stored in the **/home** directory structure – in the user’s **home** directory.

•A user can navigate around the file system graphically using the **Nemo file browser** app.

•An individual **file** can be copied, moved, renamed, and deleted with the file browser.

•Desktop launcher shortcuts are easily created by selecting the **Add to desktop** option on the Menu.

•The “Launcher Properties” dialog can create shortcuts to apps.

•A shortcut to a local file can be created as a **link**, which is merely a reference to the target file.

•Care must be taken to avoid orphaning links when the target file gets moved or renamed.

•It is important to recognize that many Linux directories contain **hidden** sub-directories and files.

•Hidden files and directories always have names that begin with a **.** (period) character.

•The **View**, **Show Hidden Files** menu in the file browser allows all content to be seen.

•Files can be located using the file browser’s **Search** box to match file names or file extensions.

•The owner of a file can specify access permissions to allow the **Owner**, **Group**, and **Others** to read, write, and execute.

5

**Engaging the Internet**

***This chapter demonstrates popular Linux apps for your online activities.***

[**Browsing the Web**](#chapter05.xhtml_sec34)

[**Customizing Firefox**](#chapter05.xhtml_sec35)

[**Exchanging Email**](#chapter05.xhtml_sec36)

[**Chatting Online**](#chapter05.xhtml_sec37)

[**Downloading Content**](#chapter05.xhtml_sec38)

[**Getting More Apps**](#chapter05.xhtml_sec39)

[**Summary**](#chapter05.xhtml_sec40)

**Browsing the Web**

![image](images/pg76_1.jpg)

Most Linux distros include the open-source Mozilla Firefox web browser. This popular free browser is available for various platforms and is highly customizable. It has been developed by the open-source community from original Netscape browser source code into a strongly standards-compliant product:

![image](images/1o.jpg)Ensure you are connected to the internet, then click **Menu**, **Internet**, **Firefox Web Browser** to launch the web browser at its “Start Page”

![image](images/pg76_2.jpg)

![image](images/2o.jpg)Click the **+ New Tab** button to open a new tab containing a Search box and links to “Top Sites”

![image](images/pg76_3.jpg)

![image](images/hot.jpg)

You can enter a URL in the address bar and hit **Return** to visit a web page. The address bar is also a Search box for the Yahoo! search engine.

![image](images/hot.jpg)

The **Save to Pocket** feature lets you save web pages so you can view them later on any device.

![image](images/3o.jpg)Search for an item of interest, such as “How solar cells work”, then select a link from the results to visit the page

![image](images/pg77_1.jpg)

![image](images/4o.jpg)Next, click the **Reader view** button on the toolbar to see the page without distractions

![image](images/pg77_2.jpg)

![image](images/5o.jpg)Now, click the **Add bookmark** button on the toolbar, then choose the **Bookmarks Toolbar** folder option

![image](images/pg77_3.jpg)

![image](images/6o.jpg)Click the **Done** button to see the item now appear on a “Bookmarks Toolbar” so you can revisit the page

![image](images/pg77_4.jpg)

![image](images/forget.jpg)

The **Reader view** button is not available for all web pages, but when visible it toggles between views. Click it to return to the regular page view.

![image](images/hot.jpg)

Click the **Show sidebars** button and choose the **Bookmarks** option to see your bookmarks appear in the sidebar.

**Customizing Firefox**

![image](images/pg78_1.jpg)

The interface of the Firefox web browser is highly customizable and you can install “add-ons” for extra functionality:

![image](images/1o.jpg)Right-click on the toolbar, then choose the **Customize** option on the context menu – to open a “Customize Firefox” window

![image](images/pg78_2.jpg)

![image](images/2o.jpg)Drag any item onto the toolbar to add it, or drag an item onto the Customize Firefox menu to remove it

![image](images/pg78_3.jpg)

![image](images/hot.jpg)

You can also drag items onto the **Overflow Menu**, which you can access later by clicking the toolbar’s **>>** button.

![image](images/pg78_8.jpg)

![image](images/3o.jpg)Click the **Themes** button and choose from the “My Themes” list of installed themes, or click on **Get More Themes** to install additional themes

![image](images/pg78_4.jpg)

![image](images/4o.jpg)See your chosen theme instantly applied to the Firefox interface

![image](images/pg78_5.jpg)

![image](images/hot.jpg)

Click the **Toolbars** button to add or remove more toolbars, and click the **Density** button to adjust the size of the toolbar icons.

![image](images/pg78_6.jpg)

![image](images/pg78_7.jpg)

![image](images/5o.jpg)Next, click the **Manage** button on the My Themes list to open an “Add-ons Manager” window

![image](images/pg79_1.jpg)

![image](images/6o.jpg)Enter the name of an add-on into the Search box, such as “Adblock Plus”, then hit the **Enter** key

![image](images/pg79_2.jpg)

![image](images/7o.jpg)Select the link for “Adblock Plus” on the Search results page, then click the **Add to Firefox** button to install it

![image](images/pg79_3.jpg)

![image](images/8o.jpg)Now, click **Add** to give permissions and install the add-on into Firefox

![image](images/pg79_4.jpg)

![image](images/forget.jpg)

You can also use the Add-ons Manager to remove add-ons later.

![image](images/hot.jpg)

**Adblock Plus** is a top-rated free add-on with over 11 million users. It automatically blocks advertisements and puts a button on the Firefox toolbar. This displays the number of ads blocked and provides options to allow non-intrusive ads.

**Exchanging Email**

![image](images/pg80_1.jpg)

Many Linux distros include the popular Thunderbird email app. The first time Thunderbird gets started it offers you a new email account or the option to use an existing email account. Typically, you will need to supply the name of your ISP’s mail servers (POP and SMTP), and your email address and password. When this is complete, and you have an internet connection, you can start sending and receiving email messages:

![image](images/1o.jpg)Click **Menu**, **Internet**, **Thunderbird Mail**, then click the **Get Messages** button on Thunderbird’s toolbar

![image](images/2o.jpg)Expand the folders list in the left-hand pane, then click the **Inbox** to see received messages in the top right-hand pane

![image](images/pg80_2.jpg)

![image](images/hot.jpg)

Thunderbird is also a contact manager. Right-click this “From” field and choose **Add to Address Book** then click the **Address Book** button on the toolbar to see your contacts list.

![image](images/3o.jpg)Click on a received message in the top right-hand pane to see its contents appear in the bottom right-hand pane

![image](images/4o.jpg)To write a message, click the **Write** button on the toolbar to open a “Write” window – as seen opposite

![image](images/5o.jpg)In the Write window’s **From** field, select the account from which to send the message

![image](images/6o.jpg)In the **To** field, type the email address you are sending to

![image](images/7o.jpg)In the **Subject** field, type a short message title

![image](images/hot.jpg)

The POP (**P**ost **O**ffice **P**rotocol) server handles incoming emails, and the SMTP (**S**imple **M**ail **T**ransfer **P**rotocol) server handles outgoing emails.

![image](images/8o.jpg)Now, type your message in the main window

![image](images/9o.jpg)Use the options on the formatting bar to adjust the font, layout, content, and insert a **Smiley face** emoji

![image](images/pg81_1.jpg)

![image](images/hot.jpg)

Click this button to insert various content directly into your message.

![image](images/pg81_4.jpg)

![image](images/10o.jpg)To add an attachment, click the **Attach** button on the toolbar to launch the “Attach File(s)” dialog

![image](images/11o.jpg)Navigate to the file and click the **Open** button

![image](images/pg81_2.jpg)

![image](images/12o.jpg)Check the message for spelling errors by clicking the **Options**, **Check Spelling** menu

![image](images/13o.jpg)Click the **Send** button on the toolbar to send the message

![image](images/pg81_3.jpg)

![image](images/hot.jpg)

The **Edit**, **Preferences** menu in the main “Write” window allows you to edit all kinds of Thunderbird settings for composition, security, and much more.

**Chatting Online**

![image](images/pg82_1.jpg)

Linux distros typically include a cross-platform instant messaging application. Linux Mint includes the free open-source HexChat IRC (**I**nternet **R**elay **C**hat) app. This can be used to chat about Linux and other topics on the “freenode” IRC network:

![image](images/1o.jpg)Click **Menu**, **Internet**, **HexChat** to launch the app – connecting to the “Official Linux Mint Support Channel”

![image](images/pg82_2.jpg)

![image](images/2o.jpg)Next, click the **HexChat**, **Network List** menu option – to open the “Network List” dialog

![image](images/pg82_3.jpg)

![image](images/3o.jpg)Enter a **Nick name** and a **User name**, then select the “freenode” network

![image](images/4o.jpg)Now, click the **Connect** button – to connect to the “freenode” network

![image](images/pg82_4.jpg)

![image](images/5o.jpg)Once connected, enter the command /join ##Linux in the HexChat text field – to join freenode’s Linux Support Channel

![image](images/pg83_1.jpg)

![image](images/forget.jpg)

If the “User List” is not visible, click the **View**, **User List** menu options to make it appear.

![image](images/hot.jpg)

The **Nick name** will be your name visible in the IRC channels and the **User name** is your identity to the server.

![image](images/6o.jpg)Enter comments or questions in the HexChat text field to chat with other users connected to this channel

![image](images/7o.jpg)Double-click on any user in the **User List** to switch to a “Dialog with” window to chat directly with that user

![image](images/8o.jpg)Click the **Chat** button to send a chat request to that user

![image](images/9o.jpg)Wait until the user accepts the request, then begin to chat

![image](images/pg83_2.jpg)

![image](images/pg83_3.jpg)

![image](images/hot.jpg)

You can click the **Send** button to send a file to the user, and click the **WhoIs** button to see user connection details.

![image](images/pg83_4.jpg)

**Downloading Content**

![image](images/pg84_1.jpg)

Linux distros typically include the Transmission BitTorrent Client app to acquire content via the BitTorrent protocol. This lets you download directly from other groups of people – in which each person is called a “peer”. Pieces of content from various peers are automatically assembled, making the BitTorrent protocol very efficient and reliable, particularly for large content files.

The Transmission BitTorrent Client first requires you to download a “torrent file” containing information about the content you wish to acquire. These can be found in a BitTorrent directory such as Public Domain Torrents (publicdomaintorrents.info), Internet Archive ([archive.org](http://www.archive.org)), or Legit Torrents (legittorrents.info):

![image](images/1o.jpg)Open the **Firefox** web browser and visit a BitTorrent directory, then select an item you would like to download

![image](images/pg84_2.jpg)

![image](images/2o.jpg)Choose to save the torrent file – by default to the **Downloads** folder within your home directory

![image](images/pg84_3.jpg)

![image](images/3o.jpg)Click **Menu**, **Internet**, **Transmission** to launch the app

![image](images/4o.jpg)Click the **Open** button on the Transmission toolbar – to open an “Open a Torrent” dialog

![image](images/pg84_4.jpg)

![image](images/hot.jpg)

Torrent downloads are often associated with illegal downloads, but free open content can be legally downloaded.

![image](images/hot.jpg)

The first time you launch the **Transmission** app a dialog will appear in which you need to agree to share content responsibly.

![image](images/5o.jpg)Select the torrent file you downloaded and check the **Show options dialog** option

![image](images/pg85_1.jpg)

![image](images/6o.jpg)Click the **Open** button – to open a “Torrent Options” dialog

![image](images/pg85_2.jpg)

![image](images/hot.jpg)

You can download multiple torrents simultaneously and click here to set each one’s priority to **Low**, **Normal**, or **High**.

![image](images/7o.jpg)Check the **Download** and **Start when added** options

![image](images/8o.jpg)Click the **Open** button to start downloading the content

![image](images/pg85_3.jpg)

![image](images/hot.jpg)

Click the **Edit**, **Preferences** menu to specify how your downloads should be managed.

**Getting More Apps**

![image](images/pg86_1.jpg)

In addition to the apps that are supplied with your Linux distro, there are many more free apps that can be easily installed. The Linux Mint distro includes a Software Manager utility app that lets you search for more apps by name or by category. When you select an app, there is a description and screenshot accompanied by user reviews that help you decide if you want to install that app:

![image](images/1o.jpg)Click **Menu**, **Administration**, **Software Manager** to launch the utility

![image](images/2o.jpg)Click a category button for the type of app you are seeking – for example, to find a picture editor app, click the **Graphics** button

![image](images/pg86_2.jpg)

![image](images/forget.jpg)

If you know the name of the app you can use the Search box to find it.

![image](images/3o.jpg)Click any item listed in your chosen category to see a description and reviews of that app

![image](images/pg86_3.jpg)

![image](images/pg87_1.jpg)

![image](images/hot.jpg)

You can click this link to open the app’s Home page in your web browser and discover more about the app.

![image](images/hot.jpg)

See [here](#chapter10.xhtml_sec79) for more on installing apps.

![image](images/4o.jpg)Click the **Install** button if you decide you want this app

![image](images/5o.jpg)Enter your password to download and install the app

![image](images/pg87_2.jpg)

![image](images/6o.jpg)Now, click **Menu**, **Graphics** to see a launcher has been added into the appropriate category

![image](images/pg87_3.jpg)

![image](images/hot.jpg)

The description page of an installed app has a **Remove** button (in place of the **Install** button) that you can click to uninstall that app.

![image](images/pg87_4.jpg)

**Summary**

•The **Mozilla Firefox** web browser is included with most Linux distros.

•The **+ New Tab** button in Firefox opens a new tab containing a Search box and links to “Top Sites”.

•Firefox provides **Reader view** to hide page distractions.

•Firefox web browser is highly customizable and allows the installation of **add-ons** for extra functionality.

•Many Linux distros include the **Thunderbird** app with which to send and receive email messages.

•The **formatting bar** in Thunderbird allows you to adjust the font, layout, and content, and to insert emojis in your message.

•The **Thunderbird** email app is also a contact manager.

•Linux Mint includes the **HexChat** cross-platform instant messaging app.

•The **Official Linux Mint Support Channel** is available to chat about Linux topics.

•The **Transmission** app can download content using the BitTorrent protocol.

•Transmission requires a **torrent file** containing information about the content to be acquired.

•Pieces of content from various **peers** are automatically assembled, making the BitTorrent protocol very efficient.

•Linux Mint includes a **Software Manager** utility app that groups available apps by category.

•Software Manager provides a **description** and **reviews** of each available app.

•The Software Manager app can **Install** and **Remove** apps from the system.

6

**Producing with Office**

***This chapter describes the productive apps within the free LibreOffice suite.***

[**Creating Documents**](#chapter06.xhtml_sec41)

[**Exporting Documents**](#chapter06.xhtml_sec42)

[**Creating Spreadsheets**](#chapter06.xhtml_sec43)

[**Creating Presentations**](#chapter06.xhtml_sec44)

[**Creating Visualizations**](#chapter06.xhtml_sec45)

[**Running Macros**](#chapter06.xhtml_sec46)

[**Adding Interaction**](#chapter06.xhtml_sec47)

[**Handling Data**](#chapter06.xhtml_sec48)

[**Summary**](#chapter06.xhtml_sec49)

**Creating Documents**

The LibreOffice suite that is included with most Linux distros contains a set of office tools similar to those in Microsoft Office: word processor, spreadsheet, and presentation programs, together with a program to create charts, graphs and diagrams, and a database app. If you are familiar with Microsoft Office you will feel instantly at home with the LibreOffice equivalents.

![image](images/pg90_1.jpg)

Most importantly, LibreOffice contains file filters that allow it to work with standard Microsoft Office documents from Word, Excel and PowerPoint. Files can be saved in Microsoft Office file formats, as well as formats native to LibreOffice, and objects (OLE objects, plugins, video, applets, charts) can be embedded within a document in much the same way as in Microsoft Word:

![image](images/1bl.jpg)Click **Menu**, **Office**, **LibreOffice Writer** to launch a word processor with a new blank document open

![image](images/pg90_2.jpg)

![image](images/2bl.jpg)Type some content in the new document

![image](images/pg90_3.jpg)

![image](images/hot.jpg)

LibreOffice is forked from OpenOffice, which was based on original code from the StarOffice application by Sun MicroSystems. Sun made the code freely available for development by the open-source community – so LibreOffice has no proprietary ties.

![image](images/hot.jpg)

There are versions of LibreOffice for Linux, Mac and Windows – all available for free download at [libreoffice.org](http://www.libreoffice.org)

![image](images/3bl.jpg)Click the **Edit**, **Select All** menu item (or press **Ctrl** + **A**) to select all content, then choose a font from this drop-down list on the toolbar

![image](images/pg91_1.jpg)

![image](images/hot.jpg)

The Writer interface shown here contains the **Standard** toolbar and **Formatting** toolbar.

![image](images/4bl.jpg)Select the heading text then use these toolbar buttons to modify the font height, font weight and font color

![image](images/5bl.jpg)Click the **Insert**, **Image** menu item to launch an “Insert Image” dialog, then choose an image file to add to the document at the current cursor position

![image](images/6bl.jpg)Click on the image and drag it to position it over the text body, then drop it to see the text automatically wrap around

![image](images/pg91_2.jpg)

![image](images/hot.jpg)

Notice that an **Image** toolbar automatically replaces the Formatting toolbar when an image is selected. Double-click the image to open an “Image” dialog where you can adjust the **Wrap** spacing, and much more.

![image](images/7bl.jpg)Click **File**, **Properties** to open a “Properties” dialog where you can add a document description and security options

**Exporting Documents**

![image](images/pg92_1.jpg)

When saving documents from the LibreOffice word processor, the default file format used is the ODF (**O**pen **D**ocument **F**ormat) Text format (.odt). Many alternative file formats are available, however, so your documents can be made compatible with Microsoft Office:

![image](images/1bl.jpg)Click **File**, **Save** (or press **Ctrl** + **S**) to launch the “Save” dialog, then type a document name in the **Name** field

![image](images/2bl.jpg)Click the arrowed file type button to open a list of possible formats in which to save the document – choose the format **Word 2007-365 (.docx)**

![image](images/3bl.jpg)Choose a location at which to save the document, such as your Documents folder, then click the **Save** button

![image](images/pg92_2.jpg)

![image](images/4bl.jpg)If a “Confirm File Format” dialog appears, click the button to confirm you wish to save using the .docx file format – the file is then saved at the chosen location

![image](images/pg92_3.jpg)

![image](images/hot.jpg)

In the **Save** dialog you don’t need to include a file extension in the Name field – it gets added automatically.

LibreOffice Writer has built-in support for the PDF (**P**ortable **D**ocument **F**ormat) format. This allows you to create read-only versions of your documents in the popular PDF format, without any additional software. The PDF format maintains the style and content of the original document in a very compact file that can be easily transferred around networks and the internet:

![image](images/5bl.jpg)Click **File**, **Export As**, **Export as PDF** to open a “PDF Options” dialog

![image](images/6bl.jpg)Select **All** for the “Range” option, then click the **Export** button to create a PDF version of the document – with the same file name but with a .pdf file extension

![image](images/7bl.jpg)Copy the documents created in LibreOffice on Linux to a Windows system for comparison in Microsoft Word

![image](images/pg93_1.jpg)

![image](images/pg93_2.jpg)

![image](images/forget.jpg)

The uneditable PDF version maintains its appearance precisely, but the editable DOCX version may substitute a different font if the original is not also installed in Windows – more importantly, both versions maintain color and layout formatting.

**Creating Spreadsheets**

![image](images/pg94_1.jpg)

The spreadsheet app that is part of the free LibreOffice suite provides the powerful ability to perform calculations on data entries using given formulas. It also allows spreadsheets to be saved in the format compatible with Microsoft Excel (.xlsx):

![image](images/1bl.jpg)Click **Menu**, **Office**, **LibreOffice Calc** to launch the spreadsheet app with a new blank spreadsheet open

![image](images/2bl.jpg)Enter some row and column headings, then use the **Font** **Color** button to accent their purpose

![image](images/pg94_2.jpg)

![image](images/3bl.jpg)Drag over all cells that will contain data, then right-click and choose **Format Cells** from the context menu – to open a “Format Cells” dialog

![image](images/4bl.jpg)Choose the **Currency** category in the dialog, then click the dialog’s **OK** button to apply the selection

![image](images/pg94_3.jpg)

![image](images/5bl.jpg)Enter numerical values in all cells for each week row and day column – each value is treated as a currency amount

![image](images/hot.jpg)

You can choose cell colors, fonts, borders, alignment, and more in the **Format Cells** dialog.

![image](images/6bl.jpg)Drag the mouse across each day cell on a row and its “Total” cell, then click the **∑** button on the toolbar and select **SUM** – a SUM formula appears in the formula field and a row total value appears in the Total cell

![image](images/7bl.jpg)Repeat the previous step for each row and column

![image](images/pg95_1.jpg)

![image](images/8bl.jpg)Type =AVERAGE in an “Average” cell at a row end and hit **Return**, then drag across the day cells on that row and hit **Return** again – a row average appears in the Average cell

![image](images/9bl.jpg)Repeat the previous step for each row and column

![image](images/pg95_2.jpg)

![image](images/10bl.jpg)Click **File**, **Save** (or press **Ctrl** + **S**) to launch the “Save” dialog, then type a spreadsheet name in the **Name** field

![image](images/11bl.jpg)Click the arrowed file type button to open a list of possible formats in which to save the spreadsheet – accept the default ODF Spreadsheet format (.ods) or choose the format **Excel 2007-365 (.xlsx)**

![image](images/hot.jpg)

You can use the ![image](images/pg95_3.jpg) **Background Color** button to accent the purpose of each cell.

![image](images/hot.jpg)

You can open this file in Excel on a Windows system to see that all formatting and formula functions are preserved.

**Creating Presentations**

The presentation app that is part of the free LibreOffice suite provides the ability to easily produce great slideshows. It also allows presentations to be saved in the format compatible with Microsoft PowerPoint (.ppt).

![image](images/pg96_1.jpg)

![image](images/1bl.jpg)Click **Menu**, **Office**, **LibreOffice Impress** to launch the app with a new blank presentation open

![image](images/2bl.jpg)A “Select a Template” dialog should also appear when you launch the app – select a template, such as **Lights**

![image](images/pg96_2.jpg)

![image](images/3bl.jpg)Select how you want the content grouped from an option in the “Layouts” pane, such as **Title and 2 Content**

![image](images/pg96_3.jpg)

![image](images/hot.jpg)

If the “Select a Template” dialog does not appear when you launch the app, click the **File**, **Close** menu to close the blank presentation, then select **Templates** in the “backstage” window.

![image](images/hot.jpg)

If the “Layouts” pane is not immediately visible, click **View**, **Slide Layout** to make it appear.

![image](images/4bl.jpg)Click on the “Click to add Title” box, then type a title

![image](images/pg97_1.jpg)

![image](images/5bl.jpg)Click **Format**, **Align**, **Center** to position the title

![image](images/6bl.jpg)Next, type some narrative text in the left “Click to add Text” box

![image](images/7bl.jpg)Click on the right “Click to add Text” box, then click **Insert**, **Image** to launch an “Insert Image” dialog

![image](images/8bl.jpg)Choose an appropriate image to add to the slide, then use the grab handles around the image to adjust its size to your liking

![image](images/pg97_2.jpg)

![image](images/9bl.jpg)Right-click this slide in the “Slides” pane, then choose **New Slide** to add a slide with the same template and layout – make further slides to complete the presentation

![image](images/pg97_3.jpg)

![image](images/10bl.jpg)Click **Slideshow**, **Start from First Slide** (or press **F5**) to run the presentation

![image](images/11bl.jpg)Click **File**, **Save** (or press **Ctrl** + **S**) to launch the “Save” dialog, then type a presentation name in the **Name** field

![image](images/12bl.jpg)Click the arrowed file type button to open a list of possible formats – accept the default ODF Presentation format (.odp) or choose **PowerPoint 2007-365 (.pptx)**

![image](images/snake.jpg)

You can switch to “Master Slide View” where you can add elements you want to appear on all slides. Slides you have created are not visible when in Master Slide View, so it looks like they have disappeared. Click **View**, **Normal** to continue working on your slides.

![image](images/hot.jpg)

If the “Slides” pane is not immediately visible, click **View**, **Slide Pane** to make it appear.

**Creating Visualizations**

![image](images/pg98_1.jpg)

The LibreOffice suite includes an accomplished drawing tool that can be launched from any LibreOffice app to quickly create drawings, charts, diagrams and graphs:

![image](images/1bl.jpg)From any LibreOffice app, click **File**, **New**, **Drawing** or click **Menu**, **Office**, **LibreOffice Draw** to launch the app

![image](images/2bl.jpg)Click the arrowed button beside the **Basic Shapes** button on the Drawing toolbar, then choose the rounded rectangle object from the selection offered

![image](images/pg98_2.jpg)

![image](images/3bl.jpg)Drag the mouse in the drawing area to create a rectangle and press **Ctrl** + **C** to copy the object, then press **Ctrl** + **V** five times to paste five more rectangles on top of the first

![image](images/4bl.jpg)Drag the rectangles to separate areas, then click the ![image](images/pg98_3.jpg) **Connector** button on the Drawing toolbar

![image](images/5bl.jpg)Click on a rectangle, then drag to another rectangle to create connecting lines

![image](images/6bl.jpg)Now, click the ![image](images/pg98_4.jpg) **Insert Text box** button and label the rectangles

![image](images/pg98_5.jpg)

![image](images/hot.jpg)

If the Drawings toolbar is not immediately visible, click **View**, **Toolbars**, **Drawing** to make it appear.

![image](images/forget.jpg)

Drawings can be saved in the native ODF (**O**pen **D**ocument **F**ormat), Drawing format (**.odg**), or exported in a variety of image formats such as PNG (**.png)**, GIF (**.gif)**, and SVG (**.svg)**.

![image](images/7bl.jpg)Click the **Insert**, **Chart** menu to add a default bar chart to the drawing area – a chart Formatting toolbar also appears

![image](images/pg99_1.jpg)

![image](images/8bl.jpg)On the Formatting menu, click the ![image](images/pg99_2.jpg) **Data Table** button and modify the default values in the “Data Table” dialog that appears, then close that dialog

![image](images/9bl.jpg)Click the ![image](images/pg99_3.jpg) **Chart Type** button to launch a “Chart Type” dialog, then choose **Line** in the left-hand pane and **Points and Lines** as the type of chart

![image](images/pg99_4.jpg)

![image](images/10bl.jpg)Click the **OK** button to close the “Chart Type” dialog and apply the chosen line style

![image](images/pg99_5.jpg)

![image](images/hot.jpg)

The chart Formatting toolbar can be launched from the **View**, **Toolbars**, menu – after you have inserted a chart.

![image](images/hot.jpg)

To insert an existing chart into a document, click **Insert**, **Object**, **OLE Object** – but to insert the default editable chart, just click **Insert**, **Chart**.

**Running Macros**

![image](images/pg100_1.jpg)

A “macro” is a recorded sequence of keystrokes that are stored with a given name. Running a macro replays the sequence, writing into the current document. This is particularly useful for recreating frequently-typed text within spreadsheets in LibreOffice Calc and within text documents in LibreOffice Writer:

![image](images/1bl.jpg)Launch Writer, then click **Tools**, **Options**, **LibreOffice**, **Advanced** and check the **Enable macro recording** option

![image](images/pg100_2.jpg)

![image](images/2bl.jpg)Next, click **Tools**, **Macros**, **Record Macro** to begin recording – a small window appears, bearing a **Stop Recording** button

![image](images/pg100_3.jpg)

![image](images/3bl.jpg)Click the ![image](images/pg100_4.jpg) **Center** button on the toolbar, then type your address

![image](images/pg100_5.jpg)

![image](images/4bl.jpg)Click the **Stop Recording** button in the small window, then see a “Basic Macros” dialog appear

![image](images/5bl.jpg)In the **Macro Name** text field, replace the name “Main” by the name “Address”, then click the **Save** button

![image](images/hot.jpg)

A Java Runtime Environment (JRE) is required on the Linux system to run macros. Linux Mint includes the OpenJDK Runtime Environment for Java, but you may need to install a Java Runtime Environment on other distros.

![image](images/6bl.jpg)To run this macro at any time, first click **Tools**, **Macros**, **Run Macro** to launch a “Macro Selector” dialog

![image](images/7bl.jpg)Select the Address macro from **My Macros**, **Standard**, **Module1**, then click the **Run** button to write your address

![image](images/pg101_1.jpg)

![image](images/pg101_2.jpg)

![image](images/8bl.jpg)To edit this macro, click **Tools**, **Macros**, **Edit Macros** to launch a “My Macros” dialog, then select the Address macro to see the code behind the macro actions

![image](images/pg101_3.jpg)

![image](images/9bl.jpg)Locate the text values describing your address, then replace them with different values and click **File**, **Save** to apply the changes

![image](images/10bl.jpg)Finally, repeat Steps 6 and 7 to run this macro once more and see the modified address values written

![image](images/pg101_4.jpg)

![image](images/forget.jpg)

The macro recorder only records actions relating to document content in the window where it was started, and it only works with the LibreOffice Writer and Calc apps.

![image](images/hot.jpg)

Click on **Tools**, **Macros**, **Organize Macros**, **LibreOffice Basic**, then select an existing macro and use the **Delete** button to remove it.

**Adding Interaction**

![image](images/pg102_1.jpg)

LibreOffice apps allow interactive “form” controls to be added to documents – much like those found in web forms. These allow the user to quickly produce a finished document by providing minimal input, and this is particularly useful when repeatedly producing the same document with differing data:

![image](images/1bl.jpg)In LibreOffice Writer, click **View**, **Toolbars**, **Form Controls** to open a “Form Controls” dialog, then click its **Design Mode** button to set it to “On” – so form controls can be added

![image](images/pg102_2.jpg)

![image](images/2bl.jpg)Click the **Label Field** button on the “Form Controls” dialog, then drag the mouse on the document to create three labels – by default, these will each contain the text “Label Field”

![image](images/pg102_3.jpg)

![image](images/3bl.jpg)Double-click on each label in turn to open its “Properties” dialog, and change the value of each **Label** property, then hit **Return** to see the label text change

![image](images/pg102_4.jpg)

![image](images/4bl.jpg)Click the ![image](images/pg102_5.jpg) **Text Box** button on the controls dialog, then drag the mouse on the document to create two text boxes

![image](images/hot.jpg)

Right-click on a control, select **Position and Size** from the context menu, and choose **Anchor**, **To Paragraph** from the dialog that appears to allow easier positioning of the control.

![image](images/5bl.jpg)Click the **Date Field** button in the “Form Controls” dialog, then drag the mouse to create a date field box

![image](images/pg103_1.jpg)

![image](images/6bl.jpg)Double-click the date field box to open its “Properties” dialog, then set its **Drop-down** property to “Yes” and its **Date Format** property to “Standard (long)”

![image](images/7bl.jpg)Now, click the **Design Mode** button to set it to “Off ”, then enter data in the text boxes and use the **Drop-down** menu to choose a date

![image](images/pg103_2.jpg)

![image](images/8bl.jpg)Save the file, then click **File**, **Export As**, **Export as PDF** to create a version that can be sent to others

![image](images/pg103_3.jpg)

![image](images/forget.jpg)

The data entered into form fields can be edited later to produce new completed forms.

**Handling Data**

![image](images/pg104_1.jpg)

The LibreOffice suite includes a database app that, like Microsoft Access, lets you store data and easily extract specific items of data:

![image](images/1bl.jpg)Click **Menu**, **Office**, **LibreOffice Base** to launch the app, then select “Create a new database” and click **Finish** – to open a “Save” dialog

![image](images/2bl.jpg)Enter a **Name**, then click **Save** to close the dialog

![image](images/3bl.jpg)Select **Tables**, then click **Use Wizard to Create Table** – to open a “Table Wizard” dialog

![image](images/pg104_2.jpg)

![image](images/4bl.jpg)Choose the **Personal** category, then select a **Sample table** – to see the available fields within that table

![image](images/pg104_3.jpg)

![image](images/5bl.jpg)Click an available field, then click the **>** button to move it to the **Selected fields** pane – to include it in your table

![image](images/6bl.jpg)Select all the fields you want, then click **Finish** to close the dialog and see a “Table Data View” window appear

![image](images/hot.jpg)

The **Design View** and **Create View** options offer greater control but the **Wizard** is simpler.

![image](images/hot.jpg)

You can limit fields to accept only particular types of data in the **Set types and formats** step. By default, a field can accept up to 100 characters of text.

![image](images/7bl.jpg)Enter and save your data, then close the window

![image](images/pg105_1.jpg)

![image](images/8bl.jpg)Select **Queries**, then click **Use Wizard to Create Query** – to open a “Query Wizard” dialog

![image](images/9bl.jpg)Click the **>>** button to select all fields, then click **Next**

![image](images/10bl.jpg)**Select Search conditions**, then choose a field to query

![image](images/pg105_2.jpg)

![image](images/11bl.jpg)Enter a value to match within the chosen field, then click the **Finish** button – see that a query icon gets added in the app’s “Queries” pane

![image](images/12bl.jpg)Double-click the query icon to see the results in a “Table Data View” window – extracting only specific data

![image](images/pg105_3.jpg)

![image](images/hot.jpg)

There is a “Report Wizard” that can quickly produce a summary of your data.

![image](images/forget.jpg)

You can specify other conditions, such as **Greater than** for numerical values, and you can specify multiple conditions for finer-precision queries.

![image](images/hot.jpg)

There is also a “Form Wizard” that can quickly produce a user form for data entry.

**Summary**

•**LibreOffice** contains a set of office tools similar to those in the Microsoft Office suite.

•Files can be saved in **Microsoft Office file formats** and file formats native to LibreOffice apps.

•LibreOffice **Writer** is a word processor app for documents that can contain text and embedded objects.

•LibreOffice Writer has built-in support for the **Portable** **Document Format (PDF)**.

•LibreOffice **Calc** is a spreadsheet app that can perform calculations on data entries using given formulas.

•LibreOffice Calc provides a **Format Cells** facility to specify how cell content should appear.

•LibreOffice **Impress** is a presentation app that can produce slideshows.

•LibreOffice Impress provides a number of standard **Templates** and offers many standard **Layouts**.

•LibreOffice **Draw** is a drawing app that can create illustrations, charts, diagrams, and graphs.

•LibreOffice Draw provides a **Chart Type** facility that provides many standard charts.

•A **macro** is a recorded sequence of keystrokes that can be replayed to repeat those keystrokes.

•LibreOffice apps can add **form controls** to a document for interaction with the user.

•LibreOffice **Base** is a database app that can store data and retrieve specific items of data.

•LibreOffice Base provides wizards that can create **Tables** and perform **Queries** in a database.

7

**Enjoying Media**

***This chapter describes how to enjoy media content with various popular Linux apps.***

[**Viewing Images**](#chapter07.xhtml_sec50)

[**Managing Photos**](#chapter07.xhtml_sec51)

[**Scanning Images**](#chapter07.xhtml_sec52)

[**Editing Images**](#chapter07.xhtml_sec53)

[**Watching Movies**](#chapter07.xhtml_sec54)

[**Playing Music**](#chapter07.xhtml_sec55)

[**Streaming TV**](#chapter07.xhtml_sec56)

[**Sharing Content**](#chapter07.xhtml_sec57)

[**Summary**](#chapter07.xhtml_sec58)

**Viewing Images**

![image](images/pg108_1.jpg)

Many Linux distros include the simple Image Viewer app (**xviewer**) that can zoom and scroll. In Linux Mint you can find its launcher on the menu in the Accessories category, but usually you will launch it from a right-click context menu:

![image](images/1v.jpg)Drag the mouse over image file icons to select them, then right-click and choose **Open with Image Viewer**

![image](images/pg108_2.jpg)

![image](images/2v.jpg)See the Image Viewer app launch, displaying the first image alphabetically

![image](images/pg108_3.jpg)

![image](images/hot.jpg)

You can also double-click on any file icon to instantly open that image in Image Viewer.

![image](images/hot.jpg)

You can use your mouse to zoom too. Place the cursor over an image in Image Viewer then use the mouse wheel to zoom in and out.

![image](images/3v.jpg)Click the ![image](images/pg109_1.jpg) **Forward** button to view all the selected images, or click **View**, **Slideshow** to view them full-screen

![image](images/pg109_2.jpg)

![image](images/pg109_3.jpg)

![image](images/pg109_4.jpg)

![image](images/4v.jpg)Click **View**, **Image Gallery** to open a scrollable gallery pane within the Image Viewer window

![image](images/pg109_5.jpg)

![image](images/pg109_6.jpg)

![image](images/5v.jpg)Scroll to an image, then click **File**, **Set as Wallpaper** to make that image your Desktop background

![image](images/pg109_7.jpg)

![image](images/hot.jpg)

A full-screen slideshow displays each image for five seconds, but you can change this with **Edit**, **Preferences**, **Slideshow**. Click **Esc** to quit a running slideshow.

![image](images/hot.jpg)

You can convert images to different file formats using the image gallery. Press **Ctrl** + **A**, to select all images in the gallery, then click **File**, **Save As** and choose the preferred file format in the dialog.

![image](images/pg109_8.jpg)

**Managing Photos**

![image](images/pg110_1.jpg)

In addition to the simple Image Viewer app described [here](#chapter07.xhtml_sec50), Linux Mint includes the Pix viewer app that enables you to arrange images and photos in catalogs:

![image](images/1v.jpg)Click **Menu**, **Graphics**, **Pix** to launch the app, then select an image folder in the left-hand pane to see the photos inside

![image](images/pg110_2.jpg)

![image](images/2v.jpg)Hold down the **Ctrl** key, then click on photos to select them for inclusion in a catalog

![image](images/3v.jpg)Right-click and select **Tags** from the context menu – to open an “***n* files**” dialog

![image](images/pg110_3.jpg)

![image](images/4v.jpg)Enter a tag name and click “Create tag”, then click the **Save and Close** button – to tag the selected photos

![image](images/hot.jpg)

The Pix app starts in **Browser mode**. Double-click on a photo to open it in **Viewer mode**, as shown below.

![image](images/pg110_4.jpg)

![image](images/hot.jpg)

The context menu also has options for **Add to Selection**, **Add to Catalog**, and **Comment**.

![image](images/pg110_5.jpg)

Descriptive comments can be saved within a photo file as “metadata”.

![image](images/5v.jpg)Next, click the **Organize** button just above the photos – to open an “Organize Files” dialog

![image](images/pg111_1.jpg)

![image](images/6v.jpg)Select “Tag” in the drop-down menu, then click the **Execute** button

![image](images/7v.jpg)Check the **Create** option beside the tag name you have assigned to the selected photos

![image](images/pg111_2.jpg)

![image](images/8v.jpg)Click the **Save** button to create the new catalog and close the dialog

![image](images/9v.jpg)Expand **Catalogs**, **Tags** in the left-hand pane of the Pix window, then click on any catalog icon to see its photos

![image](images/pg111_3.jpg)

![image](images/hot.jpg)

You can click the **Edit File** button to see lots of quick editing options.

![image](images/pg111_4.jpg)

![image](images/hot.jpg)

The Pix app can automatically open an “Import” dialog when you connect a digital camera or memory card containing photos.

![image](images/pg111_5.jpg)

**Scanning Images**

![image](images/pg112_1.jpg)

Linux Mint includes a Document Scanner app that, as its name suggests, makes it simple to import images from a scanner:

![image](images/1v.jpg)Connect a scanner to your PC and switch the scanner on

![image](images/2v.jpg)Click **Menu**, **Graphics**, **Document Scanner** to launch the app and see it automatically identify your scanner

![image](images/pg112_2.jpg)

![image](images/hot.jpg)

The **Scan** button changes to a **Stop** button when scanning is in progress – so you can click it to abort the current scan.

![image](images/3v.jpg)Click the arrow beside the “Scan” button, then choose from the menu whether the content you want to scan is **Text** or **Image**

![image](images/pg112_3.jpg)

![image](images/4v.jpg)Now, click the **Scan** button to scan your content – see the image of the content gradually appear in the app window

![image](images/pg112_4.jpg)

![image](images/hot.jpg)

Click the ![image](images/pg112_6.jpg) button to open a menu, then select **Preferences**, **Quality** to specify resolution, brightness, and contrast settings.

![image](images/pg112_5.jpg)

![image](images/5v.jpg)Click the **Crop** button to see a frame appear over the image, then drag the frame’s edges to the desired position

![image](images/pg113_1.jpg)

![image](images/6v.jpg)Next, click the app’s **Save** button to open a “Save As” dialog, then choose a file format from this menu

![image](images/pg113_2.jpg)

![image](images/7v.jpg)Next, click the dialog’s **Save** button to import the cropped scan to an image file

![image](images/pg113_3.jpg)

![image](images/hot.jpg)

Click the ![image](images/pg113_4.jpg) button to open a menu, then select **Preferences**, **Scanning** to choose a scanner if there is more than one connected.

![image](images/pg113_5.jpg)

![image](images/hot.jpg)

Multiple scans can be made to add pages in the Document Scanner. Click the ![image](images/pg113_6.jpg) button, then choose **Reorder Pages** to see options for how to rearrange them.

![image](images/forget.jpg)

You can double-click the image file to view it in the Image Viewer app.

**Editing Images**

![image](images/pg114_1.jpg)

The primary image editing application in Linux is the GIMP (**G**NU **I**mage **M**anipulation **P**rogram) open-source app that includes over 220 plugins in a standard installation. These provide the GIMP with many of the capabilities of Adobe Photoshop but do not provide native support for CMYK colors.

The GIMP is highly configurable and has powerful scripting support. GIMP can be used to edit images and to create attractive web page graphics:

![image](images/pg114_2.jpg)

![image](images/1v.jpg)Items in the Tool Options panel change according to which tool is selected in the Toolbox panel. For example, click the ![image](images/pg114_3.jpg) Paintbrush tool in the Toolbox to see options available for that tool in the Tool Options panel

![image](images/pg114_4.jpg)

![image](images/hot.jpg)

The GIMP app is not bundled with Linux Mint by default. See [here](#chapter05.xhtml_sec39) for installation instructions.

![image](images/2v.jpg)Now, in the Toolbox, select each tool in turn to see their available options in the Tool Options panel

![image](images/3v.jpg)The Brushes, Patterns and Fonts panel has tabs for each category that display items in a scrollable window. Each tab displays the current selection for that category. For example, click the ![image](images/pg115_2.jpg) Brushes tab and select a star-shaped brush to see that shape appear on the tab

![image](images/pg115_1.jpg)

![image](images/4v.jpg)Select the ![image](images/pg115_3.jpg) Paintbrush tool in the Toolbox and click on an image in the Image Window to paint star shapes

![image](images/5v.jpg)Now, select the ![image](images/pg115_4.jpg) Pattern tab and ![image](images/pg115_5.jpg) Fonts tab in turn to examine the available items in those categories

![image](images/6v.jpg)The Layers, Channels and Paths panel has tabs that display items for each category. Each category provides a button to toggle the visibility of individual items. For example, select the ![image](images/pg115_7.jpg) Channels tab then click the ![image](images/pg115_8.jpg) eye button of the Red channel to hide all red components of the image

![image](images/pg115_6.jpg)

![image](images/7v.jpg)There are buttons at the bottom of the Layers, Channels and Paths panel that allow you to add, remove, or arrange items in each category. For example, select the ![image](images/pg115_9.jpg) Layers tab then click the ![image](images/pg115_10.jpg) Create button to open a “Create a New Layer” dialog

![image](images/8v.jpg)Enter a layer name, such as “StarLayer”, then click the **OK** button to close the dialog and see the new layer added in the Layers tab

![image](images/pg115_11.jpg)

![image](images/forget.jpg)

The GIMP can read many image file types – including PSD files produced by Photoshop.

![image](images/snake.jpg)

The results of some GIMP plugins can be less predictable than those in Photoshop for inexperienced users.

**Watching Movies**

![image](images/pg116_1.jpg)

Linux Mint includes a fast, light-weight media player app named Celluloid that can play audio and video content in many file formats including AVI, MPG, WMV, WAV, MP3, and many more. Celluloid is the default media player for audio and video files in Linux Mint:

![image](images/1v.jpg)Double-click on a video file icon to begin immediate playback of that video

or

Click **Menu**, **Sound & Video**, **Celluloid** to launch the media player app, then click **+**, **Open** and browse to a video file

![image](images/pg116_2.jpg)

![image](images/pg116_3.jpg)

![image](images/2v.jpg)Select a movie to see it immediately begin to play in the Celluloid app’s display area

![image](images/pg116_4.jpg)

![image](images/hot.jpg)

The Celluloid media player also supports subtitles.

![image](images/3v.jpg)Click the **Volume** button and drag its pop-up slider to adjust the volume level

![image](images/pg117_1.jpg)

![image](images/4v.jpg)Drag the corner of the window to change its size – see border areas appear around the movie in the display area

![image](images/pg117_2.jpg)

![image](images/hot.jpg)

You can advance a paused movie by dragging the slider, or by placing the cursor over the display area and rolling your mouse wheel.

![image](images/5v.jpg)Click the **Toggle Fullscreen** button to switch between a window and fullscreen views and see the video automatically resize

![image](images/pg117_3.jpg)

![image](images/hot.jpg)

You can click the hamburger button and choose the **Toggle Controls** option to hide or show the controls.

**Playing Music**

![image](images/pg118_1.jpg)

The Rhythmbox music player is great for playing music files and is also a podcast aggregator – and an internet radio tuner:

![image](images/1v.jpg)Click **Menu**, **Sound & Video**, **Rhythmbox** to launch the Rhythmbox app

![image](images/2v.jpg)Select **Music** in the “Library” pane, then click the **Import** button on the toolbar

![image](images/pg118_2.jpg)

![image](images/forget.jpg)

The ![image](images/pg118_5.jpg) Play button will change to a ![image](images/pg118_6.jpg) Pause button during playback.

![image](images/3v.jpg)Use the drop-down menu to choose a folder containing music files, such as a sub-folder within your **Music** folder

![image](images/pg118_3.jpg)

![image](images/4v.jpg)See Rhythmbox list the music files within the chosen folder as “tracks”

![image](images/5v.jpg)Click on the tracks in the list to select them, then click the **Import *n* selected tracks** button to make a playlist

![image](images/6v.jpg)Click the ![image](images/pg118_4.jpg) **Play** button to start playing from “Track 1” or double-click any listed track to play that track

![image](images/pg119_1.jpg)

![image](images/hot.jpg)

Right-click on a track and choose **Remove** to delete it from the playlist.

![image](images/forget.jpg)

You can also right-click on a music file icon and choose **Open with**, **Rhythmbox** to play it.

![image](images/7v.jpg)Select **Radio** in the “Library” pane and double-click one of the listed radio stations to start listening

![image](images/pg119_2.jpg)

![image](images/8v.jpg)Select **Podcasts** in the “Library” pane, then click the **Add** button on the toolbar and search for podcasts by topic

![image](images/9v.jpg)Double-click on any podcast of interest to start listening

![image](images/pg119_3.jpg)

![image](images/10v.jpg)Click the **X** button to close the Rhythmbox window, then click the **Rhythmbox** icon on the System Tray and click the **X** button in the pop-up panel to exit the app

![image](images/hot.jpg)

You can add more radio stations by clicking the **Add** button and entering a URL – use a search engine to find URLs for internet radio stations and podcasts.

![image](images/hot.jpg)

A ![image](images/pg119_5.jpg) icon gets added to the System Tray when playback begins of music, podcasts or radio. You can close the Rhythmbox window and playback will continue. Click the ![image](images/pg119_5.jpg) icon and use the controls on the panel that appears to control playback, or click its **X** button to quit playback.

![image](images/pg119_6.jpg)

**Streaming TV**

![image](images/pg120_1.jpg)

Linux Mint includes a streaming app named “Hypnotix” that supports live TV, movies and series. The app does not provide content itself but streams content from IPTV (Internet Protocol TV) providers. Hypnotix is configured by default with only one IPTV provider called “Free-TV”. This provider supplies only free, legal, publicly available content, and no adult content:

![image](images/1v.jpg)Click **Menu**, **Sound & Video**, **Hypnotix** to launch the Hypnotix app

![image](images/pg120_2.jpg)

![image](images/2v.jpg)Click the **TV Channels** panel to see a selection of streaming services, listed with flags denoting their country of origin and the number of channels they offer

![image](images/pg120_3.jpg)

![image](images/3v.jpg)Click on one of the listed services, such as “Redbox USA”, to see a scrollable alphabetical list of channels appear alongside a display area

![image](images/pg121_1.jpg)

![image](images/forget.jpg)

There are presently no Movies or Series, so those panels are inactive.

![image](images/hot.jpg)

Free-IPTV offers over 2000 legally available TV channels from all over the world.

![image](images/4v.jpg)Scroll through the list and click any channel to begin streaming its content to the display area

![image](images/pg121_2.jpg)

![image](images/5v.jpg)Place your cursor over the display area, then use the pop-up controls to pause or resume live streaming TV

![image](images/pg121_3.jpg)

![image](images/hot.jpg)

Hypnotix is a new app introduced in Linux Mint version 20.

![image](images/snake.jpg)

Your viewing experience depends on your connection speed.

![image](images/hot.jpg)

To add another IPTV provider, click the ![image](images/pg121_4.jpg) button on the launch screen, then click **Add a new provider** and enter the URL of an M3U playlist. Search online for “Free IPTV M3U Playlist”.

**Sharing Content**

![image](images/pg122_1.jpg)

You can easily send files to another Linux PC on your local network using the Warpinator app. Each computer must be running the Warpinator app in order to be detected. Additionally, they must each use the same group code and port number, set in the Warpinator app’s Preferences dialog window – by default, the group code is “Warpinator” and the port number is 42000.

![image](images/1v.jpg)Select **Menu**, **Accessories**, **Warpinator** on a locally networked PC to see the app detect another Linux PC

![image](images/pg122_2.jpg)

![image](images/pg122_3.jpg)

![image](images/2v.jpg)Click on the other detected PC to which you want to send a file – to switch into a **File Transfers** window

![image](images/3v.jpg)Next, browse to the file’s location to select a file, or drag and drop the file onto the File Transfers window

![image](images/pg122_4.jpg)

![image](images/4v.jpg)Now, click the **Send files** button – to send a request to the other PC

![image](images/forget.jpg)

The file will not be transferred until the user on the receiving PC gives their approval.

![image](images/5v.jpg)See a notification appear on the other PC describing the incoming file and requesting approval for the transfer

![image](images/pg123_1.jpg)

![image](images/6v.jpg)The user on the other PC can click **Accept** to receive the file and the transfer will be made immediately to that PC

![image](images/pg123_2.jpg)

![image](images/hot.jpg)

Select the **Preferences** item on this menu to choose file transfer options and configure the group code and port number if desired.

![image](images/7v.jpg)Received files are automatically added to Warpinator’s “save” folder on the other PC by default – click the ![image](images/pg123_3.jpg) hamburger button, then choose **Open save folder** to see all transferred files

![image](images/pg123_4.jpg)

![image](images/hot.jpg)

Warpinator is a new app introduced in Linux Mint version 20.

![image](images/snake.jpg)

Warpinator will continue running if you simply close the window. An icon is added to the System Tray that you can right-click and choose **Quit** to exit the app.

**Summary**

•The **Image Viewer** app displays images and can create a slideshow of multiple images.

•Image Viewer can make a selected image the Desktop background **wallpaper**.

•The **Pix** viewer app has a Browser mode and a Viewer mode.

•Pix viewer can arrange images and photos in a **Catalog** by grouping them with a common tag.

•The **Document Scanner** app can import images from a scanner.

•Scanned **text** and **photos** can be cropped and saved as a file.

•The GNU Image Manipulation Program (**GIMP**) is the primary image editing application in Linux.

•The GIMP app includes over 220 **plugins** that provide many of the capabilities of Adobe Photoshop.

•The **Celluloid** app can play audio and video content in many file formats.

•**Celluloid** app can play video in a window or fullscreen.

•**Rhythmbox** can import selected music files as **tracks** within a library.

•The Rhythmbox music player is also a podcast aggregator and an internet radio tuner.

•The **Hypnotix** app can stream live TV content.

•Hypnotix lists services supplied by Free-IPTV who only provide legally available channel content.

•The **Warpinator** app can transfer files to another Linux PC on your local network.

•To transfer files with Warpinator both PCs must be running Warpinator and the receiver must approve the transfer.

8

**Using Accessories**

***This chapter describes some of the useful accessory apps included with Linux Mint.***

[**Writing Text**](#chapter08.xhtml_sec59)

[**Doing Calculations**](#chapter08.xhtml_sec60)

[**Managing Archives**](#chapter08.xhtml_sec61)

[**Taking Notes**](#chapter08.xhtml_sec62)

[**Grabbing Screenshots**](#chapter08.xhtml_sec63)

[**Reading Documents**](#chapter08.xhtml_sec64)

[**Summary**](#chapter08.xhtml_sec65)

**Writing Text**

The plain text Text Editor app (**xed**) in Linux Mint is the equivalent of the Notepad app in Windows – but Text Editor has many more features. It can number lines, sort lines into alphanumeric order, and it provides syntax highlighting for a whole range of scripting, programming, and markup languages.

![image](images/pg126_1.jpg)

You must recognize, however, that Linux does not treat text line endings in the same way as Windows. Linux adds a non-printing line feed \n (“newline”) character, whereas Windows adds non-printing carriage return and line feed \r\n characters. This means that text files created in Linux do not maintain their line endings correctly when viewed on a Windows system. The Text Editor app provides an option when saving text files that lets you choose your preferred type of line endings:

![image](images/1b.jpg)Click **Menu**, **Accessories**, **Text Editor** to launch the app

![image](images/2b.jpg)Next, click **Tools**, **Autocheck Spelling** to turn the spellchecker on

![image](images/3b.jpg)Now, type in some lines of text – see the spellchecker place a red underline beneath any suspicious items

![image](images/pg126_2.jpg)

![image](images/4b.jpg)Click **Edit**, **Preferences**, **Editor**, then slide the “Display line numbers” toggle switch to the “On” position – to see the lines get numbered

![image](images/5b.jpg)Click the **Close** button, click **Edit**, **Select All** (or press **Ctrl** + **A**) to select all text, then hit the **Delete** key to remove all text

![image](images/hot.jpg)

The Notepad app in versions of the Windows 10 operating system from October 2018 supports both Linux LF (line feed) line endings, and Windows CRLF (carriage return + line feed) line endings.

![image](images/hot.jpg)

You can click **Edit**, **Sort lines** to rearrange the lines into alphanumeric order, then click **Edit**, **Undo** to revert to the original order.

![image](images/6b.jpg)Select **View**, **Highlight Mode**, **HTML** to turn on syntax highlighting for HTML markup code

![image](images/7b.jpg)Now, type in some HTML markup tags – see the elements, attributes and content appear colored

![image](images/pg127_3.jpg)

![image](images/8b.jpg)Click **File, Save As** to open a “Save As” dialog, then enter a file name and choose the **Windows** line ending option

![image](images/pg127_4.jpg)

![image](images/9b.jpg)Click the **Save** button, then copy the file to a Windows system and see the line endings are preserved

![image](images/pg127_5.jpg)

![image](images/forget.jpg)

The line numbers appear only in the Text Editor window – they are not inserted into the text.

![image](images/forget.jpg)

This file saved with Linux line endings may appear like this on older versions of Windows Notepad.

![image](images/pg127_6.jpg)

**Doing Calculations**

Linux Mint includes a Calculator app that can perform many different types of calculations and conversions. It provides a scrollable History View of your previous calculations so you can select a previous calculation to manipulate further.

![image](images/pg128_1.jpg)

There are five modes available in the Calculator app in which you can enter basic equations, execute math and financial functions, and perform conversions of currency, size, and number base:

![image](images/1b.jpg)Click **Menu**, **Accessories**, **Calculator** to launch the app in “Basic Mode”

![image](images/2b.jpg)Enter some equations to see the result and see them get added to the **History View** area

![image](images/pg128_2.jpg)

![image](images/3b.jpg)Select “Advanced Mode” from the title bar menu, then select options to convert a measured distance

![image](images/pg128_3.jpg)

![image](images/hot.jpg)

There is no limit to the number of calculations in the **History View** area.

![image](images/forget.jpg)

The **Advanced Mode** provides additional buttons that perform math functions, such as logarithm (**log**).

![image](images/4b.jpg)Select “Financial Mode” from the title bar menu, then select options to approximately convert a sum of currency

![image](images/pg129_1.jpg)

![image](images/5b.jpg)Select “Programming Mode” from the title bar menu, then select options to convert number bases

![image](images/pg129_2.jpg)

![image](images/6b.jpg)Select “Keyboard Mode” from the title bar menu, then select options to convert temperature scales

![image](images/pg129_3.jpg)

![image](images/forget.jpg)

The **Financial Mode** provides additional buttons that perform financial functions such as future value (**Fv**).

![image](images/hot.jpg)

Decimal 100 is binary **1100100**, which represents the sum of 64+32+0+0+4+0+0\. Decimal 100 is also octal **144** and hexadecimal **64**.

![image](images/forget.jpg)

The **Programming Mode** provides additional buttons that perform programming functions, such as Boolean algebra (**AND**, **OR**, **XOR**, **NOT)**.

**Managing Archives**

![image](images/pg130_1.jpg)

The Linux Mint distro includes a versatile Archive Manager app that can compress files into many archive file formats. If you choose the popular ZIP (**.zip**) format you can password-protect the archive, but this format often does not produce the smallest archive file size. You can find the Archive Manager launcher on the Menu in the Accessories category, but usually you will launch it from a right-click context menu:

![image](images/1b.jpg)Right-click on a folder you would like to compress, and choose **Compress** on the context menu – to open a “Compress” dialog

![image](images/pg130_2.jpg)

![image](images/2b.jpg)Enter an archive file name, then select the .zip archive file format

![image](images/pg130_3.jpg)

![image](images/3b.jpg)Choose a location and expand “Other Options”, then enter a password

![image](images/4b.jpg)Click the **Create** button to make an archive copy of the original folder and its contents at your chosen location

![image](images/5b.jpg)Right-click on the original folder and choose **Delete** on the context menu – to remove the folder and its contents

![image](images/snake.jpg)

Not all archive file formats support password protection.

![image](images/forget.jpg)

The archive does not replace the original folder – it is created in addition to the original.

![image](images/6b.jpg)Next, right-click on the archive file and choose **Open With Archive Manager** – to see its contents

![image](images/pg131_1.jpg)

![image](images/7b.jpg)Now, click the **Extract** button in an attempt to extract the folder and its contents

![image](images/pg131_2.jpg)

![image](images/hot.jpg)

You can check an archive for errors by choosing the **Test Integrity** option on this menu.

![image](images/pg131_6.jpg)

![image](images/8b.jpg)Enter the password for this archive, then click the **OK** button – to extract a copy of the folder and its contents

![image](images/pg131_3.jpg)

![image](images/pg131_4.jpg)

![image](images/hot.jpg)

Click the **Show the Files** button to see the folder’s contents listed in the Nemo file manager.

![image](images/9b.jpg)Click the **Close** button to exit the Archive Manager app

![image](images/10b.jpg)Create another archive of the same folder using the 7-ZIP (.7z) archive file format, and compare the file sizes

![image](images/pg131_5.jpg)

![image](images/hot.jpg)

See [here](#chapter10.xhtml_sec80) for more on archive management.

**Taking Notes**

![image](images/pg132_1.jpg)

Linux Mint includes the Gnote app that lets you keep track of small pieces of information. You can use this in much the same way as Sticky Notes on Windows, but you can also add one or more links in a Gnote note to reference your other notes, and you can group Gnote notes by topic in notebooks:

![image](images/1b.jpg)Click **Menu**, **Accessories**, **Gnote** to launch the app

![image](images/2b.jpg)Click the ![image](images/pg132_2.jpg) button, then select **New Notebook** to open a dialog

![image](images/pg132_3.jpg)

![image](images/3b.jpg)Enter a name for the notebook, such as “Web”, then click the **Create** button – see a “Web” notebook icon get added in the left-hand pane of the app

![image](images/pg132_4.jpg)

![image](images/4b.jpg)Select the new “Web” icon, then click the ![image](images/pg132_6.jpg) button to create a new note that opens in a separate window

![image](images/pg132_5.jpg)

![image](images/5b.jpg)See that by default the new note contains a colored editable heading and a black editable paragraph

![image](images/pg132_7.jpg)

![image](images/hot.jpg)

Gnote provides three default notebooks for **All** notes, **Important** notes, and **Unfiled** notes that have not been filed in any other notebook.

![image](images/6b.jpg)Edit the new note to give it a name and text content

![image](images/pg133_1.jpg)

![image](images/7b.jpg)Select some lines of text, then click the ![image](images/pg133_3.jpg) button and choose **Bullets** to make a list

![image](images/pg133_2.jpg)

![image](images/hot.jpg)

You can also change the font size and indentation options on this menu.

![image](images/8b.jpg)Next, select one of the list items, then click the ![image](images/pg133_4.jpg) button and select the **Link to New Note** option to open a new editable note

![image](images/pg133_5.jpg)

![image](images/hot.jpg)

You can select the **Important** option on this menu to file a note in the Important notebook.

![image](images/9b.jpg)Edit the new note to provide further information

![image](images/pg133_6.jpg)

![image](images/10b.jpg)Now, click the ![image](images/pg133_7.jpg) button to return to the dialog and select the “All” icon to see all your notes

![image](images/pg133_8.jpg)

![image](images/11b.jpg)Select the first note once more, then repeat steps 8-10 to add linked notes providing further information for the other list items

![image](images/pg133_9.jpg)

![image](images/hot.jpg)

Right-click on a notebook or note and choose **Delete** to remove it.

**Grabbing Screenshots**

![image](images/pg134_1.jpg)

As with the Windows operating system, in Linux Mint you can press the **Print Screen** button (**PrtSc**) to immediately capture an image of your screen or use the **Alt** + **PrtSc** key combination to immediately capture the currently-active window. Additionally, Linux Mint includes a Screenshot app that provides delay and other options – much like the Snipping Tool app in Windows:

![image](images/1b.jpg)Click **Menu**, **Accessories**, **Screenshot** to launch the app

![image](images/2b.jpg)Choose the “Grab the whole screen” option and select a delay period, then click the **Take Screenshot** button

![image](images/pg134_2.jpg)

![image](images/3b.jpg)Edit the Name and location, then click the **Save** button

![image](images/pg134_3.jpg)

![image](images/pg134_4.jpg)

![image](images/hot.jpg)

You can also click **Copy to Clipboard** and close this dialog, then paste a screenshot into the GIMP app for editing.

![image](images/forget.jpg)

Notice that some options are “grayed out” (indicating they are not available) depending on the type of screenshot you have chosen.

![image](images/4b.jpg)Relaunch the app, then choose the “Grab the current window” option

![image](images/5b.jpg)Select the “Include pointer” option, then click the **Take** **Screenshot** button

![image](images/pg135_1.jpg)

![image](images/6b.jpg)Edit the name and location, then click the **Save** button

![image](images/pg135_2.jpg)

![image](images/7b.jpg)See that the screenshot includes the cursor and any pop-up tooltips

![image](images/8b.jpg)Relaunch the app, then choose the “Select area to grab” option, then click the **Take Screenshot** button

![image](images/pg135_3.jpg)

![image](images/9b.jpg)Drag the cursor to select a rectangular area of the screen, then release the mouse button to capture that area

![image](images/10b.jpg)Edit the name and location, then click the **Save** button

![image](images/pg135_4.jpg)

![image](images/hot.jpg)

You can open the **Apply effect** drop-down menu to choose an effect when grabbing the current window.

![image](images/pg135_5.jpg)

![image](images/hot.jpg)

You can also press **Shift** + **PrtSc** to see the cursor change to a crosshair so you can select an area of the screen to grab.

**Reading Documents**

![image](images/pg136_1.jpg)

The Linux Mint distro includes the Document Viewer app (**xreader**) that is useful when reading multi-page documents such as a user guide. Typically, these types of documents are in the Portable Document Format (.pdf) that can contain annotations and are sometimes protected by a password. You can find the Document Viewer launcher on the Menu in the Accessories category, but usually you will launch it by double-clicking on a PDF document’s file icon or from a right-click context menu:

![image](images/1b.jpg)Right-click on a document file icon and choose **Open With Document Viewer** to launch the app

![image](images/pg136_2.jpg)

![image](images/2b.jpg)If an “Enter password” dialog appears, enter the password then click the dialog’s **Unlock Document** button – to see the first page of the document

![image](images/pg136_3.jpg)

![image](images/hot.jpg)

If the Side Pane is not immediately visible, click **View**, **Side Pane** to make it appear.

![image](images/3b.jpg) Click the **Forward** button to advance the pages, or click on a “Thumbnail” in the Side Pane to jump to a page

![image](images/4b.jpg)Select the “Annotations” option in the Side Pane drop-down menu, then click on its icon to see the note

![image](images/pg137_1.jpg)

![image](images/hot.jpg)

Use the **View** buttons to choose whether or not to view Continuous pages in the window, and click the **View**, **Dual** menu option to view facing pages.

![image](images/5b.jpg)Select the “Bookmarks” option in the Side Pane menu, then to mark a page, click **Bookmarks**, **Add Bookmark**

![image](images/pg137_2.jpg)

![image](images/hot.jpg)

You can click **File**, **Properties** to discover a document’s origin.

![image](images/pg137_3.jpg)

**Summary**

•The **Text Editor** app is a plain text editor that can number lines and sort lines alphanumerically.

•Text Editor can provide **syntax highlighting** for many scripting, programming, and markup languages.

•Linux does not treat text **line endings** in the same way as Windows, but Text Editor supports both types of endings.

•The **Calculator** app can perform basic equations, execute math and financial functions, and perform conversions.

•Calculator provides a scrollable **History View** of previous calculations so they can be quickly recalled.

•The **Archive Manager** app compresses files into many archive file formats.

•The **ZIP** file format supports password-protection but may not produce the smallest archive files.

•The **7-ZIP** file format produces smaller compressed archive files than the ZIP file format.

•The **Gnote** app can keep track of small pieces of information grouped in notebooks.

•**Gnote** supports **hyperlinks** to other notes.

•The **Screenshot** app can capture an image of the entire screen, current window, or a selected area.

•Screenshot provides **delay** and border options.

•The **Document Viewer** app can display multi-page documents and provide Thumbnail views of each page.

•Document Viewer supports **bookmarks** that mark a page for future reference.

•Document Viewer supports **annotations** that provide additional information on a page.

9

**Commanding the Terminal**

***This chapter introduces the power of the command-line Terminal for file management and text manipulation.***

[**Invoking the Terminal**](#chapter09.xhtml_sec66)

[**Navigating at the Prompt**](#chapter09.xhtml_sec67)

[**Operating on Directories**](#chapter09.xhtml_sec68)

[**Managing Files**](#chapter09.xhtml_sec69)

[**Examining File Properties**](#chapter09.xhtml_sec70)

[**Comparing Files**](#chapter09.xhtml_sec71)

[**Finding Files**](#chapter09.xhtml_sec72)

[**Reading Text Files**](#chapter09.xhtml_sec73)

[**Writing Text Files**](#chapter09.xhtml_sec74)

[**Manipulating Text Content**](#chapter09.xhtml_sec75)

[**Matching Text Patterns**](#chapter09.xhtml_sec76)

[**Summary**](#chapter09.xhtml_sec77)

**Invoking the Terminal**

At the very heart of the Linux operating system is a core series of machine instructions known as the “kernel” – this is a technical program that is not user-friendly, as it is mainly designed to communicate with electronic components. A Linux “shell” is a facility that allows the user to communicate via commands with the kernel in a human-readable form. It translates command-line instructions so they can be processed.

![image](images/pg140_1.jpg)

Most Linux distros include several shell programs that offer different features. The default Linux shell program, however, is called Bash (**B**ourne **A**gain **SH**ell), which is an updated version of the original Bourne shell found in the Unix operating system.

The shell understands a large number of commands, and each has a number of “options” that may (optionally) be specified to modify their behavior – usually these are prefixed by a hyphen. Many also accept “arguments” that provide data to be used by the command. The typical syntax of a shell command looks like this:

*command -option argument*

Shell commands can be executed at a prompt in a Terminal window on a graphical desktop interface:

![image](images/1r.jpg)Click **Menu**, **Administration**, **Terminal** (or click the ![image](images/pg140_2.jpg) launcher on the Taskbar) to launch a Terminal window

![image](images/pg140_3.jpg)

The Terminal window above displays the default bash command prompt and places the cursor after the prompt – ready to receive a command. The default prompt here comprises the current user name (mike), a separator character (@), the host PC name (linux-pc), the current directory (**~** tilde character denoting the Home directory), and a final terminating character ($).

![image](images/hot.jpg)

You can learn more about **bash** commands with the companion book in this series Bash in easy steps. Visit **[www.ineasysteps.com](http://www.ineasysteps.com)** for more information on this book.

![image](images/snake.jpg)

Options are not standardized – the same option can have different meanings for different commands.

You can confirm the current user and host PC name at any time with the whoami and hostname commands:

![image](images/2r.jpg)Type the **whoami** command at a prompt, then hit **Return**

![image](images/3r.jpg)Now, type the **hostname** command and hit **Return** again

![image](images/pg141_1.jpg)

![image](images/forget.jpg)

Commands use lowercase only – in uppercase the command will not be recognized.

Some commands call upon individual programs that reside on your system – for example, the clear command that removes previous content from the Terminal. Others are “builtin” commands that are built in to the shell itself – for example, the exit command that quits the shell and closes the Terminal window. You can determine whether a command is a builtin using the type command and the command’s name as its argument:

![image](images/4r.jpg)Type **clear** and hit **Return** to remove the previous content, then enter **type clear** and hit **Return** again to discover the location of the clear command program

![image](images/5r.jpg)Enter **type exit** and hit **Return** to discover that the exit command is a shell builtin instruction, then type the exit command and hit **Return** to quit the shell

![image](images/pg141_2.jpg)

![image](images/hot.jpg)

Type a **--help** argument (two hyphens & “help”) after any command, then hit **Return**, to see a list of options for that command.

**Navigating at the Prompt**

When you start a shell session you are, by default, located in your home directory of the Linux file system. You can switch to any directory to which you have access permission by stating its absolute address as the argument to the cd command. Similarly, you can return to your home directory by stating its absolute address as the argument to the cd command, or using its tilde alias with the command cd ~.

![image](images/pg142_1.jpg)

For shorter hierarchical moves, the command cd .. moves up one level to the parent directory of the current directory. Stating just the name of an immediate sub-directory as the argument to the cd command moves down one level to that sub-directory:

![image](images/1r.jpg)Launch a shell window then enter the pwd command at the prompt to print the current working directory

![image](images/2r.jpg)Enter the combined command cd /etc ; pwd to switch to the /etc directory and confirm it as the working directory

![image](images/3r.jpg)Next, enter the combined command cd ~ ; pwd to return to the home directory and confirm the location

![image](images/4r.jpg)Enter the combined command cd .. ; pwd to switch to the parent directory and confirm the location

![image](images/5r.jpg)Now, enter the combined command cd mike ; pwd to switch to the named sub-directory and confirm it

![image](images/pg142_2.jpg)

![image](images/snake.jpg)

There must be space between the command and its argument.

![image](images/forget.jpg)

Replace **mike** with your own username in the combined command.

The contents of the current directory can be revealed using the ls command to display a list of its files and immediate sub-directories. This is a comprehensive command that has many useful options:

•Use the -a option to see all directory contents – including hidden files and hidden sub-directories.

•Use the -l option to see long format listing for each item – including user and group ownership names.

•Use the -t option to sort the contents by the time they were created or last modified.

•Use the -o option to suppress group ownership details.

•Use the -g option to suppress user ownership details.

![image](images/hot.jpg)

Directory names that contain spaces must be enclosed within quotation marks when specified as a command argument – to avoid truncation of the name.

Options can be combined to produce a complex option where each parameter is applied:

![image](images/6r.jpg)Enter the command cd “My Topics” to move to an immediate sub-directory whose name contains a space

![image](images/7r.jpg)Next, enter the ls command to simply list all its contents

![image](images/8r.jpg)Enter the command ls -altog to list all contents including hidden files, in long format, listed by modification time – but with user and group details suppressed

![image](images/pg143_3.jpg)

![image](images/forget.jpg)

All absolute directory addresses begin with a “/” character – as they descend from the / root location.

**Operating on Directories**

It is sometimes useful to be able to extract the name of a file, program or directory from the end of a path address using the basename command. Conversely, you can use the dirname command to remove the final part of the path address to a file – leaving just the path to its parent directory.

![image](images/pg144_1.jpg)

A new directory can be created in the current working directory by specifying a directory name of your choice as the argument to the mkdir command. Alternatively, a new directory can be created elsewhere by specifying a full path as the argument:

![image](images/1r.jpg)To discover the location of the bash program that is the default shell, at a prompt enter the command echo $SHELL

![image](images/2r.jpg)Issue a basename $SHELL command to extract the program name from the path address

![image](images/3r.jpg)Issue a dirname $SHELL command to extract the parent directory of the bash program name from the path

![image](images/4r.jpg)Enter the command mkdir Sub1 to create a directory named “Sub1” in the current working directory

![image](images/5r.jpg)Enter the command mkdir /home/mike/Data/Sub2 to create a directory named “Sub2” using an absolute path address

![image](images/pg144_2.jpg)

![image](images/forget.jpg)

The **basename** and **dirname** commands simply manipulate the path string – they do not implement any action.

Directories can be removed in the shell using the rmdir command. This takes the directory name as its argument and will instantly remove an empty directory, but will simply warn you that the directory is not empty if it contains files.

Having to delete files manually, one by one, may provide safeguards but can be tedious. An intelligent alternative is available by using the recursive interactive -ri option of the rm command. This steps inside the directory and examines every file – requesting your confirmation before deleting each file. When all files have been deleted it then asks if you want to delete the directory:

![image](images/6r.jpg)Launch the Text Editor using the xed command, and create three text files in the “Sub2” directory

![image](images/7r.jpg)Issue the command rmdir Sub1 to remove the empty “Sub1” directory

![image](images/8r.jpg)Now, issue the command rmdir Sub2 to attempt to remove the non-empty “Sub2” directory

![image](images/9r.jpg)Enter the command rm -ri Sub2 to interactively delete the files within the “Sub2” directory, and remove the directory itself, by replying “Y” (yes) to each question

![image](images/pg145_1.jpg)

![image](images/hot.jpg)

You can use a **-v** option with both the **rmdir** command and the **rm** command to produce verbose output – describing what is happening.

![image](images/snake.jpg)

If you’re feeling brave, and are absolutely certain that the directory contains nothing you will miss, you can use the **rm** command with just a **-r** option to instantly delete a directory and its entire contents – use with care!

**Managing Files**

The shell mv command lets you easily move files around your Linux system from the command line. This command requires two arguments stating the name of the file to be moved, and the destination to which it should be moved. Interestingly, the mv command can also be used to rename a file by stating its current name and a new name as its two arguments.

![image](images/pg146_1.jpg)

If you wish to copy rather than move a file to a new location, the cp command can be used. This command can accept one or more files to be copied as its arguments, stating the destination as the final argument:

![image](images/1r.jpg)Launch a shell Terminal window, then enter an ls command to see the contents of the current directory

![image](images/2r.jpg)Issue an mv command to rename an existing file – for example, from “alpha.txt” to “zebra.txt” with mv alpha. txt zebra.txt – and an ls command to confirm the name change

![image](images/3r.jpg)Enter mv zebra.txt Box to move the renamed file to a Box sub-directory – and an ls command to see it’s gone

![image](images/4r.jpg)Enter cp some.txt Box to copy a file named “some.txt” to the same sub-directory

![image](images/5r.jpg)Issue an ls command with the name of the sub-directory – confirming a file was moved and a file was copied

![image](images/pg146_2.jpg)

![image](images/hot.jpg)

Use the **-i** option with the **mv** command to prompt before overwriting a file of the same name.

The rm command can be used to delete one or more files named as its arguments. The * wildcard can also be used to delete all files in a directory – if you are absolutely certain none are needed.

You can create hard links, pointing to the system address of a file, and soft (symbolic) links, storing the path to a file, with the ln command. By default, this will create a hard link to the file named as its argument – use its -s option to create a symbolic link.

![image](images/snake.jpg)

The wildcard ***** character means “all” and should be used with caution.

The readlink command can be used to discover the target to which a symbolic link is pointing:

![image](images/6r.jpg)Enter rm Box/zebra.txt to delete a file in a sub-directory and an ls Box command to confirm it’s gone

![image](images/7r.jpg)Enter ln Box/some.txt hardlink to create a hard link named “hardlink” to a file in the sub-directory

![image](images/8r.jpg)Now, enter ln -s Box/some.txt softlink command to create a soft link named “softlink” to the same file

![image](images/9r.jpg)Enter an ls command to see both links have been created in the home directory

![image](images/10r.jpg)Enter a readlink softlink command to see the target to which the soft link points

![image](images/pg147_1.jpg)

![image](images/hot.jpg)

If you delete the target file a hard link will retain a copy of the file’s content, but a soft link will simply point to a target that no longer exists.

![image](images/forget.jpg)

You can find more details on shortcut links [here](#chapter04.xhtml_sec30).

**Examining File Properties**

The Linux shell provides many commands that can be used to examine attributes of any file. The most comprehensive is the stat command that lists every important attribute of the file stated as its argument.

![image](images/pg148_1.jpg)

If you just want to discover the file size, use the du disk usage command with its -b option to count the number of bytes.

Use the wc word count command to quickly discover how many newlines, words, and bytes a text file contains, or assess what type of file it is with the file command:

![image](images/1r.jpg)Enter stat Box/some.txt to discover the attributes of a file named “some.txt” in a Box sub-directory

![image](images/2r.jpg)Enter du -b Box/some.txt to discover the size of this file in byte units

![image](images/3r.jpg)Enter wc Box/some.txt to discover that file’s line count, word count, and byte count

![image](images/4r.jpg)Now, enter file Box/some.txt and file Box/tux.png commands to discover the file type of two files

![image](images/pg148_2.jpg)

![image](images/hot.jpg)

Use the **wc** command with its **-m** option to just see a total word count.

![image](images/pg148_3.jpg)

See that here the **wc** command reveals the number of newlines (29), words (175), and bytes (1137) of this file.

The touch command introduces some interesting possibilities, as it can create an empty file and can change the Last Accessed and Last Modified timestamp attributes of a file. Used alone, it simply updates these to the present time, but used with a -d option it allows you to specify a date in a variety of formats – specify a day number and month number to set the timestamps to midnight on that day of the current year, or specify a complete date including year and time.

![image](images/5r.jpg)Enter touch -d “12/25” more.txt to update the timestamps of a file named “more.txt” to a date in the current year

![image](images/6r.jpg)Enter a stat more.txt command to confirm the timestamps have been updated

![image](images/7r.jpg)Now, enter touch -d \ “07/04/2023 12:00” more.txt to update timestamps to the specified date, time, and year

![image](images/8r.jpg)Enter a stat more.txt command to confirm the timestamps have been updated once more

![image](images/pg149_1.jpg)

![image](images/forget.jpg)

Date numbers supplied as an argument to the touch command must be enclosed within quotes.

![image](images/pg149_2.jpg)

See that the properties indicate the date and time of the last change and the new timestamp after modification.

**Comparing Files**

The shell provides several ways to compare two files. You can check to see if two files are identical with the cmp command. If they are indeed identical, the command reports nothing, but if they differ, it reports the location of the first difference.

![image](images/pg150_1.jpg)

Text files can be compared line-by-line with the comm command. Its output is slightly unusual, as it creates three columns to indicate lines that match in each file:

•**Column 1** – lines found in the first file, but not the second.

•**Column 2** – lines found in the second file, but not the first.

•**Column 3** – lines found in both files.

![image](images/1r.jpg)Use a text editor to create a file named abc.txt, with three lines “Alpha”, “Bravo”, and “Charlie”, and a file named acd.txt with three lines “Alpha”, “Charlie” and “Delta” – save the files in the current directory

![image](images/2r.jpg)Launch a shell Terminal window and enter the command cmp abc.txt acd.txt to discover where the first difference occurs between these two files

![image](images/3r.jpg)Enter comm abc.txt acd.txt to see a line-by-line comparison

![image](images/pg150_2.jpg)

![image](images/hot.jpg)

The **cmp** command can also be used to compare binary files such as images.

![image](images/hot.jpg)

The **comm** command has options to suppress column output – the option **-12** suppresses the first two columns to show only lines that are common to both files.

The diff command offers an alternative to the comm command for comparison of text files. It too compares line-by-line, and it produces a detailed report showing any unique lines. It can also be used to compare two directories to reveal unique files.

Files may also be compared using checksum numbers to verify their integrity. Checksum numbers are often found on internet download pages so the user can ensure that a downloaded file is intact – typically, the checksum is made using the md5 algorithm.

The md5sum command produces a 32-byte checksum for the file specified as its argument, and should exactly match that stated by the originator if the file is indeed intact.

An alternative checksum can be created in much the same way by the cksum command. This generates a CRC (Cyclic Redundancy Check) value and includes the file’s byte size in the output.

![image](images/4r.jpg)Enter a diff abc.txt acd.txt command to discover those lines that are unique to each file

![image](images/5r.jpg)Now, enter md5sum abc.txt to create a checksum number for that file

![image](images/6r.jpg)Similarly, enter cksum abc.txt to create another checksum number for that file

![image](images/pg151_1.jpg)

![image](images/forget.jpg)

You can enter the command **man diff** to discover more about the diff output from its manual page.

**Finding Files**

![image](images/pg152.jpg)

Locating a file on your system can be achieved from a shell prompt using the find command. This is a very powerful command, with over 50 possible options, but it has an unusual syntax. Possibly the one most often used looks like this:

find *DirectoryName* -type f -name *FileName*

The directory name specifies the hierarchical starting point from which to begin searching. If you know the file exists somewhere in your home directory structure, you could begin searching there ( ~ ). The -type f option specifies that the search is for a file – denoted by the letter “f ”. The -name option makes the search by name – seeking the specified file name:

![image](images/1r.jpg)Enter find ~ -type f -name some.txt to seek all files named some.txt within your home directory structure

![image](images/pg152_1.jpg)

![image](images/hot.jpg)

Use the wildcard ***** with the file name when you know the name but not the extension.

By default, the find command will only report the location of actual files, but you can also have it include symbolic links in the report by adding a -L option as its very first argument:

![image](images/2r.jpg)Now, enter find -L ~ -type f -name some.txt to see the result now locate the file and a symbolic link to that file – and an error message!

![image](images/pg152_2.jpg)

![image](images/forget.jpg)

You can recall the last command entered by pressing the **Up** arrow key.

If a search result includes error messages, you can exclude error messages by appending 2>/dev/null to the command:

![image](images/3r.jpg)Enter find -L ~ \ -type f -name some.txt 2>/dev/null to seek the location of a file, report the location of any softlinks to that file, and suppress error messages

![image](images/pg153_1.jpg)

In addition to searching for files, the -type option can specify that the search is for directories – denoted by the letter “d”.

![image](images/hot.jpg)

The \ backslash in this command simply lets you continue the command on the next line. Hit **Enter** after you type the \ backslash to see a continuation prompt appear on the next line.

When searching deep directory structures, with many sub-directory levels, it is sometimes desirable to limit the depth of search with the find command’s -maxdepth option. This requires an integer argument to specify the number of levels to search:

![image](images/4r.jpg)Enter find /usr -maxdepth 1 -type d to report only those directories that are direct descendants of the /usr directory

![image](images/pg153_2.jpg)

![image](images/hot.jpg)

The **/usr** directory has many levels – remove the **-maxdepth 1** option from the command in Step 4 and run the command again to see all directories.

**Reading Text Files**

![image](images/pg154_1.jpg)

The simplest way to view a text file in the shell is with the cat command. Just state one or more files to view as its arguments and it will display their content, concatenating the text together. Viewing one or two small text files will fit comfortably in a single window so you will see the entire text. Larger files, however, will exceed the space in a single window so you will only see the final part of the text. The solution is to send the text stream to the less command via the “|” pipe operator. This means that the text is displayed one screen at a time, starting from the beginning:

![image](images/1r.jpg)At a shell prompt, enter cat quote1.txt quote2.txt to display the content of two text files on standard output

![image](images/pg154_2.jpg)

![image](images/2r.jpg)Now, type cat ballad.txt | less then hit **Return** to display the file contents in less mode – in which a “:” prompt appears below the content text where you can enter special **less** mode commands to display selective text

![image](images/pg154_3.jpg)

![image](images/hot.jpg)

You can use a **-n** option with the **cat** command to number each line on standard output.

![image](images/hot.jpg)

The “less” facility offers many great options – press the **H** key in less mode to see them all.

![image](images/3r.jpg)Use the **Page Up** and **Page Down** keys to scroll through the text in less mode, then press the > key to skip to the end of the text and hit the Q key to quit less mode

The head command lets you preview the first 10 lines of a text file, and its companion tail command lets you preview the final 10 lines – great for skipping to the end of a long log file.

You can also display text with added line numbers using the nl number line command that provides useful control over numbering. Its -v option specifies an integer at which to start numbering, and its -b t option numbers only non-empty lines.

![image](images/4r.jpg)Enter the command **tail ballad.txt** to preview the last 10 lines of text within the file (including empty lines)

![image](images/5r.jpg)Now, enter nl -v 0 -b t ballad.txt | head to preview the first 10 lines of text – numbered starting at zero, and numbering only non-empty lines

![image](images/pg155_1.jpg)

![image](images/forget.jpg)

The shell pipeline technique allows the output from any command to be redirected as input for another command.

**Writing Text Files**

![image](images/pg156_1.jpg)

The classic Linux shell program for creating and editing text files is the compact vi application that is also found on Unix systems:

![image](images/1r.jpg)Type vi at a shell prompt, then hit **Return** to open the text editor in the shell window at its “splash screen”

![image](images/pg156_2.jpg)

The vi (vim) editor displays a tilde character at the beginning of each empty line. You cannot enter any text initially, as vi opens in “command mode” where it will attempt to interpret anything you type as an instruction:

![image](images/2r.jpg)Press the **Insert** key to change to “insert mode” where text can be input

![image](images/3r.jpg)In insert mode, type some text into the vi editor – the splash screen information disappears as you begin typing

![image](images/pg156_3.jpg)

![image](images/4r.jpg)To save your text as a file, first hit the **Esc** key to exit “insert mode”, switching vi to “command mode”

![image](images/snake.jpg)

The **vi** editor does not have automatic word wrap at line ends – it will wrap mid-word unless you hit **Return** to wrap a word manually.

![image](images/hot.jpg)

In command mode you can enter a **dd** command to delete the line where the cursor is currently positioned.

![image](images/5r.jpg)Type a “:” colon to begin a vi command – a colon character appears at the bottom-left corner of the editor

![image](images/6r.jpg)Now, type a lowercase “w” (for “write”) followed by a space and a name for the text file – simple.txt, for example

![image](images/7r.jpg)Hit the **Return** key to write the file – in the current directory by default

![image](images/8r.jpg)Type a “:q” vi command then hit **Return** to close vi and return to a regular shell prompt

![image](images/pg157_1.jpg)

![image](images/hot.jpg)

Using **vi** needs a little practice. Some distros, such as Linux Mint and Ubuntu, ship with other text editors – try typing “nano” at a prompt to launch an alternative text editor app.

You can launch vi and open a file for editing in one single action by typing vi at a prompt, followed by a space and the file name:

![image](images/9r.jpg)At a shell prompt, enter the command vi simple.txt to re-open the text file in the vi editor

![image](images/pg157_2.jpg)

![image](images/forget.jpg)

To edit a file opened in vi you need to first hit the **Insert** key to enter insert mode.

**Manipulating Text Content**

![image](images/pg158_1.jpg)

The shell cut and paste commands may not be what you expect. They work with text arranged in columns, delimited by an invisible tab character. Each column of text is known as a “field” and the cut command can specify which field to display – for instance, the option -f3 chooses the third column from the left. The paste command is the opposite of the cut command, combining columns from multiple files for display horizontally:

![image](images/1r.jpg)Use vi to create two text files “nums.txt” and “vegs.txt”, each with two columns of text separated by tab characters

![image](images/2r.jpg)Enter cat nums.txt vegs.txt to display the file contents vertically, one above the other

![image](images/3r.jpg)Now, enter paste nums.txt vegs.txt to display the file contents horizontally, side-by-side

![image](images/4r.jpg)Enter cut -f2 vegs.txt to just display the contents from the second column of one file

![image](images/pg158_3.jpg)

Simple text transformations can easily be made by piping a text stream to the **tr** command. This requires two arguments to specify what to change, and how it should be changed. For instance, the command tr a “*” changes all occurrences of the letter “a”, replacing each one with an asterisk on standard output.

![image](images/hot.jpg)

Use a **-T** option with the **cat** command to display the invisible tab characters as “^I” on standard output.

![image](images/pg158_2.jpg)

![image](images/forget.jpg)

Multiple fields can be specified as a commaseparated list, like **-f1,3** or as a range such as **-f2-4**.

Typically, the tr command is used to transform capitalization on output. The sort command is often used at the end of a pipeline to display lines of text sorted alphabetically. It can also be used to order lines numerically if a -n option is used. The tee command is useful in a pipeline that ends with a sort instruction to write the text stream as a file before sorting. The file name is specified by the argument to the tee command and the file is created in the current directory:

![image](images/5r.jpg)Enter cat quote3.txt ; \ cat quote3.txt | tr “a-z” “A-Z” to display the contents of a file named “quote1.txt” – both in its original format and after transformation to uppercase

![image](images/6r.jpg)Enter cut -f2 vegs.txt | sort to just display the contents of a second column, sorted alphabetically

![image](images/7r.jpg)Now, enter cut -f2 vegs.txt \ | tee vegs-column2.txt | sort to save a second column as a text file before displaying it sorted alphabetically on standard output

![image](images/8r.jpg)Finally, enter cat vegs-column2.txt to display the file

![image](images/pg159_1.jpg)

![image](images/snake.jpg)

Remember that the sequence of characters specified to the **tr** command must be enclosed in quotes.

![image](images/hot.jpg)

Use a **-a** option with the **tee** command to append text to a file, rather than overwriting previous text.

**Matching Text Patterns**

![image](images/pg160_1.jpg)

The grep command is one of the most useful of all commands. It has many possible options, but its purpose is simply to display all lines from a text file that contain a specified string or pattern. A grep command can specify a string to seek as its first argument, and a file name in which to search as its second argument:

![image](images/1r.jpg)At a shell prompt, enter grep sword ballad.txt to display all lines in this text file that contain the word “sword”

![image](images/pg160_2.jpg)

Notice that the output above has two duplicate lines. The sort command can be used to reorder lines – to make duplicate lines appear in succession – and duplicated successive lines can be removed with the uniq command. Output from the grep command can be piped to a sort command to make the duplicate lines successive, then piped to uniq so only unique lines remain:

![image](images/2r.jpg)Enter grep sword ballad.txt \ | sort | uniq to display all unique lines in this text file that contain the word “sword”

![image](images/pg160_2.jpg)

The look command is useful to quickly output all lines of text from a file that begin with a specified prefix. It can accept a -d option to only seek to match alphanumeric characters.

![image](images/hot.jpg)

The **grep** command can also match regular expressions. For instance, **grep [Y] ballad.txt** would output all lines that have an uppercase Y. See the **grep** man page for more on regular expressions.

![image](images/3r.jpg)Enter look -d Y ballad.txt to see a list of lines beginning with the letter “Y” from this file, ignoring spaces and tabs

![image](images/pg161_1.jpg)

![image](images/hot.jpg)

You can also use the **look** command with a string argument to see a list of words starting with that string – taken from an editable dictionary file that is normally located at **/usr/share/dict/words**.

The aspell program is a powerful spellchecker that has a -c option that lets you interactively check a file for spelling errors. This highlights possible errors and suggests alternatives that you can choose to replace or ignore each highlighted word in turn:

![image](images/4r.jpg)Enter aspell -c ballad.txt to begin the spellchecker for this text file

![image](images/5r.jpg)Type the number against a suggested replacement to immediately replace the highlighted word with it

![image](images/pg161_2.jpg)

![image](images/forget.jpg)

Press the **I** key to ignore a word, the **R** key to type your own replacement, or the **X** key to exit the **aspell** spellchecker.

**Summary**

•The whoami command reveals the user name, hostname reveals the host PC name, clear empties the shell window, and exit terminates the shell session.

•The pwd command reveals the current working directory and the directory location can be changed with the cd command.

•The ~ tilde character is an alias for the home directory and any directory’s content can be revealed by the ls command.

•The basename command returns the last part of an address, whereas the dirname command returns just the first part.

•New directories are created with the mkdir command, and empty directories can be removed by the rmdir command.

•Files are moved or renamed with the mv command, copied with the cp command, and removed with the rm command.

•The ln command is used to create hard links and soft links, but the readlink command can only be used with soft links.

•The stat command lists all file properties, du reports the file size, and the file command reports the file type.

•Timestamps of a file can be modified by the touch command, and the wc command can be used to report the word count.

•Files can be compared with cmp, comm, and diff commands, and checksums generated by the cksum and md5 commands.

•The find command locates a file, grep locates a string within a file, and look locates lines beginning with a given letter.

•Files can be viewed using the cat command, lines numbered with nl, and spelling checked by the aspell command.

•The head command displays the first 10 lines of a file, whereas the tail command displays its final 10 lines.

•The vi editor can be used to create text files and individual text columns manipulated by the cut and paste commands.

•A shell pipeline directs output to be used as input for another command and can include tee to write a file, tr to transform the output, and sort to order the output alphanumerically.

10

**Performing Operations**

This chapter demonstrates how to perform useful operations with the Linux command-line shell app.

[**Becoming the Superuser**](#chapter10.xhtml_sec78)

[**Installing Packages**](#chapter10.xhtml_sec79)

[**Handling Archives**](#chapter10.xhtml_sec80)

[**Examining File Systems**](#chapter10.xhtml_sec81)

[**Working with Accounts**](#chapter10.xhtml_sec82)

[**Setting Access Permissions**](#chapter10.xhtml_sec83)

[**Controlling Processes**](#chapter10.xhtml_sec84)

[**Exploring the Network**](#chapter10.xhtml_sec85)

[**Printing from the Shell**](#chapter10.xhtml_sec86)

[**Evaluating Expressions**](#chapter10.xhtml_sec87)

[**Scripting the Shell**](#chapter10.xhtml_sec88)

[**Summary**](#chapter10.xhtml_sec89)

**Becoming the Superuser**

A regular user can call upon many shell commands, but some are only available to a privileged “superuser”. These restricted commands typically perform system administration functions to which regular users should not be allowed instant access.

![image](images/pg164_1.jpg)

On a typical home Linux system, the default user created during installation is given access to the sudo command, which allows commands to be executed as if the regular user is the superuser.

The sudo command is most often needed where you receive a “Permission denied” message when attempting to perform an operation. Prefixing the previous command with the sudo command effectively grants the required permission. If the previous command was lengthy, you can simply issue a sudo !! command to run it again with the required sudo prefix:

![image](images/1g.jpg)At a shell prompt, enter parted /dev/sda to attempt to launch the partition editor for the hard-drive device

![image](images/2g.jpg)As the shell informs you that you are not the superuser, type **c** then hit **Return** to cancel the attempt

![image](images/pg164_2.jpg)

![image](images/3g.jpg)Now, enter sudo parted /dev/sda (or just enter sudo !!) to launch the partition editor successfully

![image](images/4g.jpg)At the (parted) prompt, enter a print command to list the partition information for the hard drive

![image](images/5g.jpg)Now, enter a help command to see the available operations that may be performed, or enter a quit command to exit the partition editor

![image](images/pg165_1.jpg)

![image](images/hot.jpg)

Storage devices (“sd”) on your system are labeled alphabetically, so the first device on your system is labeled **sda**.

![image](images/snake.jpg)

The root superuser can access any file or program on the system – with the potential to wreak havoc! Only log in as the root superuser if it’s absolutely essential.

To assume superuser status in order to perform system administration, the sudo command can be used together with the su (switch user) command. This makes you the “root” user, with system-wide access, whose home directory is the /root directory:

![image](images/6g.jpg)Issue the sudo su command, then enter your regular user password to assume superuser status

![image](images/7g.jpg)Enter cd ~ ; pwd to navigate to the root superuser’s home directory and display its location

![image](images/8g.jpg)Log out from the root superuser account by entering the exit command – to resume regular user status back in the user’s home directory

![image](images/pg165_2.jpg)

![image](images/forget.jpg)

For security, the shell displays no characters for password entries.

**Installing Packages**

The Advanced Packaging Tool (APT) is a command-line tool that automates the process of retrieving, configuring, and installing software packages. It relies upon online repositories to locate software and resolve dependencies – so that the installation package will include any libraries required by the application. Unsurprisingly, as package installation modifies your system, all APT commands must be run using sudo for superuser privileges.

![image](images/pg166_1.jpg)

The APT’s apt-get command has several options with which to manage packages. It’s useful to first execute an apt-get update command to update the list of available repository packages, before issuing an apt-get install *package-name* command.

Once installed, a package can be upgraded to the latest version with an apt-get upgrade *package-name* command.

After a package has been installed it can be removed later using an apt-get remove package-name command – but this retains the configuration files for that package. For complete removal of a package and its configuration files, you can instead use the command apt-get --purge remove *package-name*.

![image](images/1g.jpg)Enter the sudo apt-get update command to ensure the package list is up-to-date

![image](images/2g.jpg)Now, issue a command to install a package – for example, enter sudo apt-get install gnome-mahjongg (note gg ending) to install a graphical tiles game package

![image](images/pg166_2.jpg)

![image](images/3g.jpg)Some packages request confirmation before installation that requires you to type Y and hit Return if you are happy to proceed, or enter N to cancel the installation

![image](images/pg167_1.jpg)

![image](images/hot.jpg)

Use **apt-cache search *package-name*** to locate an installed or available package.

![image](images/hot.jpg)

Use man apt-get to see the full range of options.

After the packages are retrieved, unpacked and set up, the installation is complete and the application is ready to run:

![image](images/4g.jpg)Check the Menu to see that a new Games category containing a launch icon has been added for the newly-installed package – click **Games**, **Mahjongg** to play

![image](images/pg167_2.jpg)

![image](images/pg167_3.jpg)

![image](images/hot.jpg)

The Synaptic Package Manager is a user-friendly graphical interface for the Advanced Packaging Tool (APT) – in Linux Mint, click **Menu**, **Administration**, **Synaptic Package Manager** to launch the app.

**Handling Archives**

![image](images/pg168_1.jpg)

The traditional file compression tool in Linux uses the gzip command to compact one or more files into a single archive – adding a “.gz” file extension and replacing the original files. Its companion gunzip command can be used to extract files from an archive created with gzip – replacing the compressed archive:

![image](images/1g.jpg)Enter du-b ele* to learn the byte size of local files whose names begin “ele” – in this case, it’s one named elegy.txt

![image](images/2g.jpg)Next, enter gzip elegy.txt to create a compressed archive of that file – named with an added “.gz” file extension

![image](images/3g.jpg)Now, use a further du -b ele* command to compare the file size of the compressed **gzip** archive to the original file

![image](images/4g.jpg)Enter gunzip elegy.txt.gz to extract the original file

![image](images/pg168_2.jpg)

The modern bzip2 compression tool gets better compression than gzip but is less widely used – distributing bzip2 archives may not find universal acceptance. It works like the gzip tool, but adds a “.bz2” file extension and has a companion bunzip2 uncompressor:

![image](images/5g.jpg)Enter du -b ele* to learn the byte size of local files whose names begin “ele” – in this case, it’s one named elegy.txt

![image](images/6g.jpg)Next, enter bzip2 elegy.txt to create a compressed archive of that file – named with an added “.bz2” file extension

![image](images/7g.jpg)Now, use a further du -b ele* command to compare the file size of the compressed bzip2 archive to the original file

![image](images/forget.jpg)

A bzip2 archive file size is smaller than gzip and zip archives – notice the size of the archives in these examples.

![image](images/8g.jpg)Enter bunzip2 elegy.txt.bz2 to extract the original file – being sure to include the added “.bz2” file extension

![image](images/pg169_1.jpg)

Compressed archives created in Windows systems invariably use the zip compression format. In Linux systems their contents can be extracted by the unzip command and archives created for distribution to Windows users with the zip command. The unzip command does not delete the archive file after extraction:

![image](images/9g.jpg)Enter zip elegy.zip elegy.txt to specify the archive name and the file it should contain in compressed form

![image](images/10g.jpg)Issue another du -b ele* command to compare file sizes, then enter unzip elegy.zip to extract the archive contents

![image](images/11g.jpg)When asked, choose the “r” option, then rename the extracted file elegy.unzipped – to differ from the original

![image](images/pg169_2.jpg)

![image](images/snake.jpg)

The zip command requires the archive name as its first argument, followed by a list of files to be included in that archive.

![image](images/hot.jpg)

Use a **-c** option with **gunzip**, **bunzip2**, or **unzip** commands to display the content of compressed text files on standard output.

**Examining File Systems**

![image](images/pg170_1.jpg)

A Linux system may span multiple hard disk drives and extend across many disk partitions. Each partition is represented by a special file in the /dev directory – typically, /dev/sda1 may represent the first partition on your master hard disk drive. During installation of the Linux operating system, each partition is formatted as a persistent storage “file system” on the hard drive in which files can be stored and recalled. Similarly, media drives are formatted with their own file systems in which to store data. Media drives must be “mounted” onto the Linux file tree in order to make them accessible, and this can be achieved automatically:

![image](images/1g.jpg)Click **Menu**, **Accessories**, **Files** – to open the “Nemo” file manager

![image](images/2g.jpg)In Nemo, click **Edit, Preferences, Behavior**, then scroll down to the “Media Handling” category

![image](images/pg170_2.jpg)

![image](images/3g.jpg)Now, ensure that the option to “Automatically mount removable media when inserted and on startup” is selected

![image](images/4g.jpg)Click the **Close** button to confirm the selection and to close the “File Management Preferences” dialog

The df disk free command shows how file systems are being used by indicating free space. It has a -h option to make the output more understandable and a -T option to display file system types:

![image](images/5g.jpg)Insert a flash drive into a USB port on your device

![image](images/6g.jpg)Open a **Terminal** window, then enter the command df -hT to discover how the file system currently appears

![image](images/pg171_1.jpg)

![image](images/snake.jpg)

The df -T option (uppercase) will display file system types, whereas the df -t option (lowercase) specifies which file system types to list.

![image](images/pg171_2.jpg)

See that there are many items of the “tmpfs” type, but these are merely temporary file system storage facilities in volatile memory. Only the highlighted items identify persistent storage devices.

Here, the hard drive file systems on /dev/sda1 and /dev/sda2 were automatically mounted onto the Linux file tree during the boot process, and the media drive file system on /dev/sdb1 was automatically mounted when the flash drive was inserted into the device port. A file system can be manually unmounted using the umount command to perform maintenance on it without fear of file corruption. For instance, the root superuser can run the fsck file system check command to check for integrity and errors:

![image](images/7g.jpg)Enter umount /dev/sdb1 to unmount the file system on the USB flash drive

![image](images/8g.jpg)Now, issue the command sudo fsck /dev/sdb1 to check the USB flash drive file system for errors

![image](images/9g.jpg)When the check completes, remove the flash drive from the USB port – reinsert it into the port to mount it again

![image](images/pg171_3.jpg)

![image](images/forget.jpg)

The fsck command uses the same file system checker that is used during the boot process prior to the mount procedures – it should not be used on mounted devices.

**Working with Accounts**

![image](images/pg172_1.jpg)

User accounts are administered by the superuser. The useradd command will create a new user of a specified name, the usermod command can modify a specified user, and the userdel command can delete a specified user. A user’s login password can be changed by the passwd command. The user’s full name can be changed by the chfn command, and their default shell program can be changed by the chsh command. Each user may employ these to change their own details, or the superuser can change the user’s details. The pinky -l command will show the details of any specified user:

![image](images/1g.jpg)Enter the command sudo useradd tony and your regular user password – to create a new user named “tony”

![image](images/2g.jpg)Next, enter the command sudo usermod -l toni tony to rename the user named “tony” to “toni”, then enter the command sudo passwd toni and set a login password

![image](images/3g.jpg)Issue the command sudo chfn toni and enter the full name of this user, then issue the command sudo chsh toni and enter /bin/bash to set the bash program as the default

![image](images/4g.jpg)Enter the command pinky -l toni to see this user’s details

![image](images/pg172_2.jpg)

![image](images/snake.jpg)

Never change any aspect of the root user account. Also note that the options here for usermod and **pinky** are a lowercase L character.

![image](images/forget.jpg)

The user’s personal information details are typically more extensive than the brief details in this example – they are simplified here for brevity.

A “group” is a set of user accounts whose rights can be modified simultaneously by the superuser. For example, a group may be granted permission to access a previously inaccessible file – all users who are members of that group are then allowed access.

Any user can discover which groups they belong to with the groups command and can specify a username as its argument to reveal the group membership of one particular user. The superuser can employ the groupadd command to specify the name of a new group, or groupmod -n to change the name of an existing group, or groupdel to delete a specified group. The superuser can also add a user to an existing group with the usermod -G command – stating the group name and username as its arguments:

![image](images/5g.jpg)Enter the command groups toni to discover that this user is only a member of a group named “tony” – added when the user account was created

![image](images/6g.jpg)Enter the command sudo groupmod -n toni tony to change the group name to match the modified username

![image](images/7g.jpg)Enter sudo groupadd fund to create a new group named “fund”, then enter sudo usermod -G fund toni to make the user a member of the new group

![image](images/8g.jpg)Issue the command groups toni once more to see all groups of which this user is now a member

![image](images/pg173_1.jpg)

![image](images/hot.jpg)

Group information is typically stored in a file at /etc/group that lists all group names, together with a comma-separated list of users belonging to each group.

**Setting Access Permissions**

![image](images/pg174_1.jpg)

The ls -l long listing command reveals the access permissions of each item in the current directory as a string of 10 characters at the start of each line. The first is a d for a directory, or a dash for a file, followed by sequential Read (r), Write (w) and Execute (**x**) permissions for the owning User, Group, and Others. In the listing below, a script may be Read and Executed by everyone and the owner may also Write to it. The owner can both Read and Write a text note but others may only Read it. Three other text files may be Read or Written to only by their respective owners.

![image](images/pg174_2.jpg)

Each set of permissions can also be described numerically where Read = 4, Write = 2, and Execute = 1\. For instance, a value of 7 describes full permissions to Read, Write and Execute (4 + 2 + 1), 6 describes permissions to Read, Write (4 + 2), and so on.

Permissions can be changed at a shell prompt with the chmod command, stating the permission values and the file name as its arguments. For example, the command chmod 777 myfile sets full permissions for a file named “myfile”. You must first assume root superuser status with the sudo command if you are not the owner. The chgrp command can be used to change the group membership of a file by stating a group name and the file name as its arguments. Similarly, the chown command can specify a username and the file name to change the user ownership.

![image](images/forget.jpg)

Notice that this user is a member of the group named “fund” that was created [here](#chapter10.xhtml_access).

![image](images/hot.jpg)

See [here](#chapter04.xhtml_sec32) for more on access permissions.

![image](images/1g.jpg)Enter chmod 644 mike-notes to allow everyone to read this owned file, then enter sudo chown mike andy-notes to change ownership of that file – so this user can read it

![image](images/2g.jpg)Next, enter sudo usermod -G fund dave, to make the user “dave” a member of the group named “fund”, then enter sudo chgrp fund dave-notes to change the file’s group

![image](images/3g.jpg)Now, enter sudo chmod 640 dave-notes, to allow all exit to members of the group to read this file, then enter exit to end the Terminal session

![image](images/pg175_1.jpg)

![image](images/4g.jpg)Open the Terminal to start a new session, then issue an ls -l command to see the changes, then read the files where access was previously denied

![image](images/pg175_2.jpg)

![image](images/snake.jpg)

Do not fall into the habit of setting everything to permissions of 777 – use access permissions thoughtfully to maintain useful restrictions.

**Controlling Processes**

![image](images/pg176_1.jpg)

A Linux system has many processes running at any given time, representing open apps, shell jobs, and background services. Each process has a unique PID (**P**rocess **ID**entity) number. You can see a list of every current process with the ps -e command – or those for a particular user – with ps -u followed by the username. The process owner can terminate a process by stating its PID number as the argument to a kill command:

![image](images/1g.jpg)Open a **Terminal** window, then enter a command to begin a new process – for example, to start the ftp internet file transfer program

![image](images/pg176_2.jpg)

![image](images/2g.jpg)Next, open a second **Terminal** window, then enter the command ps -e to see a long list of all processes

![image](images/pg176_3.jpg)

![image](images/3g.jpg)Scroll down the list to find the Terminal windows listed as “pseudo terminals” named as pts/0 and pts/1

![image](images/hot.jpg)

Enter the command **man ftp** to discover more about the ftp file transfer program.

![image](images/forget.jpg)

Each PID is dynamically allocated by the operating system when a process is launched, to identify that particular process instance.

![image](images/4g.jpg)Now, enter the command ps -e | grep pts to refine the list to just the processes running in each Terminal window

![image](images/5g.jpg)See that the first number against each listed process is its PID number – the ftp program is PID 2627 in this case

![image](images/pg177_1.jpg)

![image](images/6g.jpg)Enter the command kill 2627 to terminate the ftp program process in the first window

![image](images/pg177_2.jpg)

![image](images/7g.jpg)Enter the command ps -e | grep pts once more to see the process is no longer in the list

![image](images/pg177_4.jpg)

![image](images/pg177_3.jpg)

Highlighted here are the **ftp** program process PID and the message in the first window after you issue a **kill** command.

![image](images/hot.jpg)

At a prompt you can enter the **top** command to view the most active processes – press the **Q** key to quit.

**Exploring the Network**

In much the same way that each house on a street has a unique address to which mail can be addressed for direct communication, every computer on a network has a unique number, known as its IP (**I**nternet **P**rotocol) address, which can be used to directly communicate with a particular computer.

![image](images/pg178_1.jpg)

You can discover the IP address of the computer behind a web address by stating the URL as the argument to the host command. In some cases, for large-scale websites, this may reveal multiple IP addresses:

![image](images/1g.jpg)At a shell prompt, enter host [www.google.com](http://www.google.com) to discover the IP address for that URL

![image](images/pg178_2.jpg)

![image](images/hot.jpg)

Add a **-a** option to a **host** command to see all information about that host.

The most basic test to see if another computer is reachable across the network sends tiny data packets to its IP address using the ping command. This continues sending test packets until you stop it, but you may limit the number of packets by adding a -c option stating the total number of packets to send:

![image](images/2g.jpg)Enter the command ping -c 3 216.58.209.4 to send three packets to this IP address – to see if it is reachable

![image](images/pg178_3.jpg)

![image](images/forget.jpg)

The IP address used here is one of those for the Google URL – revealed by the **host** command in Step 1.

In Linux you can discover the IP address of your own computer by issuing the ifconfig command to display the network interface configuration. If you know the connection device name, you can specify that as the argument to the ifconfig command to see an individual report. If your computer has multiple network connection devices, each one will be listed separately:

![image](images/3g.jpg)Issue a plain ifconfig command to discover the network IP address of your computer

![image](images/pg179_1.jpg)

The computer in this example has a network connection through a wireless router, with an IP address of 192.168.0.166, via a device named wlp2s0. Traditionally, the devices were named “eth0”, “eth1”, etc. for Ethernet devices and “wlan0”, “wlan1”, etc. for wireless devices, but a new naming scheme was introduced to overcome identification problems where multiple network interfaces are available on modern networks. The new naming scheme identifies the devices more specifically, to avoid confusion. With the connection above, the devices identified are Ethernet (enp3s0f2), localhost (lo), and wireless LAN (wlp2s0).

![image](images/hot.jpg)

The “lo” loopback interface is useful for testing network applications locally before live deployment.

![image](images/snake.jpg)

The **ifconfig** command only displays the status of active interfaces – add a **-a** option to include inactive interfaces.

**Printing from the Shell**

The lpr command takes a file name or path as its argument to establish a print job to send the specified file to the printer. Each job is placed in a queue awaiting transmission to the printer – when the job reaches the front of the queue, data from the file is sent to the printer and gets printed.

![image](images/pg180_1.jpg)

You can examine jobs in the print queue with the lpq command – each job is automatically assigned a job number. A job can be removed from the queue, before it gets sent to the printer, using the lprm command together with its job number:

![image](images/1g.jpg)At a shell prompt, enter lpr tux.png to create a print job – to print an image file named “tux.png”

![image](images/2g.jpg)Enter lpr ballad.txt to create another print job – to print the specified text file “ballad.txt”

![image](images/3g.jpg)Issue an lpq command to see the current print queue

![image](images/pg180_2.jpg)

The print queue reveals that the printer is actively printing job number 1 – the image file.

![image](images/4g.jpg)Before print job number 1 completes, issue the command lprm 2 (or alternatively, the command cancel 2) to remove that job from the print queue

The printer removes that job while continuing to print the image file – the text file in job number 2 is not sent to the printer, so does not get printed.

![image](images/hot.jpg)

A print job can only be removed from the print queue by its owner or the root superuser.

Printing from a shell prompt is not restricted to simply printing files – data can also be queued for printing using the lpr command together with the | pipe character:

![image](images/5g.jpg)Enter ls -l /etc | lpr to print a list of the /etc directory – by piping results of an ls command to the lpr command

![image](images/6g.jpg)While the list is printing, issue an lpq command to see the print queue source is piped from standard input

![image](images/pg181_1.jpg)

The ability to print in Linux is provided by the CUPS (**C**ommon **U**nix **P**rinting **S**ystem) facility. This provides a print spooler, which buffers data in a format the printer will understand, and a scheduler, which sends the buffered data to the printer when it is ready to be received.

The lpstat command has individual options to provide CUPS status information about the scheduler, spooler, and printer/s:

![image](images/7g.jpg)Issue the command lpstat -t option to see printer status

![image](images/pg181_2.jpg)

![image](images/hot.jpg)

Where more than one printer is available, use **lpr -P** to nominate the printer to print the job.

**Evaluating Expressions**

The expr command enables you to perform simple math calculations at the shell prompt. It recognizes all the usual arithmetic operators, but those that have other meanings in the shell need to be prefixed by a backslash \ escape character. For instance, the * wildcard must be escaped for multiplication.

![image](images/pg182_1.jpg)

Each argument must be separated by whitespace, and parentheses can be used to establish operator precedence in longer expressions – but each parenthesis character must be escaped.

The expr command can also perform Boolean evaluations that return either true (1) or false (0) answers, and perform simple string manipulation with functions length, substr, and index.

![image](images/1g.jpg)At a shell prompt, enter expr 7 + 3 to perform addition, and expr 7 \* 3 to perform multiplication

![image](images/2g.jpg)Enter expr 7 \* \( 3 + 1 \) to evaluate a complex expression, and expr 7 = 3 to make a Boolean equality evaluation

![image](images/3g.jpg)Issue the command expr length “Linux in easy steps” to discover the length of the specified string

![image](images/4g.jpg)Issue the command expr substr “Linux in easy steps” 7 13 to extract a substring of the specified string

![image](images/5g.jpg)Issue the command expr index “Linux in easy steps” “x” to discover the position of the first “x” in the string

![image](images/pg182_2.jpg)

![image](images/forget.jpg)

The arithmetic operators are **+** add, **-** subtract, ***** multiply, **/** divide, and **%** modulo.

![image](images/hot.jpg)

You can quickly launch a graphical calculator from a Terminal window using the **xcalc** command.

The result of an expression evaluation can be made to cause a particular action using an if-then-else statement. This has three separate parts that specify a test expression, the action to perform when the test is true, and the action to perform when it is false.

The if keyword begins the statement and is followed by the test expression enclosed within a pair of [ ] square brackets. Each part of the entire statement must be separated from the next by whitespace, to enable the shell to evaluate the expression.

The then keyword begins the second part of the statement, specifying the commands to execute when the test is true. Similarly, the else keyword begins the third part of the statement, specifying the commands to execute when the test is false. Finally, the fi keyword must be added to mark the end of the statement.

![image](images/forget.jpg)

You must leave a space after the **if** keyword to avoid an error. Also leave a space after the **[** bracket and before the **]** bracket to avoid an error.

You may type the first part of the statement then hit **Return** to be prompted to enter the rest of the statement, or type the entire statement separating each part with a semicolon:

![image](images/6g.jpg)Type if [ `expr 7 % 2` = 0 ] to test if the remainder of dividing seven by two is zero, then hit **Return**

![image](images/7g.jpg)At the statement prompt, enter then echo “Even Number”

![image](images/8g.jpg)Now, enter else echo “Odd Number”

![image](images/9g.jpg)Type fi then hit **Return** to perform the appropriate action

![image](images/10g.jpg)Make a similar test in a continuous statement by typing if [ `expr 8 % 2` = 0 ]; then echo Even; else echo Odd; fi, then hit **Return** to perform the appropriate action

![image](images/pg183_1.jpg)

![image](images/snake.jpg)

The backtick **`** operators enclose **expr 7 % 2** so that operation gets performed before the test expression is evaluated – in this case, the remainder of 1 is substituted, making the expression **if [ 1 = 0 ]**.

**Scripting the Shell**

Lengthy shell routines, like those [here](#chapter10.xhtml_must), can be conveniently saved as a shell script for execution when required. Shell scripts are simply plain text files that begin their first line with #!/bin/bash, specifying the location of the bash program, and are typically given a .sh file extension.

![image](images/pg184_1.jpg)

Once a shell script file has its access permission set to “executable”, it can be executed by specifying its path at a shell prompt – its name prefixed by ./ dot-slash characters if it is in the current directory.

A script might, perhaps, employ the $RANDOM shell variable that generates an integer from zero to 32,767 each time it is called. These are not truly random, however, as the same sequence is generated given the same starting point (seed) – in order to ensure different sequences, it is necessary to set it with different seeds.

One solution is to extract a dynamic value from the current time using the date +%s command to deliver the current number of seconds that have elapsed since 00:00:00 GMT January 1, 1970. Using this to seed the $RANDOM variable gets better random number generation.

![image](images/hot.jpg)

Enter **RANDOM=1** then **echo $RANDOM** three times to see the pattern. Repeat both commands to see the pattern repeat.

Arithmetic can be performed on shell variables, such as $RANDOM, by including the let command in a script:

![image](images/1g.jpg)Open any plain text editor and begin a new file with the line #!/bin/bash

![image](images/2g.jpg)On a new line, type a line to seed the $RANDOM variable RANDOM=`date +%s`

![image](images/3g.jpg)Add a line to assign a value 1-20 to a variable let NUM=( $RANDOM % 20 + 1 )

![image](images/4g.jpg)On the next line, type an instruction to clear the window clear

![image](images/5g.jpg)Add these lines to output text for the user echo “I have chosen a number between 1 and 20” echo “Can you guess what it is?”

![image](images/forget.jpg)

Parentheses surround the expression to evaluate, but you must not introduce whitespace around the **=** character in the assignments.

![image](images/6g.jpg)Now, add a line to read the user’s guess into a variable read GUESS

![image](images/7g.jpg)Type the following lines exactly to evaluate whether the user’s guess matches the generated number and output an appropriate response for each incorrect attempt

**while [ $GUESS -ne $NUM ]**

**do**

**if [ $GUESS -gt $NUM ]**

**then echo “No - try lower... ”**

**else echo “No - try higher... ”**

**fi**

**read GUESS**

**done**

![image](images/8g.jpg)Add a line to confirm a correct guess echo “Yes the number is $NUM”

![image](images/9g.jpg)Save the script as guess.sh in the current directory

![image](images/10g.jpg)At a shell prompt, change the access permissions to make the script executable by its owner with this command chmod 711 guess.sh

![image](images/11g.jpg)Enter ./guess.sh to execute the script, then guess the number randomly selected by the script

![image](images/pg185_1.jpg)

![image](images/hot.jpg)

The **while-do** statement is a loop that employs the **-ne** (not equal) comparison operator and a **-gt** (greater than) comparison operator. Other Bash shell comparison operators include **-eq** (equal) and **-lt** (less than).

![image](images/snake.jpg)

Remember that the square bracket characters are operators – there must be space around them to avoid errors.

**Summary**

•The sudo command executes commands at a shell prompt as if a regular user is the root superuser.

•The Advanced Packaging Tool (APT) list of packages can be updated with **apt-get update**, packages installed with apt-get install, and removed with apt-get remove.

•Files can be compressed with gzip, bzip2 or zip, and uncompressed with their companions gunzip, bunzip2, and unzip.

•File systems can be attached to the tree with mount, detached with umount, and checked with the fsck command.

•User accounts can be created and edited by the root superuser with the commands useradd, userdel and usermod.

•Login passwords can be changed with the passwd command, and personal details can be edited with the chfn command.

•The groups accounts can be created and edited by the superuser with groupadd, groupdel and groupmod.

•Access permissions can be modified using the chmod command, and ownership changed using chown and chgrp.

•Each process has a unique Process ID (PID), revealed by the ps command, and may be terminated by a kill command.

•The IP address of a URL can be discovered with the host command, and that of your own computer with ifconfig.

•Print jobs can be created with lpr, removed with lprm, listed with lpq, and status displayed with the lpstat command.

•Expressions can be evaluated with the expr command, and strings manipulated with length, substr, and index functions.

•Bash shell scripts begin with #!/bin/bash and are executed at a prompt by prefixing the file name by ./ dot-slash characters.

[![image](images/IBC.jpg)](http://www.ineasysteps.com)

[![image](images/bcover.jpg)](http://www.ineasysteps.com)