
# Reference

- http://www.openoffice.org—The home page for the OpenOffice.org office suite.
- http://www.pclinuxonline.com/modules.php?name=News&file=article&sid=3199—A set of links to tips, tricks, and enhancements for OpenOffice.org. One link at the site is to a PDF file that explains how to use OpenOffice.org as a database front end for MySQL.
- http://www.gnome.org/projects/ooo/—The GNOME Office site.
- http://www.koffice.org—The home page for the KOffice suite.
- http://eri.hancom.com/—The home page for the Hancom Office suite.
- http://bulldog.izo.org/webcal/webcal.html—The home page of the excellent WebCal web-based calendar and scheduling program.
- http://www.codeweavers.com—Website of the hugely popular CrossOver Office from CodeWeavers that allows you to run Windows programs under Linux.

# CHAPTER 10

## Multimedia Applications

### IN THIS CHAPTER

- Burning CDs and DVDs in Fedora Core Linux
- Sound and Music
- Viewing TV and Video
- Reference

The twenty-first century has become the century of the digital lifestyle, with millions of computer users around the world embracing new technologies such as digital cameras, MP3 players, and other assorted multimedia gadgets.

Whereas 10 years ago you might have had a collection of WAV files littering your Windows installation, nowadays you are more likely to have hundreds, if not thousands of MP3 files scattered across computers. Along with video clips, animations, and other graphics, the demand for organizing and maintaining these vast libraries is driving development of applications. Popular proprietary applications such as iTunes and Google's Picasa are coveted by Linux users, but open source applications are starting to appear that provide real alternatives, and for some the final reasons they need to move to Linux full time.

This chapter provides an overview of some of the basic multimedia tools included with Fedora. You will see how to create your own CDs, watch TV, rip audio CDs into the open source OGG audio format for playback, as well as manage your media library.

> **NOTE**
>
> Continuing a move that began with the release of Red Hat 9, The Fedora Project maintains a philosophy that has been controversial with many longtime users. Because of concerns of potential liability arising from copyright and patent issues in the United States, Red Hat and The Fedora Project have voluntarily removed any functionality that could violate the intellectual property rights of others or subject Red Hat to any penalties. That does not mean individual users would be violating those same rights, so we have provided resources to the reader as to how some of that functionality can be restored; the choice is yours.

By installing and using xine as described in Chapter 7, "Managing Software," you can easily restore full multimedia functionality to Fedora.

Because Fedora uses UTF-8 language encoding, some non-Fedora applications will have display problems if they are not UTF-8 compliant. You can fix this by placing the following line in /etc/bashrc:

```
export LANG=en_US_SUPPORTED=en_US
LC_MESSAGES=C LC_ALL=C
```

### Burning CDs and DVDs in Fedora Core Linux

Linux is distributed across the Internet by using ISOs that are waiting to be written to CDs or DVDs. Therefore learning how to burn discs is essential if you have to download and install a Linux distribution. Not only that, but you are likely to want to use CDs and, more commonly, DVDs to back up your music, family pictures, or other important files. With DVD writers being so cheap, the format has really taken off and more and more people use cheap DVDs as way of archiving simply due to the larger storage size available. Today's high-resolution digital cameras can occupy upward of 3MB per shot, and music files can be anything from 1MB to 10MB+ in size. These file sizes make DVD the obvious choice, but there are still occasions when you need to write to a CD. You can use CDs and DVDs to

- Record and store multimedia data, such as backup files, graphics images, and music, on to a CD or DVD.
- Rip audio tracks from a music CD (*ripping* refers to extracting music tracks from a music CD) and compile your own music CD for your personal use.

Linux audio clients and programs support the creation and use of many different types of audio formats. Later sections of this chapter discuss sound formats, sound cards, music players, and much more. Because CD burning is used for many other purposes in Fedora, we cover the essentials of that process first in this chapter. To record multimedia data on a CD, you must have installed a drive with CD writing capabilities on your system. Chapter 4, "Post-Installation Configuration," explains the rudiments of getting a CD writer configured and working properly. The hardware should have been set up properly during the initial Fedora installation or configured properly when detected by Kudzu. To make certain that your CD writer is working, use `cdrecord -scansbus` to get the information for using the CD drive under SCSI (small computer system interface) emulation:

```
# cdrecord -scansbus
Cdrecord-Clone 2.01a32-dvd (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling

Linux sg driver version: 3.5.27
Using libsgv version 'schily-0.8'
scsibus0:
0,0,0  0)  'HL-DT-ST'  'RW/DVD GCC-4120B'  '2.01'  Removable CD-ROM
0,1,0  1)  *
0,2,0  2)  *
0,3,0  3)  *
0,4,0  4)  *
0,5,0  5)  *
0,6,0  6)  *
0,7,0  7)  *
```

Here, we see that the CD writer (in this example, a CD writer/DVD reader) is present and is known by the system as device 0, 0, 0. The numbers represent the scsi/bus/target/lun (logical unit number) of the device. You need to know this device number when you burn the CD, so write it down or remember it.

> **TIP**
>
> An IDE drive used to create CDs and DVDs needs to be emulated as a SCSI drive. Fedora does this automatically when you first install it, but in case you need to do it manually, here are the few items you need to configure (assuming that the CD drive is at /dev/hdd):
> - Add the following line to the /etc/modules.conf file:
>   `probeall ide-scsi`
> - Edit the /boot/grub/menu.lst file to add the following to the kernel commands:
>   `hd=ide-scsi`
> - Reboot your computer.
>
> These items load the appropriate modules and provide SCSI emulation. You would no longer refer to the CD drive as /dev/hdd, but as /dev/scd0. Check the symbolic for /dev/cdrom to make certain that it points to /dev/scd0.
>
> However, because Fedora now uses the 2.6 kernel, SCSI emulation is not necessary, although it is useful information should something not work correctly.

#### Creating CDs from the Command Line

In Linux, creating a CD is a two-step process. You first create the iso9660-formatted image, and you then burn or write the image onto the CD. The iso9660, as you will learn in Chapter 38, “Managing the File System,” is the default file system for CD-ROMs.

Use the `mkisofs` command to create the ISO image. The `mkisofs` command has many options (see the man page for a full listing), but use the following for quick burns:

```
$ mkisofs -r -v -J -l -o /tmp/our_special_1cd.iso /source_directory
```

The options used in this example are as follows:

- **-r**—Sets the permission of the files to more useful values. UID and GID (individual and group user ID requirements) are set to zero, all files are globally readable and searchable, and all files are set as executable (for Windows systems).
- **-v**—Displays *verbose* messages (rather than terse messages) so that you can see what is occurring during the process; these messages can help you resolve problems if they occur.
- **-J**—Uses the *joliet* extensions to *iso* so that our Windows-using buddies can more easily read the CD. The *joliet* (for Windows), Rock Ridge (for UNIX), and HFS (for Mac) extensions to the *iso9660* standard are used to accommodate long filenames rather than the eight-character DOS filenames that the *iso9660* standard supports.
- **-l**—Allows 31-character filenames; DOS does not like it, but everyone else does.
- **-o**—Defines the directory where the image will be written (that is, the *output*) and its name. The *output* directory is *convenient* for the purpose, but the image could go anywhere you have write permissions.
- **Source directory**—Indicates the path to the source directory; that is, the directory containing the files you want to include. There are ways to append additional paths and exclude directories (and files) under the specified path—it is all explained in the man page. If you need that level of complexity, our simple solution is to construct a new directory tree and populate it with the files we want to copy, and then make the image using that directory as the source.

Many more options are available, including options to make the CD bootable.

After you have created the ISO image, you can write it to the CD with the `cdrecord` command:

```
$ cdrecord -eject -v speed=12 dev=0,0,0 /tmp/our_special_cd.iso
```

The options used in this example are as follows:

- ***eject*—Ejects the CD when the write operation is finished.**
- ***v*—Displays verbose messages.**
- ***speed*—Sets the speed; the rate depends on the individual drive's capabilities. If the drive or the recordable medium is poor, you can use lower speeds to get a good burn.**
- ***dev*—Specifies the device number of the CD writer (the number I told you to write down earlier).**

> **NOTE**
>
> You can also use the `blank=` option with the `cdrecord` command to erase CD-RW disks. The `cdrecord` command has fewer options than `mkisofs` does, but it offers the `-multi` option, which enables you to make multisession CDs. A multisession CD enables you to write a data track, quit, and then add more data to the CD later. A single-session CD can be written to only once; any leftover CD capacity is wasted. Read about other options in the `cdrecord` man page. Current capacity for CD media is 700MB of data or 80 minutes of music. (There are 800MB/90-minute CDs, but they are rare.) Some CDs can be overburned; that is, recorded to a capacity in excess of the standard. The `cdrecord` command is capable of overburning if your CD-RW drive supports it. You can learn more about overburning CDs at http://www.cdmediaworld.com/hardware/cdrom/cd_oversize.shtml/
