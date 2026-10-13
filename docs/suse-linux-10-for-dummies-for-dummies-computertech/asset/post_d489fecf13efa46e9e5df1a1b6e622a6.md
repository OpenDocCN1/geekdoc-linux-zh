
a Windows file or print server. You can also access shared folders on other Windows systems on your network.

## Networking

Now that most PCs are either in a local area network or connected to the Internet, you need to manage the network as well. You set up the local area network when you install SUSE Linux. For connecting to the Internet using a modem, you can use YaST.

If you connect to the Internet using DSL (that’s the fast Internet connection from the phone company) or a cable modem, you need a PC with an Ethernet card that connects to the cable or DSL modem. It also means that you have to set up a local area network and configure the Ethernet card. But fortunately, these steps are typically a part of the SUSE Linux installation. If you want to do the configurations later, you can — by using a GUI network configuration tool accessible from YaST.

SUSE Linux also includes tools for configuring a firewall, a protective buffer that helps keep your system relatively secure from anyone trying to snoop over your Internet connection. You can configure the firewall by running a GUI firewall configuration tool accessible from YaST.

## Getting Started with SUSE Linux

Based on my personal experience in learning new subjects, I recommend a three-step process to get started with SUSE Linux:

1. Install and configure SUSE Linux on your PC.
2. Explore SUSE Linux — the GUI desktop and the applications.
3. Use SUSE Linux for your day-to-day work.

In the following sections, I explain this prescription a bit more.

### Install and configure SUSE Linux

Your PC probably came with some flavor of Microsoft Windows. So the first step is to get SUSE Linux onto your PC. This book comes with SUSE Linux — all you have to do is follow the instructions in Chapter 2 to install it.

Just to pique your curiosity, you can keep both Windows and SUSE Linux on the PC; the SUSE Linux installer can split up the space on the hard drive into two parts — one part for Windows and the other for installing SUSE Linux. During the SUSE Linux installation, you configure many items — from the network card (if any) to the X Window System.

As you’ll find out for yourself, SUSE Linux installation is very easy, especially with the graphical YaST installer.

After you install SUSE Linux, you can configure individual system components (for example, the printer) and tweak any needed settings that aren’t configured during installation.

You also can configure your GUI desktop of choice — GNOME or KDE. Each has configuration tools. You can use these tools to adjust the look and feel of the desktop (background, fonts, screen saver, and even the entire color scheme).

After you’re through with the configuration step, all the hardware on your system and the applications should run to your liking.

### Explore SUSE Linux

With a properly configured SUSE Linux PC at your disposal, you can start exploring SUSE Linux. You can begin the exploration from the GUI desktop that you get after logging in.

Explore the GUI desktops — GNOME and KDE — and the folders and files that make up the Linux file system. You can also try out the applications from the desktop. SUSE Linux comes with office and multimedia applications and databases that you can begin using.

Also try out the shell — open up a terminal window and type some Linux commands in that window. You can also explore the text editors that work in text mode. Knowing how to edit text files without the GUI is a good idea. At least you won’t be helpless if the GUI is unavailable for some reason.

### Use SUSE Linux

After you explore the SUSE Linux landscape and know what is what, you can then start using SUSE Linux for your day-to-day work — browsing the Web, using Office applications such as a word processor and spreadsheet, listen to music, burn a music CD, and anything else you want.

Of course, you can expect to become increasingly proficient in SUSE Linux as time goes on. After all, learning is a lifelong journey.

Bon voyage!

## Chapter 2

## Installing SUSE Linux

### In This Chapter

- Understanding the installation steps
- Checking your PC’s hardware
- Installing SUSE Linux
- Configuring SUSE Linux

Most PCs come with Microsoft Windows preinstalled, so you typically never have to go through the Windows installation (except when something goes wrong, of course). To run SUSE Linux, however, you first have to install it on your PC. All you have to do to install SUSE Linux is take out the DVD that comes with this book and follow the steps in this chapter.

You can install SUSE Linux in addition to Microsoft Windows and simply select one or the other operating system after you power up the PC. The SUSE Linux installer can shrink the disk space used by Windows and create a new *disk partition* — basically set aside a part of the hard drive for SUSE Linux.

Before you get started, just take a deep breath and exhale sloooowly. You have nothing to worry about because I explain everything in this chapter.

## Introducing the Installation Steps

Before getting started with the installation, I find it helpful to go over the entire sequence of installation steps, without the gory details. In this section, I show you the road map for the installation process. Then you can follow the detailed steps and install SUSE Linux from this book’s companion DVD.

Here are the general steps for installing SUSE Linux:

1. **Check your PC’s hardware to make sure everything works with SUSE Linux.**

2. **Make sure that your PC can boot from the DVD/CD-ROM drive.**
   You may have to get into SETUP and change the order of boot devices.

3. **Boot your PC from the DVD.**
   At the initial boot screen, use the arrow keys to select Installation and press Enter. This starts SUSE’s graphical installer — YaST — that you use to complete the installation.

4. **Select the installation language and then select New Installation.**
   YaST then gathers information about your PC and displays a set of installation settings.

5. **If you are going to add SUSE Linux to a PC that already has any version of Microsoft Windows on the hard drive, edit the Partitioning setting and select the hard drive as the location where you want to install SUSE Linux.**
   Then YaST gives you the option to shrink the Windows partition. In particular, YaST can resize Windows XP partitions that use the NTFS file system. When you resize the Windows partition, everything is safe until you confirm that installation should begin.

6. **Edit any other installation settings.**
   In particular, you probably have to edit the time zone to suit your geographic location. You have to edit the software selection if you want a GNOME desktop instead of the default KDE desktop.

7. **After you have finished editing the installation settings, accept the selections and confirm that YaST should begin installing.**
   This is the point of no return. YaST formats the selected disk partition and begins copying files from the DVD onto the hard drive.

8. **After installing a minimal SUSE Linux system, YaST reboots the PC.**
   After the initial version of SUSE Linux starts again, YaST guides you through a number of configuration steps that include setting the root (superuser) password; configuring the network and firewall; setting up online updates of SUSE Linux; creating a normal user account; and configuring hardware such as a graphics card, printer, and sound card.

9. **At the end of the installation, YaST reboots the PC. When SUSE Linux runs again, you should get the GUI desktop.**

### Checking Your PC’s Hardware

If you are concerned that your PC may not be able to run SUSE Linux, here are some of the key components in your PC that you need to consider before you start the SUSE Linux installation.

- **Processor:** A 400 MHz Pentium II or better is best. The processor speed, expressed in MHz (megahertz) or GHz (gigahertz), is not that important as long as it’s over 400 MHz, but the faster the better. Linux can run on other Intel-compatible processors such as AMD, Cyrix, and VIA processors.
- **RAM:** RAM is the amount of memory your system has. As with processing speed, the more RAM, the better. You need 256MB to install both SUSE Linux and to comfortably run a GUI desktop.
- **DVD/CD-ROM:** You must have a DVD/CD-ROM drive, and the PC must be able to boot from that drive. The exact model doesn’t matter. What matters is how the DVD/CD-ROM drive connects to the PC. Most new PCs have DVD/CD-ROM drives that connect to the hard drive controller (called IDE for Integrated Drive Electronics or ATA for AT Attachment). If you add an external DVD/CD drive, it most likely connects to the USB port. Any IDE/ATA or USB DVD/CD-ROM works in SUSE Linux.
- **Hard drives:** Any IDE disk drive works in SUSE Linux. Another type of hard drive controller is SCSI (Small Computer System Interface), which SUSE Linux also supports. To comfortably install and play with SUSE Linux, you need about 5GB of hard drive space.
- **Keyboard:** All keyboards work with SUSE Linux and the X Window System.
- **Mouse:** The installation program can detect the mouse. All types of mice (such as PS/2 or USB) work with SUSE Linux and the X Window System.
- **Video card:** SUSE Linux works fine with all video cards (also known as *display adapters*) in text modes, but if you want the GUI desktop, you need a video card that works with the X Window System. The installer can detect a supported video card and configure the X Window System correctly. However, if the installer cannot detect the video card, it helps if you know the make and model of your video card.
- **Monitor:** The kind of monitor is not particularly critical except that it must be capable of displaying the screen resolutions that the video card uses. The screen resolution is expressed in terms of the number of picture elements (pixels), horizontally and vertically (for example, 1024 x 768). The installer can detect most modern monitors. If it does not detect your monitor, you can select a generic monitor type with a specific
