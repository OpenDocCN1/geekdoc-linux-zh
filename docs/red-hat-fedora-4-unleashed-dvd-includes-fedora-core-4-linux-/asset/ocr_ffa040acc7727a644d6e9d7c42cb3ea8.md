By installing and using apt or yum as described in Chapter 7, “Managing Software and System Resources,” you can easily restore full multimedia functionality to Fedora.
Because Fedora uses UTF-8 language encoding, some non-Fedora applications will have display problems if they are not UTF-8 compliant. You can fix this by placing the following line in /etc/bashrc:

```
export LANG=en_US SUPPORTED="en_US"
LC_MESSAGES=C LC_ALL=C
```

# # Burning CDs and DVDs in Fedora Core Linux

Burning (or creating) your own CDs is a fundamental skill for Linux multimedia enthusiasts. The CD and DVD (digital versatile disc) have become the standard media for multimedia content because of the increasingly larger size of typical media files. (Individual songs, even in compressed audio format, usually require several megabytes of storage space.) You can use CDs to

+   -   Record and store multimedia data, such as backup files, graphics images, and music, on a CD.
+   -   Rip audio tracks from a music CD (ripping refers to extracting music tracks from a music CD) and compile your own music CD for your personal use.

Linux audio clients and programs support the creation and use of many different types of audio formats. Later sections of this chapter discuss sound formats, sound cards, music players, and much more. Because CD burning is used for many other purposes in Fedora, we cover the essentials of that process first in this chapter. To record multimedia data on a CD, you must have installed a drive with CD writing capabilities on your system. Chapter 4, “Post-Installation Configuration,” explains the rudiments of getting a CD writer configured and working properly. The hardware should have been set up properly during the initial Fedora installation or configured properly when detected by Kudzu. To make certain that your CD writer is working, use cdrecord -scanbus to get the information for using the CD drive under SCSI (small computer system interface) emulation:

```
# cdrecord -scanbus
Cdrecord-Clone 2.01a32-dvd (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling

Linux sg driver version: 3.5.27
Using libscg version 'schily-0.8'
scsibus0:
	s0,0,0  0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
	s0,1,0  1) *
	s0,2,0  2) *
	s0,3,0  3) *
	s0,4,0  4) *
```