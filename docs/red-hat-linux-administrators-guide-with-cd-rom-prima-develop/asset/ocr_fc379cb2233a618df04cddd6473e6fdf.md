the PCMCIA slot on a laptop. When connected to that slot, the pcmcia.img driver recognizes the basic drivers for most Ethernet PCMCIA cards.

You might prefer installing rawrite in the root directory of your Windows machine when creating a boot floppy. The bootimg file goes in the same location. To use rawrite, simply start a DOS window and change into the root directory. Type rawrite, and then when prompted type the filename you wish to copy to the floppy. In most cases, you would type boot.img. You will need to type the target diskette drive as well. Nearly all Windows machines use a:\ as their primary floppy drive specification. Figure 1.3 shows a sample session.

Once rawrite is done copying the file to the floppy sector by sector, you will get your prompt back. You can now use this floppy on most PCs to boot up the Linux installation program.

# Creating a Boot Floppy Using Linux

The boot image can just as easily be made on a Linux machine. You must have root or superuser permission in order to write to the floppy drive or the /dev/fd0 device. For most users, this is the 1.44 megabyte floppy drive. You may also need to be more specific when listing this device if you have more than one type of floppy drive. A definitive path would be the following: /dev/fd0H11440. This path specifies the initial floppy drive or a:\ drive. If a second floppy drive, or b:\, exists, then the assignment would be /dev/fd1H11440.

![](bbox=[0.14, 0.65, 0.66, 0.91])

![](bbox=[0.7, 0.73, 0.86, 0.88])