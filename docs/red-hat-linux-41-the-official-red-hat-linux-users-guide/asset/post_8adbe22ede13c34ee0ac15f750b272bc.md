
cept for the nfsroot and the kernel link. Instead of using `/images/vmlinux.` use `tftpboot.img`. Put it in `/home/tftp` and make the symlink:

```bash
cd /home/tftp 
ln -s tftpboot.img C7B718EB_SUN4M
```

Please remember to change the IP address and architecture based on your own network numbers and machine architecture.

Now all you need to do is a **boot net** from the SPARC, and it should TFTP everything over, boot a kernel, and start the install program. You can then do an FTP install from a server near you, or you can do an NFS, hard drive, or CD-ROM install if you choose.

## 4.5 Installation Using a Serial Terminal

You can also install Red Hat Linux/SPARC 4.1 using a serial terminal: any terminal which emulates a VT100 ought to work fine. Boot from the floppy, and at the SILO prompt enter:

```bash
linux serial
```

The installation program runs on the first serial port at 9600,8,N,1 (9600 baud, 8 bits, no parity, 1 stop bit). The installation program can run in color, if your serial terminal supports color.

At any prompt dialog during a serial installation (any dialog with an OK button), you can press Ctrl + Z to start a subshell; to return to the installation program, enter exit at the shell prompt.

**Important!** After installing using a serial terminal, the only way to log into your Red Hat Linux system is via the network; however, the `/etc/security` file keeps the root user from logging in from the network. When the serial install is completed, but before you reboot your machine, press Ctrl + Z to start a subshell and enter the following command:

```bash
rm /mnt/etc/security
```

If you fail perform this step, you will not be able to log into your machine.

## 4.6 Installation: Selecting System Components

(For an explanation of system components, please see Chapter 2, Section 2.4.11.)

**Important!** When selecting system components to install for Red Hat Linux/SPARC, choosing to install **Everything** without choosing **Select individual packages** could result in an unbootable Red Hat Linux system.

The last kernel to be installed will be a multi-processor kernel, which will fail to work on uniproc machines. Additionally, the default X server will end up as **XsunMono**, which may not work for most people. If you do wish to install **Everything**, choose **Select individual packages** as well. Then, deselect all the kernels except for one you wish to install (**kernel-sparc** works for most) and all X servers except the one for your hardware (XsunMono for lwtwo video cards, **Xsun** for all 8-bit displays, and **Xsun24** for the supported 24-bit displays).

## 4.7 SILO Configuration

SILO configuration is nearly identical to LILO configuration, see section 2.4.18 for details.

## 4.8 Partitioning

There is one additional step in partitioning a hard drive for a SPARC. You must create the third partition of every disk as type **Whole Disk** spanning from cylinder 0 to the end of the disk. It shouldn't be touched, but should exist. You can still create other partitions just as you normally would.

## 4.9 X Windows

There is no mouse or X windows config on the SPARC. The 8 bit server is installed by default. If you want to use the 24 bit server (for TCX cards), you need to install the **Xsun24** package. If you only have a bwtwo frame-buffer and want to increase performance, install the **XsunMono** package.

Installing both of the above requires you to restart X windows. Also, you can uninstall the Xsun package if you use one of the above servers.

# Chapter 5

## Post Installation Configuration

After installation your system is fully functional, but you may still want to do some additional configuration. This chapter describes some of the various system configuration tasks you may need to do.

## 5.1 Building a Custom Kernel

With the introduction of modularization in the Linux 2.0.x kernel there have been some significant changes in building customized kernels. In the past you were required to compile support into your kernel if you wanted to access a particular hardware or filesystem component. For some hardware configurations the size of the kernel could quickly reach a critical level. To require ready support for items that were only occasionally used was an inefficient use of system resources. With the capabilities of the 2.0.x kernel, if there are certain hardware components or filesystems that are used infrequently, driver modules for them can be loaded on demand. For information on handling kernel modules see Chapter 8, Section 8.6.

### 5.1.1 Building a modularized kernel

Only Red Hat Linux/Intel and Red Hat Linux/SPARC support modular kernels; Red Hat Linux/Alpha users must build a monolithic kernel (see Section 5.1.3 below).

These instructions provide you with the knowledge required to take advantage of the power and flexibility available through kernel modularization. If you do not wish to take advantage of modularization, please see Section 5.1.3 for an explanation of the different aspects of building and installing a monolithic kernel. It is assumed that the **kernel-source** package has been previously installed and all commands are issued in the directory *usr/src/linux*.

It is important to begin a kernel build with the source tree in a known condition. Therefore, it is recommended that you begin with the command **make mrproper**. This will remove any configuration files along with the remains of any previous builds that may be scattered around the source tree. Now you must create a configuration file that will determine which components to include in your new kernel. Depending upon your hardware and personal preferences there are three methods available to configure the kernel.

- **make config** An interactive text program. Components are presented and you answer with **Y** (yes), **N** (no), or **M** (module).
- **make menuconfig** A graphic, menu driven program. Components are presented in a menu of categories, you select the desired components in the same manner used in the Red Hat Linux installation program. Toggle the tag corresponding to the item you want included; **Y** (yes), **N** (no), or **M** (module).
- **make xconfig** An X Windows program. Components are listed in different levels of menus, components are selected using a mouse. Again, select **Y** (yes), **N** (no), or **M** (module).

In order to use **kernel** (see Section 8.6 for details) and kernel modules you must answer **Yes** to **kernel support** and **module version (CONFIG_MODVERSIONS)** support in the configuration. If you want to build a kernel with a configuration file (*usr/src/linux/.config*) that you have already created with one of the above methods, you can omit the make mrproper and make config commands and use the command make dep followed by make clean to prepare the source tree for the build.

The next step consists of the actual compilation of the source code components into a working program that your machine can use to boot. The method described here is the easiest to recover from in the event of a mishap. If you are interested in other possibilities details can be found in the Kernel-HOWTO or in the Makefile in /usr/src/linux on your Linux system.

- Build the kernel with make boot.
- Build any modules you configured with make modules.
- Move the old set of modules out of the way with:

```bash
rm -rf /lib/modules/2.0.27-old
mv /lib/modules/2.0.27 /lib/modules/2.0.27-old
```

Of course, if you have upgraded your kernel, replace 2.0.27 with the version you are using.

- Install the new modules (even if you didn't build any) with make modules_install.

If you have a SCSI adapter and made your SCSI driver modular, build a new initrd image (see Section 5.1.2). Note that there are few practical reasons to make the SCSI driver modular in a custom kernel.

In order to provide a redundant boot source to protect from a possible error in a new kernel you should keep the original kernel available. Adding a kernel to the LILO menu is as simple as renaming the original kernel in /boot, copying the new kernel to /boot, adding a few lines in /etc/lilo.conf and running /sbin/lilo. Here is an example of the default /etc/lilo.conf file shipped with Red Hat Linux:

```bash
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=100
image=/boot/vmlinuz
```
