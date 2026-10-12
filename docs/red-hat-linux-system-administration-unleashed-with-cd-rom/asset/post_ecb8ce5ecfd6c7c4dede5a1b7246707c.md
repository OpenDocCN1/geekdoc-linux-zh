
## LISTING 5.1 continued

```
label = FreeBSD
alias = 5
single-key
table = /dev/hda
```

Let's take this example apart and see what it does by examining the options used. You may be surprised at the level of control you are allowed and some of the interesting things you can do with LILO.

The global section comes first, and as you can see from the boot option, LILO will be installed in place of the master boot record. LILO is expected to optimize the loading process.

Next, we specify the file to be used as the boot sector. This line could be left out of this example because the value used is the default.

Now we come to the message option. In our example, this is set to /etc/lilo.msg. Here are the contents of that file, which as you can see, contain a simple menu and instructions to the user on what to do:

```
+....! Select The OS To Run !....+

1. Red Hat Linux 6.0

2. Experimental Kernel 2.3.6
   (Password Required)

3. Windows 95

4. Fred's Linux

5. FreeBSD 3.0

Defaults to system booted
most recently after 10 seconds

Enter the number of the OS you
wish to start.
```

The file begins with a form feed character. This is generated using vi and typing Ctrl+V followed immediately by Ctrl+L. This character causes LILO to clear the screen before displaying the rest of the file, which contains no color and straight ASCII text only.

### Tip

> There are patches to LILO that allow you to create fancy color screens, and that include the line drawing characters available on the Web at http://www.stack.nl/~stilgar/lilocolors.html.

The next keyword is set to display information about labels, aliases, and other diagnostic information when the lilo map installer is run. The level of messages can be adjusted using this keyword, and the value here of 2 is just my preference.

Next, you'll find a keyword that many people find useful, especially when testing a new kernel. By specifying the lock keyword, LILO remembers which image you last booted, and provided that the currently booted image doesn't have a fallback keyword specified and that you do not crash your system, LILO will keep booting that image until you explicitly request a different image.

The next two keywords are ones that I almost always include in lilo.conf. They are the prompt and timeout keywords. With prompt specified, LILO will wait for user input without requiring the user to interrupt the boot sequence with a keypress. The timeout keyword is a failsafe, so that if the user doesn't respond within the specified number of tenths of a second, the boot process will continue anyway, allowing for unattended reboots.

This covers the general keywords specified. Now we can take a look at each of the defined images and see some of the interesting things you can do with LILO keywords on a per-image basis.

## LILO Per-Image Keywords

Our sample config file begins the per-image definitions with a definition for a Linux kernel image that uses the kernel file /boot/vmlinuz-2.2.5. Using the label and alias keywords, this kernel is given the names Red Hat and 1 in the map file. The root keyword specifies that the root filesystem for this kernel is /dev/hda5. When this kernel is booted, this filesystem will initially be mounted read-only and an initial ramdisk will be loaded from the image found in /boot/initrd.gz. Finally, the user will be prompted to enter a password if they attempt to pass anything on the kernel command line. This means that a password is required to boot into single user mode, and although this measure is not foolproof, it could deter some would-be crackers.

Next, an image is defined that uses an experimental kernel contained in /boot/vmlinuz-2.3.8, called Testing, with an alias of 2. The root filesystem is the same as the previous kernel, and like the previous kernel definition, an initial ramdisk is specified and the root filesystem is initially mounted read-only. Two differences between this kernel and the preceding one are that this image always requires a password, and if the system crashes while running, the system will reboot to the Red Hat kernel regardless of the previously defined lock keyword.

The image defined next is used to boot the system into Windows. It is easy to determine that we consider this a foreign operating system by the use of the other keyword. This keyword defines where LILO should look for this operating system. In this case, the foreign operating system resides on /dev/hda1, the first partition on the first IDE hard drive. The keywords defined for this image give it a name of Windows with an alias of 3. The user has only to type the number 3 to select this image and the partition table information needed by this operating system can be found on /dev/hda. As you can see, it is quite simple.

The next image is the most interesting one defined thus far because it appears that we have not correctly defined it. You may be wondering why we didn’t specify the kernel image file and other normal kernel options. To answer these questions, we have only to look at the definition of the problem that we specified. In it we stated that we wanted Fred’s Linux to be totally independent of the Red Hat installation. If we had specified the path to an image boot file as was done for the other two kernel images, we would have been sharing a partition where these images reside and thus violating the stated parameters of the problem. To overcome this, Fred’s Linux is treated like any other guest operating system. The only problem with that is that we are still without a boot sector for the partition containing Fred’s Linux. This problem is solved by creating a simple lilo.conf file for Fred’s Linux that installs lilo into the boot sector where it resides and allowing it to boot only Fred’s Linux. This simple lilo.conf file would look something like this:

```
#
# General section
#
boot = /dev/hda2
install = /boot/boot.b
delay = 50
verbose = 2

#
# Boot my Linux 2.2.5 kernel
#
image = /boot/vmlinuz-2.3.8
label = linux
root = /dev/hda2
read-only
initrd = /boot/initrd.gz
```

As you can see, there are no prompt and timeout options specified, which results in Fred's Linux booting immediately unless interrupted by a user keystroke. The primary reason for including the delay is to allow for the passing of command-line options, such as single to boot into single user mode.

The final image defined is the same as the one that is used to boot Windows, except that it boots FreeBSD. The boot sequence given the preceding configuration is illustrated in Figure 5.6.

## FIGURE 5.6
Multiple OS with LILO as MBR.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_160_0.png)

As you can plainly see, you can customize LILO in many different ways to suit your needs. The combinations are not quite endless, but with the available options, you can come up with some very complex arrangements.

## Alternatives to LILO

Although LILO is the most popular boot loader for Linux, it is definitely not the only one available. There are many boot loaders, both commercial and non-commercial, that are capable of loading Linux. This section lists a few of these and where you can obtain them.

If you don't like the idea of altering the boot sectors on your system drives, one of the options for booting Linux is LOADLIN, which is a DOS program that is capable of loading and executing the Linux kernel. Recent additions to this software include support for bZImages and initial RAM disks. The software, which contains documentation, is available by FTP from the Linux archives at ftp://metalabs.unc.edu/pub/linux/system/boot/dualboot/.

Another boot loader that can be used to replace the master boot record and that presents a menu of available operating systems is the bootactv program. This program is included with the pfdisk package and is available by FTP from ftp://ftp.funet.fi/pub/Linux/tools/. This package works, but appears not to have been updated since 1992.

SYSLINUX is a boot loader for Linux that allows you to boot from DOS floppies and is used by some distributions as their installation floppies. This program is primarily used to create boot floppies and is not intended to be a general-purpose boot loader. SYSLINUX is available by FTP from ftp://metalabs.unc.edu/pub/linux/system/boot/loaders/.

Two other boot loaders available in the same place as SYSLINUX are GRUB and CHOS. Both of these are general-purpose boot loaders that present users with interactive menus allowing them to boot the operating system of their choice in a manner similar to the OS/2 boot manager.

System Commander* Deluxe is a commercial offering from V Communications that is capable of booting Linux. Much more than a boot loader, System Commander manages the entire installation process for new operating systems. It protects existing operating systems from the new ones being installed, resizes partitions to make room for new operating systems, and so on. The company Web site at http://www.v-com.com has complete information on features and pricing.

This is not an exhaustive list by any stretch of the imagination. If you are not happy with LILO, a simple Net search may yield a program more suitable to your needs.

## The Linux Boot Process and System Initialization Scripts

Once the boot loader has loaded a Linux kernel, what next? This section discusses the process of loading the kernel, including device initialization, and the handoff to the init process, which starts the many processes required to actually make your Linux system useful.

### Kernel Startup and Device Initialization

Starting the Linux kernel is much like starting any other operating system in that it all starts with the boot sector code. As discussed earlier, the boot sector code is responsible for loading the operating system kernel into memory and executing it. For Linux, this results in the following sequence of events:
