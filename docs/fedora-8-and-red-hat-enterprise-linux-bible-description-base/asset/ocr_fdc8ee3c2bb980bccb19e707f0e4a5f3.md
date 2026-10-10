However, you might sometimes want access to server applications, administration tools, development environment, or thousands of free applications you can get with Fedora.

+   * Fedora only — Although you pay a bit of a premium for Apple hardware (though not as much as you used to), you might like the form and features of those cute Apple Mac computers enough to pay a bit extra to have it as your primary desktop Fedora computer.

This section describes how to start with an Intel-based Apple Mac computer (I used a Mac Mini for this example) and configure it to either dual boot with Mac OS X or run Fedora alone.

> CAUTION: Installing Fedora on Intel-based hardware is still a technology that is experimental in the Fedora community. Some hardware components still require extra tweaking or won’t work at all. I recommend that you don’t do this procedure if you can’t afford the possibility that your disk may be blown away and have to be reinstalled from scratch.

# Before installing Fedora on your Mac

Let’s start with a reminder that this procedure is only for Apple Mac computers that are based on Intel architecture. I ran this procedure on a new Mac Mini 1.1 (Intel Core Duo CPU, 512MB RAM). However, the same procedure should work for Intel-based iMac, MacBook, MacBook Pro, or Mac Pro computers.

This procedure is not for Macs with PowerPC architectures. Fedora does support that configuration, but you need to download the ppc installation media from Fedora instead of using the DVD that comes with this book. (Get the media for installing on PowerPCs from http://fedoraproject.org/wiki/Distribution/Download.)

When you purchase your Mac, the entire hard disk is devoted to Mac OS X. To keep your Mac OS X installation on the computer (so you can boot either Mac OS X or Fedora), you need to reduce the amount of space devoted to Mac OS X. Then you need to use that space to create one or more partitions for installing Fedora.

Although the procedure for resizing and repartitioning your disk is fairly safe, there is some risk that you could corrupt your Mac OS X partition or make the machine (temporarily) unbootable. For that reason, before starting the procedure that follows, please . . .

. . . BACK UP ANY IMPORTANT DATA!

# Installing Fedora

Mac OS/X Leopard offers software called Boot Camp that can be used to resize Mac hard disks (using the default HFS+ file system type). Until Leopard was released, the beta version of Boot Camp was available as a free download from Apple. The following procedure describes how to update your firmware, resize your disk, and install Fedora.

+   1. **Check for firmware updates** — Update your Mac OS X system to the latest firmware. Refer to the Mac OS X Firmware Updates page for information on how to do that