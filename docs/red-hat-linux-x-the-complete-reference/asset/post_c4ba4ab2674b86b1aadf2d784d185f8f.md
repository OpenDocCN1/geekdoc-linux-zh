
You will also need to determine how you want to use hardware resources, for example, how much of your hard disk you want to devote to Linux.

## CD-ROM, Hard Disk, and Mouse Information

For some older SCSI CD-ROM drives, you need the manufacturer's name and model.

Decide how much of your hard drive (in megabytes) you want to dedicate to your Linux system. If you are sharing with Windows, decide how much you want for Windows and how much for Linux.

Decide how much space you want for your swap partition. Your swap partition should be about the same size as your RAM memory, but it can work with as little as 64MB. For systems with smaller RAM configurations, the swap disk should be twice the size of the RAM. The size of the swap partition was expanded with the 2.4 kernel. Your swap partition is used by Linux as an extension of your computer's RAM.

Find the make and model of the mouse you are using. Linux supports serial, USB, PS/2, IMPS/2, and bus mice. Most mice are supported, including Microsoft, Logitech, and Mouse Systems.

Know what time zone you are in and to what time zone your hardware clock is set. This can be either Greenwich Mean Time (GMT), also called Universal Coordinated Time (UTC), or your local time zone.

Know which kind of port your mouse is using, such as PS/2, USB, or serial port. Most systems now use a PS/2 port. For a serial port mouse, you will need to know which port it is connected to: COM1, COM2, or none.

## Video and Monitor Information

Although most monitors and video cards are automatically configured during installation, you might still need to provide the manufacturer's make and model, in case the detection is wrong. Find out the manufacturer for your monitor and its model, such as Iiyama VisionMaster or Hitachi CM828. Do the same for your video card-for example, Matrox Millennium G400 or ATI Radeon (you can find a complete list of supported cards at www.xfree86.org). This should be listed on the manuals or registration information provided with your computer. For some of the most recent monitors and video cards, and some older, uncommon ones, you may need to provide certain hardware specifications. Having this information on hand, if possible, is advisable. At the end of the installation process, you are presented with lists of video cards and monitors from which to choose your own. These lists are extensive. If your card or monitor is not on the list, however, you need to provide certain hardware information about them. If the configuration should fail, you can always do it later using the X Window System configuration tool, redhat-config-xfree86. Of particular importance is the monitor information, including the vertical and horizontal refresh rates.

### Video Card Information

You should also know the following video card information, though the chipset is most likely not necessary. Your card will be automatically detected, but you should make sure the selection is accurate:

- What is the make and model of your video card?
- What chipset does your video card use?
- How much memory is on your video card?

### Monitor Information

What are the manufacturer and model of your monitor? Linux supports an extensive list of monitors, covering almost all current ones. Your monitor will be automatically detected and selected. If the detection is wrong, you can find the correct one and select it from the list. If, however, your monitor is not on this list, you may need to provide the following information. Be sure this information is correct. If you enter a horizontal or vertical refresh rate that is too high, you can seriously damage older monitors. Newer ones will just shut down. You can choose a generic profile, or you can enter information for a custom profile. To do that, you need the following information:

- The horizontal refresh rate in Hz
- The vertical refresh rate in Hz

## Network Configuration Information

If your ISP service or network uses DHCP, you will most likely not have to provide any configuration information. Most local networks, cable connections, and DSL connections now use DHCP to automatically configure hosts. Network information is provided automatically by a DHCP server. During the installation process, you will be given the option of either automatically configuring your network connection (DHCP) or entering the network information manually.

If you need to configure your network connection, you can also put configuration off until a later time and use network configuration utilities provided by your distribution to perform network configuration. All you need to do during installation is provide a hostname.

If you decide to manually configure your network connection, you will need the following information, usually obtainable from your network administrator:

- The name for your computer (this is called a hostname). Your computer will be identified by this name on the Internet. Do not use "localhost," which is reserved for special use by your system.
- The Internet Protocol (IP) address assigned to your machine. Every host on the Internet is assigned an IP address.
- Your network IP address. This address is usually similar to the IP address, but with one or more zeros at the end.
- The netmask. This is usually 255.255.255.0 for class C IP addresses. If, however, you are part of a large network, check with your network administrator.
- The broadcast address for your network, if available. Usually, your broadcast address is the same as your IP address with the number 255 used for the last number.
- The gateway IP address for your network. The gateway connects your network to a larger one like the Internet.
- The IP address of any name servers your network uses.
- The NIS domain and IP address if your network uses an NIS server.
- The Samba server if your network is connected to a Windows network.

## Creating the Boot Disks

If you are installing Red Hat using the DVD-ROM included with this book, or you are using a set of CD-ROM discs to install Linux, and if your computer is fairly new, it most likely has the ability to boot from your CD-ROM. This book's DVD-ROM operates as a bootable CD-ROM. In this case, you can just use your CD-ROM or this book's DVD-ROM as your installation disk and skip this section. (You may need to configure your BIOS to boot from your CD-ROM.) If you cannot boot from your CD-ROM or DVD-ROM, you will have to create floppy install disks as described here.

Note If you are installing from the Red Hat DVD-ROM included with this book, you will need a DVD-ROM drive on your computer to read the DVD-ROM disc. The DVD-ROM included with this book has been configured to be bootable, functioning like a boot CD-ROM. If your system supports bootable CD-ROMs, then it will boot from this DVD-ROM, letting you install your Red Hat system from the DVD-ROM directly.

On Windows, to use the rawritewin program to create a floppy install disk, first insert the CD-ROM into your CD-ROM drive (if you are installing from the DVD-ROM disc included with this book, you would use your DVD-ROM drive instead). Change to your CD-ROM drive. Once you have changed to the CD-ROM drive, you then need to change to the \dosutils directory. The rawritewin command is in the dosutils\rawritewin directory. Just double-click it to start it. It is very easy to create a boot disk with rawritewin. Just run it from Windows and use its interface to select the floppy disk image bootdsk.img, with support disks pcmiadd.img, and drvnet.img. The image file you want for a CD-ROM or DVD-ROM installation is the boot.iso file, also located on your CD-ROM in the images/ directory. Be sure that your floppy drive is correctly listed. The default will be A:. Then place a blank floppy in your floppy drive and click Write.

For rawrite, which you have to use on MS-DOS, at your DOS prompt, change to your CD-ROM drive, using whatever the letter for that drive may be. For example, if your CD-ROM drive is the E drive, just type e: and press ENTER. Once you have changed to the CD-ROM drive, you then need to change to the \images directory. On the DVD-ROM included with this book, the install disk image is bootdsk.img with support disks for network and notebooks, drvnet.img and pcmiadd.img. The rawrite command has to be run at a DOS prompt. Enter the full path for the rawrite command, including the CD-ROM or DVD-ROM drive letter, such as e:\dosutils\rawrite. The rawrite command first prompts you for the name of the disk image file you want to copy. Enter the full name of the install image file. The command then asks you to enter the letter of the floppy drive where you put your floppy disk. On many systems, this is the A drive.

```
E:\> cd images
E:\images> e:\dosutils\rawrite
Enter source file name: bootdsk.img
Enter destination drive (A or B) and press ENTER: a
```

Press ENTER to confirm that you have a blank floppy disk in the drive. rawrite will then copy the image file to your floppy disk, creating your install disk. When it finishes, remove your disk from the floppy drive. This is the disk that the installation procedure (described later) refers to as the install diskette. If you need to create a network support disk, use drvnet.img. For PCMCIA support, use pcmiadd.img.

To create floppy disks on a Linux or Unix system, you use the dd command and specify the boot image file to use along with the name of the floppy device and the size of the floppy disk. You will first need to mount the CD-ROM, then change to its mount directory. On most Linux systems, the first floppy disk drive is at /dev/fd0 and its size is usually 1440 for a 1.4 floppy disk. With the if option, you specify the image file to use, the of option indicates the floppy device name, and the bs option specifies the block size.

```
dd if=images/bootdsk.img of=/dev/fd0 bs=1440
```

If your system contains very old CD-ROM drives, SCSI adapters, or network cards, you will likely have to create a driver disk. Your Red Hat CD-ROM/DVD-ROM provides a floppy disk image called /images/drvnet.img that contains drivers for many uncommon devices, particularly those not using the PCI bus. If you have devices supported by these drivers, you should create a driver disk using drvnet.img and
