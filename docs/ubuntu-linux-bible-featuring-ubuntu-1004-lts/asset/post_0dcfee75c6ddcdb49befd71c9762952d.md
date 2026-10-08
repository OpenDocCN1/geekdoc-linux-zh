
[content]

# Installing Ubuntu

This chapter discusses how to install or simply experiment with Ubuntu Linux on a new or existing 32-bit or 64-bit PC system. This book includes an Ubuntu 10.04 Desktop CD from which you can either install permanently on your system or simply test-drive Ubuntu 10.04 without making any changes to your current system. Test-driving Ubuntu provides a great way to experiment with preconfigured Ubuntu installation without actually modifying your hard drive or going through the installation process. You can also use a Live CD as a portable computer to take with you, temporarily converting other computers to Ubuntu Linux systems regardless of whether the machine is currently running Windows. The Live CDs also offer an impressive Live CD Persistence that enables you to work and save configuration when using the Desktop CD to removable media that you can reuse the next time you boot from the CD. In most cases, you can access your existing disk storage after booting from the Ubuntu CD, so that you can even do work while using the Live CDs and save to a USB stick or to the disk used by your operating system(s).

The Ubuntu Desktop CD takes the traditional Live concept one step further by enabling you to quickly install Ubuntu Linux using an easy-to-use installer that is available by clicking an icon on the desktop that you see booting from the Live CD. Ubuntu installer can automatically reduce the size of existing Microsoft Windows or Linux partitions to free up space in which you can install Ubuntu (assuming that your existing partitions are not full, of course).

But wait, there's more! Inserting the Live CD into a system that is running Microsoft Windows enables you to use a package known as Wubi (Windows-based Ubuntu Installer) to install Ubuntu on your Windows system without modifying that system in any way, except for adding an option to boot Ubuntu when you turn it on (and, of course, using some of your existing disk space to store the Ubuntu boot image). More about that later!

## IN THIS CHAPTER

- Booting a Desktop CD
- Installing Ubuntu
- Test-driving Ubuntu
- Accessing existing partitions from a Desktop CD
- Creating bootable USB drives
- Installing Ubuntu without partitioning

# Part I: Getting Started with Ubuntu

If you're using a 32-bit x86 system and want to run or experiment with Ubuntu Linux, the Ubuntu Desktop CD provided with this book is for you. If not, this chapter explains how to get the Ubuntu Live CD that's appropriate for your system you're using.

# Note

In late 2009, Canonical announced support for the ARM platform, extending Ubuntu's availability to fewer networks that use ARM processors. To obtain a version of Ubuntu for ARM, see www.ubuntu.com/products/whatis/arm. Versions of Ubuntu are also available for the PPC (Power) and SPARC platforms, but these are no longer officially supported by Canonical. Ubuntu for PPC is a community-supported project that is still quite active, while Ubuntu for SPARC systems have faded away. You can see many community-supported versions of Ubuntu are available and download CD images from the original URL http://cdimage.ubuntu.com/ports/releases/VERSION/release, where VERSION is the name of a standard Ubuntu release, such as Karmic, Lucid, and so on.

# Getting a 64-Bit Desktop CD

The Ubuntu Desktop CD provided with this book will boot on any x86 PC system. If you want to install or experiment with Ubuntu on a 64-bit computer system, you will need to obtain a different, equivalent Desktop CD. If you have a reasonably fast Internet connection (or plenty of time) and a CD burner, the easiest way to get a different Desktop CD is to download an ISO image. An ISO image is a file containing an exact copy of the CD-ROM or DVD that is in the format mandated by the International Standards Organization 9660 specification. To get a 64-bit Ubuntu Desktop CD, go to Ubuntu's web page at www.ubuntu.com/download, select the version of Ubuntu that you want a CD, select your country or the one that's closest to you in general, and select an ISO of the 64-bit Desktop CD. Save the downloaded ISO image to a file, burn it to CD once the download completes, and you're ready to go!

If you have a slow Internet connection or do not have a CD burner, panic! As mentioned in the Introduction for this book, the Ubuntu folks will ship you Ubuntu CDs, although they take a few weeks because they're shipped from the Netherlands. This isn't the right solution for those of us who want instant gratification, but it might work for you. To request CDs directly from Ubuntu, go to the Ubuntu web page at https://shipit.ubuntu.com, create an account by entering your e-mail address and a password, and request one or more sets of Ubuntu CDs for the current release. You can order free CDs for system types at the same time.

# Booting from a Desktop CD

Booting from an Ubuntu Desktop CD is as easy as inserting the appropriate Desktop CD into your system's drive, restarting your system, and making sure that the system boots from the CD drive before booting from a hard partition.

# Chapter 2: Installing Ubuntu

## Caution

If your PC boots from the hard drive even if the correct Desktop CD is present in your CD drive, you'll need to modify the boot order in your BIOS settings. The boot order is the sequence in which available devices are searched for bootable disks when your system is powered on. To do this, turn your computer on and press the key on your keyboard that gives you access to the BIOS. Depending on the type of BIOS your computer uses, this is usually the Delete or F2 key. Once in the BIOS settings, use the arrow keys to move the CD drive to the top of the boot list. Save the settings and exit, usually by pressing F10.

When you boot from the Ubuntu CD, you'll initially see a screen like the one shown in Figure 2-1.

### FIGURE 2-1
The initial boot screen on the Desktop CD

If you do nothing when you see this screen, your system will continue booting from the Desktop CD and will eventually display the screen shown in Figure 2-2.

### FIGURE 2-2
The default Desktop CD try/install screen

Once you see this, you can optionally use the scrollable list on the left to change the language that the Ubuntu CD or the Ubuntu installer deuses. You can then either:

- **Try Ubuntu 10.04** to boot into Ubuntu Linux without making any changes to your computer system. This allows you to experiment with Ubuntu without making any changes to your system (generally referred to as test-driving). The Linux CD is shown in Figure 2-5, later in this section. Experimenting with Linux after booting from a Desktop CD is described in the section, "Test-Driving Ubuntu," later in this chapter. Skip ahead to that section for more information.
- **Install Ubuntu 10.04** to install Ubuntu Linux on your system. Installing Ubuntu on your system is described in the next section, entitled "Installing Ubuntu Linux from a Desktop CD." Skip ahead to that section for more information.

### Tip
If the screen shown in Figure 2-2 displays a link that says "update this installer," you may want to click that link to ensure that you have the latest version of the installer. If you do not update the installer, the installation process will still work correctly, but may offer different installation options than those that are discussed in this section. Similarly, updating the installer may introduce dialogs that are slightly different than those discussed in this section, but should still provide the same capabilities. ■

