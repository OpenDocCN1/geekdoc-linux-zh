**Monitor:** The kind of monitor is not particularly critical except that it must be capable of displaying the screen resolutions that the video card uses. The screen resolution is expressed in terms of the number of picture elements (pixels), horizontally and vertically (for example, *1024 x 768*). The installer can detect most modern monitors. If it does not detect, you can select a generic monitor type with a specific resolution such as *1024 x 768*. You can also specify the monitor by its make and model (which you can find on the back of the monitor).

**Network card:** Not all PCs have network cards, but if yours does, the installer can probably detect and use it. If you have problems, try to find the make and model (such as *Linksys LNE100TX Fast Ethernet Adapter*) so that you can search for information on whether Linux supports that card or not.

**SCSI controller:** Some high-performance PCs have SCSI controllers that connect disk drives and other peripherals to a PC. If your PC happens to have a SCSI controller, you might want to find out the make and model of the controller.

**Sound card:** If your PC has a sound card and you want to have sound in Fedora Core, you have to make sure it’s compatible. You can configure the sound card after successfully installing Fedora Core.

**Modem:** If you plan to dial out to the Internet, you need a modem that Linux supports. For software-based modems, called soft modems or win-modems, you may have to download a driver from the manufacturer (it may or may not be freely available).

In addition to this hardware, you need to also find out the make and model of any printer you plan to use in Fedora Core.

# # Setting Aside Space for Fedora Core

In a typical Windows PC, Windows is sitting on a big partition, taking over the whole disk. You want to shrink that partition and create room for Linux. During Linux installation, the installation program uses that free space for the Linux partitions.

The challenge is to resize the current partition without destroying anything on the hard disk. I cover tools that help you resize the partition, but first you have to make sure that all used areas of the disk are *contiguous*, or as tightly packed as possible. This is where defragmenting comes in.

# ## Defragmenting your hard disk

“Defrag your disk” is the magic chant of many a help desk. It’s the help desk’s prescription for all PC ailments. Well, for once they’re right —