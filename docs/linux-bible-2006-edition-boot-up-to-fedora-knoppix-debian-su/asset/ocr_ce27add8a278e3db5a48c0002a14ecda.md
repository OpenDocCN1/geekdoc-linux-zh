# Chapter 20 ✦ Playing Music and Video 513

Grip (grip)— Grip is primarily used as a CD ripper, it can also play CDs. Select Multimedia Grip (or type grip in a Terminal window). It includes tools for gathering data from submitting data to CD databases. It includes tools for copying (ripping) CD tracks and converting them to different formats (encoding). Naturally, the grip package must be installed to use this command.

CDPlay (cdp)—If you don't have access to the desktop, you can use the textbased cdp command. This player uses keyboard keys to play your CD, select tracks, go forward or back, or eject. The cdp or cdplay package, depending on your Linux distribution, must be installed to use this command.

X Multimedia System (xmms)—The XMMS player plays a variety of audio formats but can also play directly from CD.

If you try to use some CD players and your CD-ROM drive is not working, see the sidebar "Troubleshooting Your CD-ROM" for further information.

# Troubleshooting Your CD-ROM

If you are unable to play CDs on your CD-ROM drive, here are a few things you can check to correct the problem:

+   * Verify that your CD card is installed and working properly.
* Verify that the CD-ROM drive was detected when you booted Linux. If your CD-ROM drive is an IDE drive, type dmesg | grep ^hd. You should see messages about your CD-ROM that resemble hdc:CDROM/CD01, ATAPI CDROM drive or hdc:ATA1 4X CD drive,128K Cache.
* If you see no indication of a CD-ROM drive, verify that the power supply and cables to the CD-ROM are connected. To make sure the hardware is working, you can also boot to DOS and to access the CD.
* Try inserting a software CD-ROM. If you are running the GNOME or KDE desktop, desktop icon should appear indicating the CD mounted by itself. If no such icon appears, go to a Terminal window, and as the root user, type mount /dev/media directory and list the contents using command. This tells you that the CD-ROM is accessible.
* If you get your CD-ROM working it fails with the message CD device: Permission denied when you try to play music as a non-root user, the problem may be /dev/cdrom (which is typically a link to the actual hardware device) is not readable by any root. Type ls -l /dev/cdrom to see what the device is linked to. (Then as the root user), if for example, the CD device were /dev/dev, type chmod 644 /dev/hdc to enable all users to read your CD-ROM and enable the root user to write to it. One warning: if you use your computer, they will be able to read any CD place in this system.