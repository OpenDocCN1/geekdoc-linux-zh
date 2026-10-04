
## 26 What Fedora Core Helps You Manage

Typically, the hard drive is prepared to use Fedora Core during the installation process. After that, you usually leave the hard drive alone except to back up the data stored there or (occasionally) to install new applications.

Using CD-ROMs or DVD-ROMs in Fedora Core is easy. While you are logged in the GNOME or KDE desktop, just pop up in a CD or DVD in the drive and the DVD/CD-ROM icon appears on the desktop. You can then double-click that DVD/CD-ROM icon and the CD or DVD's contents appears in a window. While whole process of accessing the files on a CD or a DVD from Fedora Core is called mounting the CD or the DVD.

Besides the hard drive and DVD/CD-ROM drive, of course, your PC may have other drivers, such as a floppy disk or Zip drive, and using those disks in Fedora Core is also simple: Insert a disk and double-click the icon that represents the disk drive on the GUI desktop. Doing so mounts the disk so you can begin using it.

## Peripheral devices

Anything connected to you is a peripheral device, and so are some components like sound cards that are installed inside the system box. You can configure and manage these peripheral devices in Fedora Core.

One of the common peripherals is a printer

Another peripheral device that needs configuration is the sound card. Unlike Windows, Fedora requires you to perform a configuration step before the sound works. Again, you can run a graphical sound-card detection utility to test the sound card (choose Menu↩System Settings↔Soundcard Detection from the graphical desktop).

Fedora Core configures other peripheral devices such as the mouse and keyboard at the time of installation. You can pretty much leave them alone after installation.

Nowadays PCs come with the USB (Universal Serial Bus) interface and many devices, such as printers and scanners, plug into your PC's USB port. One feature of USB devices is that you can plug them into the USB port and unplug them at any time - the device does not have to be connected when you power the system. These devices are called hot plug because you can plug in a device when the system is hot, meaning while it's running. Fedora supports many hot plug USB devices. When you plug in a device into the USB port, Fedora Core loads the correct driver and makes the device available to applications.

![](img/d9230b719dc0efd80851f363d8c6f571_53_0.png)

## File systems and sharing

The whole organization of directories and files is called the file system. You can, of course, manage the file system using Fedora Core. When you browse the files from the GNOME or KDE graphical desktop, you work with the familiar icons.

A key task in caring for a file system is to back up important files. In Fedora Core you can use the tar program to archive one or more directories on a floppy or a Zip drive. You can even back up menus on a tape (if you have a tape drive). If you have a CD burner, you can also burn a CD with the files you want to back up or save for posterity.

Fedora Core can also share parts of the file system with other systems on a network. For example, you can use the Network File System (NFS) to share files with other systems on the network. To a user on the system, the system's files appear to be in a directory on the local system.

Fedora Core also comes with the Samba package, which supports sharing with Microsoft Windows systems. Samba makes a Fedora Core system work like a Windows file or print server.

## Network

Now that most PCs are either in a local area network or connected to the Internet, you need to manage the network as well. Fedora Core comes with a Network Configuration tool to set up the local area network. For connecting to the Internet using a modem, you use the Internet Configuration Wizard (choose Main Menu→System Tools→Internet Configuration Wizard).

If you connect to the Internet using DSL (that's the fastest from the phone) or cable modem, you need a PC with an Ethernet card that connects to the cable or DSL. It also means you have to set up a local area network and configure the Ethernet card. But fortunately, these steps are typically a part of Fedora Core installation. If you want to do the configurations later, you can use the Network Configuration tool (choose Main Menu→System Settings→Network).

Fedora Core also includes tools for configuring a firewall, a protective buffer that helps keep your system relatively secure from anyone trying to sniff over your Internet connection. You can configure the firewall by running the Firewall Configuration tool (choose Main Menu→System Settings→Security Level from the graphical desktop.

![](img/d9230b719dc0efd80851f363d8c6f571_53_0.png)

## 28 How Do I Get Started?

## How Do I Get Started?

Based on my personal experience in learning new subjects, I prescribe a four-step process to get started with Fedora Core:

- 1. Install Fedora Core on your PC.
- 2. Configure Fedora Core so that everything works to your liking.
- 3. Explore the GUI desktops and the applications.
- 4. Learn the details of specific subjects such as Internet servers.

In the following sections, I explain this prescription a bit more.

## Install

Microsoft Windows comes installed on your new PC, but Fedora Core usually doesn't. Your first hurdle is to get Fedora Core onto your PC.

After you overcome initial human fear of the unknown, I'll find you Fedora Core fairly easy to install — but do you get it in the first place? The good news is that it's free — available for downloading: For example, you can visit the Linux Online Web site at www.linux.org and click the Download button.

> Because the complete distribution is HUGE — it takes up several CDs or a single DVD — your best is to buy a book (such as this one) that comes with Fedora Core on a DVD-ROM. You can then do the installation by following the instructions in the book.

![](img/d9230b719dc0efd80851f363d8c6f571_54_0.png)

Just to pique your curiosity, installation involves creating space on the hard disk for both Windows and Linux. Then a step creates the Linux partitions and installs Fedora Core from the DVD. Along the way, you configure many items (if any) to the X Window System.

## Configure

When you finish installing Fedora Core, the next step is to configure individual system components (for example, the sound card and the printer) and tweak any needed settings that aren't configured during installation.

If you aren't getting a graphical login screen, for example, Fedora Core comes with tools that help you troubleshoot that problem (typically by configuring the X Window System).

## How Do I Get Started? 29

You also want to configure your GUI desktop of choice — GNOME or KDE. Each has configuration tools. You can use these tools to adjust the look and feel of the desktop (background, title fonts, even the color scheme).

After you're through with the configuration step, all the hardware on your system and the applications run to your liking.

## Explore

With a properly configured Fedora Core PC at your disposal, you are ready to explore Fedora Core itself. You can begin the exploration from the GUI desktop that you get after logging in.

Explore the GUI desktops — GNOME and KDE — and the folders and files that make up the Linux file system. You can also try out the applications from the desktop. You find office and multimedia applications and databases to explore.

Also try the shell — open up a terminal window and type Linux commands in that window. You can also explore the text editors that work in text mode. Knowing how to edit text files without the GUI just in case the GUI is not available is good. At least you won't be helpless.

## Learn

After you explore the Fedora landscape and know what it is, you can dig deeper and learn specific subject areas. For example, you may be interested in setting up Internet servers. You can then learn the details of setting up individual servers such as sendmail for e-mail, Apache for a Web server, and the INN server for news.

You can choose to find out many more areas, such as security, programming, and system administration.

Of course, you can expect this step to go on and on, even after you have your system running the way you want it — for now. After all, learning is a lifelong journey.

Bon voyage!
