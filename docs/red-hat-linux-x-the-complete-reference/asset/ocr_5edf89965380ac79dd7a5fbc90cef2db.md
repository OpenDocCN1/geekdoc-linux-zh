You will also need to determine how you want to use hardware resources, for example, how much of your hard disk you want to devote to Linux.

# CD-ROM, Hard Disk, and Mouse Information

For some older SCSI CD-ROM drives, you need the manufacturer's name and model.

Decide how much of your hard drive (in megabytes) you want to dedicate to your Linux system. If you are sharing with Windows, decide how much you want for Windows and how much for Linux.

Decide how much space you want for your swap partition. Your swap partition should be about the same size as your RAM memory, but it can work with as little as 64MB. For system's with smaller RAM configurations, the swap disk should be twice the size of the RAM. The size of the swap partition was expanded with the 2.4 kernel. Your swap partition is used by Linux as an extension of your computer's RAM.

Find the make and model of the mouse you are using. Linux supports serial, USB, PS/2, IMPS/2, and bus mice. Most mice are supported, including Microsoft, Logitech, and Mouse Systems.

Know what time zone you are in and to what time zone your hardware clock is set. This can be either Greenwich Mean Time (GMT), also called Universal Coordinated Time (UCT), or your local time zone.

Know which kind of port your mouse is using, such as PS/2, USB, or serial port. Most systems now use a PS/2 port. For a serial port mouse, you will need to know which port it is connected to: COM1, COM2, or none.

# Video and Monitor Information

Although most monitors and video cards are automatically configured during installation, you might still need to provide the manufacturer's make and model, in case the detection is wrong. Find out the manufacturer for your monitor and its model, such as Iiyama VisionMaster or Hitachi CM828. Do the same for your video card-for example, Matrox Millennium G400 or ATI Radeon (you can find a complete list of supported cards at www.xfree86.org). This should be listed on the manuals or registration information provided with your computer. For some of the most recent monitors and video cards, and some older, uncommon ones, you may need to provide certain hardware specifications. Having this information on hand, if possible, is advisable. At the end of the installation process, you are presented with lists of video cards and monitors from which to choose your own. These lists are extensive. If your card or monitor is not on the list, however, you need to provide certain hardware information about them. If the configuration should fail, you can always do it later using the X Window System configuration tool, redhat-config-xfree86. Of particular importance is the monitor information, including the vertical and horizontal refresh rates.

# Video Card Information

You should also know the following video card information, though the chipset is most likely not necessary. Your card will be automatically detected, but you should make sure the selection is accurate:

+   - What is the make and model of your video card?
+   - What chipset does your video card use?
+   - How much memory is on your video card?

# Monitor Information

What are the manufacturer and model of your monitor? Linux supports an extensive list of monitors, covering almost all current ones. Your monitor will be automatically detected and selected. If the detection is wrong, you can find the correct one and select it from the list. If, however, your monitor is not on this list, you may need to provide the following information. Be sure this information is correct. If you enter a horizontal or vertical refresh rate that is too high, you can seriously damage older monitors. Newer ones will just shut down. You can choose a generic profile, or you can enter information for a custom profile. To do that, you need the following information:

+   - The horizontal refresh rate in Hz
+   - The vertical refresh rate in Hz

# Network Configuration Information

If your ISP service or network uses DHCP, you will most likely not have to provide any configuration