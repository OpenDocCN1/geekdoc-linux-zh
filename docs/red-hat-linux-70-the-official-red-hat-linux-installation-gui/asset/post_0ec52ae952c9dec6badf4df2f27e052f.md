
## Figure A-4 Unresolved Dependencies

![](img/f097eb927132822630978994ad35bce4_112_0.png)

### A.5 Installing LILO

In order to be able to boot your Red Hat Linux system, you usually need to install LILO (the Linux LOader). You may install LILO in one of two places:

- The master boot record (MBR)

  The recommended place to install LILO, unless the MBR already starts another operating system loader, such as System Commander or OS/2’s Boot Manager. The master boot record is a special area on your hard drive that is automatically loaded by your computer’s BIOS, and is the earliest point at which LILO can take control of the boot process. If you install LILO in the MBR, when your machine boots, LILO will present a `boot:` prompt. You can then boot Red Hat Linux or any other operating system you configure LILO to boot.

- The first sector of your root partition

  Recommended if you are already using another boot loader on your system (such as OS/2's Boot Manager). In this case, your other boot loader will take control first. You can then configure that boot loader to start LILO (which will then boot Red Hat Linux).

### Figure A–5 LILO Configuration

![](img/f097eb927132822630978994ad35bce4_113_0.png)

If you choose to install LILO, please select where you would like LILO to be installed on your system (see Figure A–5, *LILO Configuration*). If your system will use only Red Hat Linux you should choose the master boot record (MBR). For systems with Win95/98, you also should install LILO to the MBR so that LILO can boot both operating systems.

If you have Windows NT (and you want to install LILO) you should choose to install LILO on the first sector of the root partition, not the MBR. Please be sure to create a boot disk. In a case such as this, you will either need to use the boot disk, or configure the NT system loader to boot LILO from the first sector of the root partition. Be sure to check out <http://www.linuxdoc.org/HOWTO/mini/Linux+NT-Loader.html> for more information on setting up LILO and NT.

#### CAUTION

If you choose not to install LILO for any reason, you will not be able to boot your Red Hat Linux system directly, and will need to use another boot method (such as a boot diskette). Use this option only if you are sure you have another way of booting your Red Hat Linux system!

The `Use linear mode` button is selected by default. In most cases, linear mode should be enabled; if your computer cannot use linear mode to access your hard drives, deselect this option.

If you wish to add default options to the LILO boot command, enter them into the `kernel parameters` field. Any options you enter will be passed to the Linux kernel every time it boots.

**Bootable Partition** -- Every bootable partition is listed, including partitions used by other operating systems. The "Boot label" column will be filled in with the word `linux` on the partition holding your Red Hat Linux system's root filesystem. Other partitions may also have boot labels. If you would like to add boot labels for other partitions (or change an existing boot label), click once on the partition to select it. Once selected, you can change the boot label.

#### Please Note

The "Boot label" column lists what you must enter at LILO's `boot:` prompt in order to boot the desired operating system. However, if you forget the boot labels defined on your system, you can always press [Tab] at LILO's `boot:` prompt to display a list of defined boot labels.

### A.5.1 Configuring LILO

- **Create boot disk** -- The **Create boot disk** option is checked by default. If you do not want to create a boot disk, you should deselect this option. However, we strongly urge you to create a boot disk. A boot disk can be handy for a number of reasons:
  - **Use It Instead of LILO** -- You can use a boot disk instead of LILO. This is handy if you’re trying Red Hat Linux for the first time, and you’d feel more comfortable if the boot process for your other operating system is left unchanged. With a boot disk, going back to your other operating system is as easy as removing the boot disk and rebooting. If you would rather use a boot disk instead of LILO, make sure you enable the Do not install LILO option.
  - **Use It If Another Operating System Overwrites LILO** -- Other operating systems may not be as flexible as Red Hat Linux when it comes to supported boot methods. Quite often, installing or updating another operating system can cause the master boot record (originally containing LILO) to be overwritten, making it impossible to boot your Red Hat Linux installation. The boot disk can then be used to boot Red Hat Linux so you can reinstall LILO.
  - **Do not install LILO** -- If you have Windows NT installed on your system, you may not want to install LILO. If you choose not to install LILO for this reason, make sure that you have chosen to create a boot disk; otherwise you will not be able to boot Linux. You can also choose to skip LILO if you do not want to write LILO to your hard drive.

#### Tip

To use the boot disk with rescue mode, you have several options:

- Using the CD-ROM to boot, type `linux rescue` at the `boot:` prompt.
- Using the network boot disk, type `linux rescue` at the `boot:` prompt. You will then be prompted to pull the rescue image from the network.
- Using the boot disk included with the Red Hat Linux boxed set, type `linux rescue` at the `boot:` prompt. You then pick an installation method and choose a valid installation tree to load from.

For more information regarding rescue mode, refer to the System Administration chapter of the Official Red Hat Linux Reference Guide.

### A.5.2 Alternatives to LILO

If you do not wish to use LILO to boot your Red Hat Linux system, there are several alternatives:

- **Boot Disk**

  As previously stated, you can use the boot disk created by the installation program (if you elected to create one).

- **LOADLIN**

  You can load Linux from MS-DOS. Unfortunately, it requires a copy of the Linux kernel (and an initial RAM disk, if you have a SCSI adapter) to be available on an MS-DOS partition. The only way to accomplish this is to boot your Red Hat Linux system using some other method (e.g., from LILO on a diskette) and then copy the kernel to an MS-DOS partition. LOADLIN is available from ftp://metalab.unc.edu/pub/Linux/system/boot/dualboot/ and associated mirror sites.

- **SYSLINUX**

  An MS-DOS program very similar to LOADLIN. It is also available from ftp://metalab.unc.edu/pub/Linux/system/boot/loaders/ and associated mirror sites.

- **Some commercial bootloaders**

  For example, System Commander and Partition Magic, which are able to boot Linux (but still require LILO to be installed in your Linux root partition).

### A.5.3 SMP Motherboards and LILO

This section is specific to SMP motherboards only. If the installer detects a SMP motherboard on your system, it will automatically create two `lilo.conf` entries, rather than the usual single entry.

One entry will be called `linux` and the other will be called `linux-up`. The `linux` will boot by default. However, if you have trouble with the SMP kernel, you can elect to boot the `linux-up` entry instead. You will retain all the functionality as before, but you will only be operating with a single processor.

## A.6 Upgrading Packages

At this point there's nothing left for you to do until all the packages have been upgraded or installed (see Figure A–6, *Installing Packages*).

### Figure A–6 Installing Packages

![](img/f097eb927132822630978994ad35bce4_117_0.png)

## A.7 Upgrade Complete

Congratulations! Your Red Hat Linux 7.0 upgrade is now complete!

You will now be prompted to prepare your system for reboot. Don't forget to remove any diskette in the floppy drive or CD in the CD-ROM drive. If you do not have LILO installed, you'll need to use your boot disk now.

#### Tip

If you need a quick review of some of the basic concepts of Red Hat Linux refer to the *Official Red Hat Linux Getting Started Guide*.

For information dealing with system configuration and administration, refer to the *Official Red Hat Linux Reference Guide* on the documentation CD-ROM.

### Figure A-7 Upgrade Complete

![](img/f097eb927132822630978994ad35bce4_118_0.png)
