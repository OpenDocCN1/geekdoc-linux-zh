
to be defragmented first.

Perform any required repartitioning successfully, but requires the disc to be defragmented first.

Frankly, unless you are fairly expert with partitioning and installing operating systems, it is probably best to boot up for a dual-boot set-up by using the CD-ROM Setup program. This will not actually do the repartitioning for you, but a complete version of the program is included on the Linux CD and can be run from the hard drive or from the CD-ROM drive.

Even if you are more experienced, I would not recommend installing Linux onto a clean section of a hard drive in an old and otherwise unused PC. Installing Linux on a cheap second-hand PC is a much easier and safer way of trying out this operating system.

## Getting started

If you have bought a set of Linux discs complete with manuals it obviously makes sense to follow the instructions in the manual which will give you detailed accounts of how to install that particular version of Linux. If you have a magazine disc which includes instructions or some other documentation, use that. As the exact method of installation varies from one distribution to another and from one version to the next, I am not able to give comprehensive general guidance here. As you are installing what is essentially the same thing regardless of which distribution you are using, the general procedure is much the same.

Many of the steps are straightforward, so we will concentrate here on the more awkward aspects of installation.

In order to install Linux you normally have to boot-up the computer in a sort of mini-Linux so that the installation software can be run. In the past it was something like a set of boot disks in order to get Linux installed, but boot disks are not normally required these days. So I would suggest that if you are supplied with a boot disk, buy a "boxed" version of Linux. It may be a bit more expensive but it's the only sensible option. If you don't have a suitable drive or bootable CD-ROM, try booting the basic version of the driver or co-op mode. It will be able to use the CD-ROM, but from this it will do no more than three critical tasks. Next, most of the time will be spent working with the CD-ROM Setup program. The CD-ROM must be in the CD-ROM drive so that all of the computer can use it. Any new computer must, for the time being, boot with a bootable floppy disk (bootable CD-ROM). In fact, the CD-ROM is usually no problem when using an ordinary ATAPI CD-ROM drive.

A modern AMD BIOS has a sort of simple graphical user interface, complete with support for some types of mouse. Select the "Advanced" option.

## Installation 1

CD-ROM if the correct boot options have been set in the BIOS Setup program.

If you wish to try booting from the CD-ROM it will almost certainly be necessary to go into the Setup program and select a suitable boot option. This is not sure whether or not your PC must boot the CD-ROM drive first so that the Setup program can be used. Also, if you are not sure whether or not your PC support this boot, check with your manual. This can be done in the Setup program. It is only used to prevent the computer from using the CD-ROM boot option.

![](img/147f057d2f063d8c60ee616870537a94_15_0.png)

![](img/147f057d2f063d8c60ee616870537a94_15_1.png)

the Windows 98 installation process. A start-up disc can be made by selecting Start, Settings, Control Panel, Add/Remove Programs, Startup Disk, and then operating the “Create Disk” button. A 1.44-MB formatted 1.44-MB disc should be placed in drive A: prior to operating the “Create Disk” button, or use a switch on a computer with a floppy drive after a system will probably not need to be booted from the first boot device.

go into the BIOS Setup program and a simple menu will appear, and the option of CD-ROM support. When the boot CD-ROM support should be selected.

Alternatively, a floppy disk can be formatted using MS-DOS. To make the disk bootable, it should be used when issuing the format command, as shown below:

```
format A:/s
```

It is also possible to add the system files to an ordinary formatted floppy disc using the SYS program supplied with MS-DOS. This is the instruction that would be used:

```
SYS A:
```

Note that the Format and Sys commands are not internal parts of MS-DOS, and the computer must be able to access the relevant program files for either of these to work.

Having made a boot-up disc, it is then a matter of booting up the computer using the disc, and then adding CD-ROM support to the boot disc. The option from the initial screen (Figure 1.3), and then “First Boot Device” from the next screen (Figure 1.4). Select “CD-ROM”, and then return to the main menu. Click the mouse on the small box in the top left hand corner of the window to exit the main menu, and then click on the Save Changes and Exit box to actually save the new set-up information. It should also be possible to boot from the newly installed CD. Note that no Setup will be necessary if the new installation settings are the same as the original boot settings. This is because the computer may fail to boot correctly from the hard drive unless it is done.

## Direct from CD-ROM

If you can not boot from the CD-ROM for one reason or another, it should be possible to just make a boot-up disc from the original DOS disc and the CD-ROM will be booted, as the DOS version on the CD-ROM support be added. The easiest way is to use a Windows 98 start-up disc, which is normally made during

![](img/147f057d2f063d8c60ee616870537a94_16_0.png)

```
Advanced Setup
1st Boot Device
2nd Boot Device  : CDROM
3rd Boot Device  : Disabled
Boot From Network Card : Disabled
Try Other Boot Devices : No
S.M.A.R.T. for Hard Disks : Enabled
Quick Boot : Enabled
Bootly Num-Lock : Off
Floppy Drive Setup : Disabled
```

![](img/147f057d2f063d8c60ee616870537a94_16_1.png)

Fig 1.4 Set the first boot device as “CDROM”

messages tell you what the computer is doing as it boots into a sort of minimalistic version of Linux. Unless you are a Linux expert most of the messages will not make a great deal of sense. Just ignore them and wait patiently for the installation program to run.

Many of the questions are very simple and just require you to select such things as the language to be used and the time zone you are in. Some Linux distributions are supplied with an installation program that, like the boot menu on CD-ROM, will ask a series of Yes or No questions. For Linux with minimal questions, such as Debian, the answers will be found in the documentation or online manual. The more important questions are: the username, the password and whether you want to install the full operating system or just the basic utilities. Installation programs are this obligation and an automatic installer may work with your particular PC. If necessary, look into the complete installation program so that you will understand how it works and can fix any problems you may encounter. Be careful about using Linux from a different directory. It is often difficult to boot up a new system from scratch. You will have to redo a complete section of the installation from scratch.

## Fig 1.3 Select the “Advanced” menu

computer or CD-ROM drive should be supplied with the necessary installation software or a reboot so that the added CD-ROM support takes effect, and you have access to the CD-ROM drive.

It is then a matter of exploring the files on the CD-ROM to track down the file that is used to launch the installation process. There may be a batch file called something like setup.exe or install.bat. There will be some readme files on the CD and one of these should tell you what you need to know. When you have located the appropriate file, it is likely that running it will start the installation procedure. It is safer to go the the root directory of the CD by specifying the path to the file. It is safer to go into the directory that contains the file and run it from there.

## Questions and answers

Once past the installation process it is largely a matter of answering a series of questions. It may take a while to get to the first question, with numerous obscure messages appearing on the screen first. These
