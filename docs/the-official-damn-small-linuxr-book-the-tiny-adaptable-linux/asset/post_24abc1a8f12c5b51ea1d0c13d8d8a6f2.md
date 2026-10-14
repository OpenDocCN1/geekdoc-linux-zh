
—DSL web server: Include XAMPP software with DSL to create an instant web server to share your web content over the Internet (see Chapter 16).

- DSL boot images—Some older hardware that has no bootable CD drive (or no CD drive at all) may need a floppy boot image to be able to boot DSL. Several different boot images are included in the /images directory of the CD.

- Chapter 10 and Chapter 11 scripts—Scripts that are described in Chapter 10, “Adding Applications and Creating Shareable Extensions,” and Chapter 11 in this book are contained in the /chapter10 and /chapter11 directories, respectively, on the CD. The scripts will help you make your own MyDSL extensions and remaster your own DSL live CD.

- MyDSL packages—There are several extra software packages that are very popular with DSL users. By including some of these packages, available as software extensions with the MyDSL facility, on the CD, we can save you the trouble of downloading them over the Internet. In the /mydsl directory in the top-level directory of the CD, you can find packages for installing standard GNU utilities (gnu-utils package), ALSA sound drivers and utilities (alsa-sound package), and the OpenOffice.org office applications (openoffice package).

You can use the software contained on the CD if you don’t have an Internet connection. As time goes by, however, you should check the Damn Small Linux website for the availability of later versions of the software included on the CD.

## SUMMARY

Damn Small Linux is the premiere business card-size Linux desktop live CD available today. Within its 50MB footprint, DSL contains nearly every type of application you would expect to find in a modern desktop operating system. Although DSL is designed to run from a read-only CD medium, you can add data, software extensions, and system settings that can be backed up separately and used again the next time you reboot.

This chapter is an introduction to the features that make DSL both a useful and fun operating system for computer enthusiasts. It presents some of the ways in which you can boot, install, reuse, and enhance DSL that are described in greater depth in later chapters of the book. It also discusses ways in which you can learn more about the DSL community and contribute to its success.

This page intentionally left blank

## Booting DSL

Whether you are using a bootable business card purchased from DamnSmallLinux.org (and thank you for the support), the CD that comes with this book, or a Damn Small Linux (DSL) image you downloaded and burned, DSL is made to boot up easily on nearly any PC. In most cases, after you insert the medium, reboot, and press Enter, the DSL desktop (see Figure 2-1) appears in a few moments.

![](img/af53325d7f38f1cdafca9f44568e4ab8_49_0.png)

FIGURE 2-1 The DSL desktop appears automatically when you boot DSL.

## SOFTWARE REQUIREMENTS–DSL VERSIONS

Damn Small Linux is available in several different versions. The version you use depends on the environment in which you are running DSL. The four versions DSL offers include:

- **A SYSLINUX version**—Used for older PCs that require the boot medium to be no larger than a floppy image (even if that image is on a CD). For more information on the SYSLINUX boot loader, refer to the SYSLINUX FAQ (http://syslinux.zytor.com/faq.php).

- **An ISOLINUX version**—Used most often for booting live CDs, because it needs no special floppy emulation disk. For more information on the ISOLINUX boot loader, refer to the ISOLINUX FAQ (http://syslinux.zytor.com/iso.php).

- **A Qemu Virtual Machine version**—Sets up Qemu to run DSL virtually within a running Linux system.

- **A VMware Virtual Machine version**—Sets up VMware to run DSL virtually within a running Windows system.

The first two versions concern booting from the CD, which is the topic of this chapter. The other two versions are discussed in Chapter 7, “Running DSL Embedded in Windows.” Why are there two versions for CD? Because DSL targets older and smaller hardware, many such systems could only boot from a CD if there existed an actual emulated boot floppy. This emulated boot floppy was restricted to the size of a real floppy. Later machines were made without such a restriction.

So, the first rule is this: If your machine cannot begin the boot process, or if your machine is an older variety, use the SYSLINUX version.

The SYSLINUX version of DSL emulates a single floppy at boot time. There are fewer drivers in the SYSLINUX version because they must all fit within a single floppy-sized file. The reason Knoppix and the other derivatives went with ISOLINUX is that there is no single floppy size limitation. The ISOLINUX version has many more drivers to support booting from newer computers.

## GETTING DAMN SMALL LINUX

There are several versions of Damn Small Linux included on the CD that comes with this book. You can read about what those versions are and how to use them by referring to Appendix A, “On the CD.” However, if you don’t have the CD handy or if a later version of DSL is available, you might consider downloading a copy of DSL to make your own bootable CD.
