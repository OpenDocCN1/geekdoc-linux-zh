# Burning CDs and DVDs in Ubuntu

Linux is distributed across the Internet through the use of ISOs that are waiting to be written to CDs or DVDs. Therefore, learning how to burn discs is essential if you have to download and install a Linux distribution. Not only that, but you are likely to want to use CDs and, more commonly, DVDs to back up your music, family pictures, or other important files. With DVD writers being so cheap, the format is now pervasive, and more and more people use cheap DVDs as way of archiving simply due to the larger storage size available. Of course, you can use blank CD media, but they don’t have anywhere near the capacity offered by DVDs albeit being slightly cheaper. Today’s high-resolution digital cameras can occupy upward of 3MB per shot, and music files can be anything from 1MB to 10MB+ in size. These file sizes make DVD the obvious choice, but there are still occasions when you need to write to a CD. You can use CDs and DVDs to

+   - Record and store multimedia data, such as backup files, graphics images, and music.
+   - Rip audio tracks from music CDs (ripping refers to extracting music tracks from a music CD) and compile your own music CDs for your personal use.

Linux audio clients and programs support the creation and use of many different types of audio formats. Later sections of this chapter discuss sound formats, sound cards, music players, and much more. Because CD burning is used for many other purposes in Ubuntu, we cover the essentials of that process first in this chapter. To record multimedia data on a CD, you must have installed a drive with CD writing capabilities on your system. To make certain that your CD writer is working, use wodim -scanbus to get the information for using the CD drive under SCSI (small computer system interface) emulation:

```
# wodim -scanbus
Cdrecord-Clone 2.01a32-dvd (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.5.27
Using libscg version 'schily-0.8'
scsibus0:
    0,0,0     0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
    0,1,0     1) *
    0,2,0     2) *
    0,3,0     3) *
    0,4,0     4) *
    0,5,0     5) *
    0,6,0     6) *
    0,7,0     7) *
```

Here, you can see that the CD writer (in this example, a CD writer/DVD reader) is present and is known by the system as device 0,0,0. The numbers represent the scsi bus/target/lun (logical unit number) of the device. You need to know this device number when you burn the CD, so write it down or remember it.