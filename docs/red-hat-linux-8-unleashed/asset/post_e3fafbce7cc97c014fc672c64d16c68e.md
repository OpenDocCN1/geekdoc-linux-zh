
## Root password
rootpw --encrypted $1$/n3yjyDV$AWOBzGRq/1AxRyHx1JSM1

Note that not the output of a sample ks.cfg is shown. However, you can see that this file will feed kickstart directions for an install, including an encrypted root password to be installed on the target Red Hat system.

The next step is to copy your new ks.cfg to a boot disk created using one of the Red Hat boot floppy images (under the images directory on the first Red Hat Linux CD-ROM). You can do this with Linux using the mount and cp commands. For example, take your Red Hat boot disk (created according to directions in the section “Making an Installation Boot Diskette in Chapter 3), insert it into your PC, and then use the mount command (as root) like so:

```bash
# mount /mnt floppy
```

If Red Hat has mounted your floppy automatically, you'll receive an error message such as /dev/fd0 already mounted. You can then simply copy ks.cfg file to the floppy like so:

```bash
# cp ks.cfg /mnt/floppy
```

You can verify the contents of the floppy using the ls command like this:

```bash
# ls /mnt/floppy
boot.msg general.msg inititrd.img ks.cfg llinux.sys
options.msg param.msg rescue.msg snake.msg splash.lss
syslinux.cfg syslinux.png vmlinuz
```

Then unmount the floppy using the umount command like so:

```bash
# umount /mnt/floppy
```

Remove the disk. It is now ready for use. When you use the disk to boot a PC, after booting, the install boot image you'd like to perform a kickstart install like this:
linux ks=floppy

The installer will then use the specifications outlined in the Kickstart Configurator and saved in ks.cfg to install Red Hat Linux.

## Reference

The following is a list of references you can use to learn a bit about partitioning, installation tools, and installing Red Hat Linux and Linux variants on a variety of hardware-. You'll also find information about installation on hardware for embedded and mainframe solutions.

## CHAPTER 2 Preparing to Install Red Hat Linux

- http://www.redhat.com/solutions/migration—Red Hat's helpful Migration Center, with news, white papers and other tips and research on migrating to a Linux solution.
- http://www.yale.edu/pclt/BOOT/DEFAULT.HTM—A basic primer to partitioning that is operating system nonspecific.
- http://www-1.ibm.com/linux/~—Home page for Linux at IBM, with links to products, services, and downloads.
- http://oss.software.ibm.com/developerworks/opensource/linux390/index.html—Home page for IBM S/30 Linux solutions.
- http://www.esfr.fr/computing/sysadmin/rtk/pc104project/howto/linux/master_hw.htm—One approach to installing and using Linux on a PC-104 single-board computer (SBC).
- http://www.dell.com/us/en/bd/topics/linux_aacraid.—Dell Computer’s server lineup running Red Hat Linux.
- http://www.dell.com/us/en/bd/topics/linux_000_linux_products.htm—Links to Dell computers available with Red Hat Linux.
- http://www.redhat.com/support/hardware/—Entry point to Red Hat's hardware compatibility database.
- http://linux1394.sourceforge.net/—Home page for the Linux Firewire Project, with information regarding the status of drivers and devices for this port.
- http://www.linux-usb.org—Home page for the Linux USB Project, with lists of devices and links to drivers.
- http://www.schirmacher.de/arne/dvgrab/dvgrab_features_e.html—Digital video grab software (via Firewire) for Linux.
- http://www.elks.ecs.soton.ac.uk/—Home page for Linux for x286 and below CPUs, ELKS Linux.
- http://open-projects.linuxcare.com/BBC/—Home page for the Bootable Business Card, a 50MB compressed distribution that offers hundreds of networking clients, a X session, web browsing, PDA backup, wireless networking, rescue sessions, and file recovery.
- http://www.cotoyimus.com—Home page for several compact Linux distributions offering firewall and VPN services; the floppy-based distribution works quite well on older PCs and does not require a hard drive.
- http://www.freesco.org/—Home page for a floppy-based Linux router solution that works on 386 PCs, requires only 6MB RAM, and provides bridging, firewalling, IP masquerading, DNS, DHCP, Web, telnet, print, time, and remote access functions.
- http://www.linux.org/vendors/systems.html—One place to check for a vendor near you Linux preinstalled on a PC, laptop, server, or hard drive.

## CHAPTER 3: Installing Red Hat Linux

In this chapter, you learn how to do a basic installation of Red Hat Linux. You'll see how to boot and then install Red Hat installer using the CD-ROMs included with this book. The chapter first shows how to prepare and research your install, choose a strategy on how Red Hat will use your computer's hard drive, decide how to boot Red Hat, and then how to complete the Red Hat installation. You'll get a

- Choosing How to Install Red Hat
- Step-by-Step Installation
- Login and Shutdown
- Reference

## Preparing for the Installation

Part of planning a custom system involves implementing a partitioning strategy based on how you plan to use Red Hat and, as previously mentioned, the capabilities of your existing hardware. For example, if you plan to host thousands of graphic images or audio files,
