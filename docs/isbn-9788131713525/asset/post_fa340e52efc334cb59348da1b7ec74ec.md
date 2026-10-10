
## 7.5 Other Bootloaders

Here we introduce the more popular bootloaders, describe where they might be used, and give a summary of their features. This is not intended to be a thorough tutorial because to do so would require a book of its own. The interested reader can consult the “Suggestions for Additional Reading” at the end of this chapter for further study.

### 7.5.1 Lilo

The Linux Loader, or Lilo, was widely used in commercial Linux distributions for desktop PC platforms; as such, it has its roots in the Intel x86/IA32 architecture. Lilo has several components. It has a primary bootstrap program that lives on the first sector of a bootable disk drive.⁴ The primary loader is limited to a disk sector size, usually 512 bytes. Therefore, its primary purpose is simply to load and pass control to a secondary loader. The secondary loader can span multiple partitions and does most of the work of the boot loader.

Lilo is driven by a configuration file and utility that is part of the lilo executable. This configuration file can be read or written to only under control of the host operating system. That is, the configuration file is not referenced by the early boot code in either the primary or secondary loaders. Entries in the configuration file are read and processed by the lilo configuration utility during system installation or administration. Listing 7-10 is an example of a simple lilo.conf configuration file describing a typical dual-boot Linux and Windows installation.

#### Listing 7-10
**Example Lilo Configuration: lilo.conf**

```
# This is the global lilo configuration section
# These settings apply to all the “image” sections.
boot = /dev/hda
timeout=50
default=linux
```

> ⁴This is mostly for historical reasons. From the early days of PCs, BIOS programs loaded only the first sector of a disk drive and passed control to it.

# This describes the primary kernel boot image
# lilo will display it with the label `linux'
image=/boot/myLinux-2.6.11.1
label=linux
initrd=/boot/myInitrd-2.6.11.1.img
read-only
append="root=LABEL=/"

# This is the second OS in a dual-boot configuration
# This entry will boot a secondary image from /dev/hda1
other=/dev/hda1
optional
label=that_other_os

This configuration file instructs the Lilo configuration utility to use the master boot record of the first hard drive (/dev/hda). It contains a delay instruction to wait for the user to press a key before the timeout (5 seconds, in this case). This gives the system operator the choice to select from a list of OS images to boot. If the system operator presses the Tab key before the timeout, Lilo presents a list to choose from. Lilo uses the label tag as the text to display for each image.

The images are defined with the *image* tag in the configuration file. In the example presented in Listing 7-10, the primary (default) image is a Linux kernel image with a file name of *myLinux-2.6.11.1*. Lilo loads this image from the hard drive. It then loads a second file to be used as an initial ramdisk. This is the file *myInitrd-2.6.11.1.img*. Lilo constructs a kernel command line containing the string "root=LABEL=/" and passes this to the Linux kernel upon execution. This instructs Linux where to get its root file system after boot.

### 7.5.2 GRUB

Many current commercial Linux distributions now ship with the GRUB boot-loader. GRUB, or GRand Unified Bootloader, is a GNU project. It has many enhanced features not found in Lilo. The biggest difference between GRUB and Lilo is GRUB's capability to understand file systems and kernel image formats. Furthermore, GRUB can read and modify its configuration at boot time. GRUB also supports booting across a network, which can be a tremendous asset in an embedded environment. GRUB offers a command line interface at boot time to modify the boot configuration.

Like Lilo, GRUB is driven by a configuration file. Unlike Lilo's static configuration however, the GRUB bootloader reads this configuration at boot time. This means that the configured behavior can be modified at boot time for different system configurations.

Listing 7-11 is an example GRUB configuration file. This is the configuration file from the PC on which this manuscript is being written. The GRUB configuration file is called grub.conf and is usually placed in a small partition dedicated to storing boot images. On the machine from which this example is taken, that directory is called /boot.

#### Listing 7-11
**Example GRUB Configuration File: grub.conf**

```
default=0
timeout=3
splashimage=(hd0,1)/grub/splash.xpm.gz

title Fedora Core 2 (2.6.9)
	root (hd0,1)
	kernel /vmlinuz-2.6.9 ro root=LABEL=/ rhgb proto=imps quiet
	initrd /initrd-2.6.9.img

title Fedora Core (2.6.5-1.358)
	root (hd0,1)
	kernel /vmlinuz-2.6.5-1.358 ro root=LABEL=/ rhgb quiet

title That Other OS
	rootnoverify (hd0,0)
	chainloader +1
```

GRUB first presents the user with a list of images that are available to boot. The title entries from Listing 7-11 are the image names presented to the user. The default tag specifies which image to boot if no keys have been pressed in the timeout period, which is 3 seconds in this example. Images are counted starting from zero.

Unlike Lilo, GRUB can actually read a file system on a given partition to load an image from. The root tag specifies the root partition from which all filenames in the grub.conf configuration file are rooted. In this example configuration, the root is partition number 1 on the first hard disk drive, specified as root(hd0, 1). Partitions are numbered from zero; this is the second partition on the first hard disk.

The images are specified as filenames relative to the specified root. In Listing 7-11, the default boot image is a Linux 2.6.9 kernel with a matching initial ramdisk image called initrd-2.6.9.img. Notice that the GRUB syntax has the kernel command line parameters on the same line as the kernel file specification.

### 7.5.3 Still More Bootloaders

Numerous other bootloaders have found their way into specific niches. For example, Redboot is another open-source bootloader that Intel and the XScale community have adopted for use on various evaluation boards based on the Intel IXP and PXA processor families. Micromonitis is in use by board vendors such as Cogent and others. YAMON has found popularity in MIPS circles.³ LinuxBIOS is used primarily in X86 environments. In general, when you consider a boot loader, you should consider some important factors up front:

- Does it support my chosen processor?
- Has it been ported to a board similar to my own?
- Does it support the features I need?
- Does it support the hardware devices I intend to use?
- Is there a large community of users where I might get support?
- Are there any commercial vendors from which I can purchase support?

These are some of the questions you must answer when considering what boot-loader to use in your embedded project. Unless you are doing something on the “bleeding edge” of technology using a brand-new processor, you are likely to find that someone has already done the bulk of the hard work in porting a boot-loader to your chosen platform. Use the resources at the end of this chapter to help make your final decisions.

> ³ In an acknowledgment of the number of bootloaders in existence, the YAMON user’s guide bills itself as Yet Another MONitor.

## 7.6 Chapter Summary

- The bootloader’s role in an embedded system cannot be overstated. It is the first piece of software that takes control upon applying power.

### 7.5 Other Bootloaders (Previous Page Content Correction & Consolidation)

*Note: The following content from Page 213 appears to be part of the discussion leading into Section 7.5 or a subsection of 7.4 which was cut off in the OCR page break. It describes U-Boot's mkimage parameters.*

Ignoring the syntactical complexity, understand that this rule calls a shell script identified by the variable \$(MKIMAGE). The shell script executes the U-Boot mkimage utility with the parameters shown. The mkimage utility creates the U-Boot header and prepends it to the supplied kernel image. The parameters are defined as follows:

- **-A** Specifies the target image architecture
- **-O** Specifies the target image OS—in this case, Linux
- **-T** Specifies the target image type—a kernel, in this case
- **-C** Specifies the target image compression type—here, *gzip*
- **-a** Sets the U-Boot *loadaddress* to the value specified—in this case, 0
- **-e** Sets the U-Boot image entry point to the supplied value
- **-n** A text field used to identify the image to the human user
- **-d** The executable image file to which the header is prepended

Several U-Boot commands use this header data both to verify the integrity of the image (U-Boot also puts a CRC signature in the header) and to instruct various commands what to do with the image. U-Boot has a command called *iminfo* that reads the image header and displays the image attributes from the target image. Listing 7-9 contains the results of loading a *uImage* (bootable Linux kernel image formatted for U-Boot) to the EP405 board via U-Boot’s *tftpboot* command and executing the *iminfo* command on the image.

#### Listing 7-9
**U-Boot *iminfo* Command**

```
=> tftpboot 400000 uimage-ep405
TFTP Speed 100 Mbps = FULL duplex connection
TFTP from server 192.168.1.9; our IP address is 192.168.1.33
Filename 'uimage-ep405'.
Load address: 0x400000
     Loading: ##########   done
Bytes transferred = 891228 (d995c hex)
=> iminfo

## Checking Image at 04040000 ... 
   Image Name:   Linux-2.6.11.6
   Image Type:   PowerPC Linux Kernel Image (gzip compressed)
   Data Size:    891164 Bytes = 870.3 kB
   Load Address: 00000000
   Entry Point:  00000000
              Verifying Checksum ... OK
=>
```
