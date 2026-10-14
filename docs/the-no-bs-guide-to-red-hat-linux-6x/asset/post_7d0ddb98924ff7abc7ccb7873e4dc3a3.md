
# INSTALLING LINUX ON YOUR PC

- About the CD-ROM 4
- Sayonara, DOS? 4
- What Hardware Will I Need? 5
- Taking Inventory 6
- The Installation at a Glance 8
- The Linux Installation Process 11
- Post Installation: Configuration 27
- I Need Help! 32

Now that you’ve had a bit of history, it’s time for the real fun—installing the Linux operating system on your own personal computer. This chapter assumes that you have a PC currently running some version of DOS, but installing Linux is going to be very different from installing a new DOS or Windows software package. And most important, when you’re done, you’ll be booting up something entirely different from the DOS-based system you’ve grown to know and, uh, tolerate.

## ABOUT THE CD-ROM

The version of Linux provided on the CD accompanying this book is Red Hat Linux version 6.2. There are many distributions of Linux available, but I chose Red Hat because it’s very stable and extremely popular with Linux aficionados. Red Hat is also known for its add-ons that make installing, configuring, and running Linux much easier. The new graphical installation program in version 6.2 makes setting up Linux easier than ever, and does a much better job of autodetecting your hardware. If your DOS system is properly configured, Red Hat Linux installs directly from the CD-ROM with one simple command—and when you’re done, you have a fully functioning Internet-ready Linux system with a graphical user interface. All the arcane file system and graphical user interface (GUI) setup and network configuration is done automatically—not the case with other Linux versions.

## SAYONARA, DOS?

You’ll be running Linux (Unix for your PC), but you can take comfort in the knowledge that your DOS system is still available in case you ever want to return from the Land of Grep and Awk. (These are two Linux commands that sound weird, but are quite useful. You’ll learn about them in Chapter 5, “Important Linux Commands”.)

In fact, you can even access your DOS files directly from Linux, and in some cases you can run DOS or Windows programs under Linux. In Chapter 12, “Linux Does DOS and Windows,” I’ll show you how to keep in touch with DOS and even boot up Windows 95/98 while running Linux.

## What Hardware Will I Need?

You don’t need an expensive state-of-the-art monster machine to run Linux. Almost any PC with a 386, 486, or Pentium processor will do nicely. That’s because Linux, unlike Microsoft Windows and other Unix flavors, is not a disk-chomping, memory-swilling CPU hog. A bare-bones Linux installation will run quite happily on a 386SX with 16MB of memory and a 150MB hard drive. Of course, it will run faster on an 800-MHz Pentium III with 128MB of RAM and a 10GB hard drive, but that’s your choice—you can get to work in a Yugo or a Cadillac.

It’s a pretty safe bet that your PC will run Linux if you already have Windows 95 installed and working, but not every piece of hardware is supported by Linux. Here are the major system components, in terms of compatibility and requirements:

- **CPU:** Intel 80386, 80486, Pentium, or the AMD/Cyrix variants (that is, almost any 386 or better); Linux will emulate a math coprocessor if one is not present.
- **Video:** Almost any VGA/SVGA card that works with DOS is acceptable.
- **Floppy drive:** A 3.5-inch floppy drive is required.
- **Hard disk:** Most MFM, RLL, IDE and SCSI drives/controllers are supported; a minimum of 800MB of free space is required for the installation detailed here, but 1,600MB is more reasonable for serious use.
- **Memory:** Minimum 16MB of RAM is recommended, but more memory dramatically improves performance; 48MB or more is recommended if the user wishes to use the GNOME GUI; mixing RAM of various speeds (that is, 60 ns, 70 ns) can cause problems.
- **CD-ROM:** Almost any IDE- or SCSI-based CD-ROM drive will work.
- **Modem:** Required if you want to connect to or host Internet services; the faster the better, but 33.6 Kbps or better is recommended.
