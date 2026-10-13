
Check out the Web site for Stampede GNU/Linux at www.stampede.org, a nonprofit organization that is, as of this writing, still developing its distribution. Its focus is on ease of use and optimization for the newest processor hardware. You can download its version of Linux from this site.

Visit www.suse.com, the Web site for S.u.S.E. GmbH, the best-selling Linux distribution in Europe. The S.u.S.E. Web site offers HCLs and a knowledge base as well as downloads of its latest version of Linux.

Explore the Web site for Turbo Linux at www.turbolinux.com, the best selling Linux distribution in Asia. The Turbo Linux Web site allows you to install its distribution by downloading its files to a hard drive or through the use of boot disks to start a Linux connection to its FTP server.

## Startup and Shutdown

Terms you'll need to understand:

- Linux Loader (LILO)
- vmlinuz
- boot.b
- map
- append
- /etc/fstab
- rc.d
- init.d
- /etc/inittab
- Shells
- shutdown

Techniques you'll need to master:

- Managing the Linux Loader (LILO)
- Editing mounted file systems (/etc/fstab)
- Analyzing initialization scripts
- Analyzing run level resource control scripts
- Explaining initialization commands (/etc/inittab)
- Understanding logins
- Editing shutdown options

This chapter explains what happens when Linux starts, and what you can do to customize your start process. The Linux Loader (LILO) manages multiple operating systems. LILO launches when you start your computer. If you choose Linux from the LILO menu, it loads the Linux kernel. The kernel loads your hardware and protocols, and then passes the rest of the process to init. The init program mounts your drives as specified in the /etc/fstab file and starts other programs at various run levels with the help of resource control (rc) files. Then it sets up shells and login screens as defined by the /etc/inittab initialization file. This file also defines who can shut down your computer and the commands that can be used to shut it down.

### Linux Loading Details

LILO is a versatile tool. You can set it up to load Linux directly from your hard drive, and it can also work with other boot managers. You can even set it up to load from a floppy disk. LILO tells Linux special details about your hardware configuration as you boot. Once you choose to load Linux, it starts your Linux kernel.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_127_0.png)

> The Linux kernel is sometimes known by its basic file name, vmlinuz.

When LILO loads on your computer, you see the following prompt, usually for just a few seconds:

```
LILO boot:
```

If you press the Shift key, LILO should stop and wait for your input. If you press the Tab key, LILO lists the available operating systems. For example, if you've set up Linux and Microsoft Windows on your computer, you might see the following:

```
linux   dos
boot:
```

In this case, you have two choices. You can type "linux" or "dos". Even if your other operating system is Microsoft Windows, typing "windows" won't work.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_127_1.png)

> There is no limit to the number of operating systems that you can select through LILO. The only limits are based on the size of your hard drive.

### Common LILO Tasks

Whatever your configuration, you'll see at least the following commands in your lilo.conf file:

```
boot=/dev/hda
install=/boot/boot.b
```

The boot command specifies the location of your lilo.conf file. The command shown assumes that you installed LILO in the Master Boot Record (MBR) of the first hard disk on your computer. If you installed LILO on the first partition of that drive, you'd see the boot=/dev/hda1 command. Alternatively, if you installed LILO on a floppy disk, you'd see the boot=/dev/fd0 command.

LILO then runs the secondary boot loader, the boot.b file. If you have LILO on a floppy disk, this command would read install=/mnt/boot.b, because floppy disks are typically mounted on the /mnt directory before Linux loads.

Some Linux distributions configure the following commands in LILO too:

```
message=/boot/messagefile
map=/boot/map
```

When used, the message command specifies a message file that you'd see before the LILO boot: prompt. The map command specifies the location of your boot partitions. By default, the map command is located in the /boot/map file.

The following commands govern how long you wait before your default operating system automatically boots:

```
prompt
timeout=100
```

The prompt command supersedes any timeout if you press the Shift or Tab key. The timeout command specifies how long LILO waits, in tenths of a second, before booting your default operating system. The time shown is equal to 10 seconds. Some versions of Linux substitute the delay command for timeout; they are, for our purposes here, identical commands.

### Multiple Operating Systems

If you do not make a selection at the LILO boot: prompt, the operating system that appears depends on the default command. On the other hand, if this command is missing, the default operating system is the first one you see in the lilo.conf file.

LILO typically defines a Linux operating system with four commands as in the following:

```
image=/boot/vmlinuz
label=redhat
root=/dev/hda3
read-only
```

The image command specifies the location of your Linux kernel. The label is what you see when you press the Tab key at the LILO boot: prompt, as well as what you need to type to select that operating system. The root is the location of the root directory (/). And read-only means that the root directory should be mounted in read-only mode. The read-only command is usually superseded when the root directory is mounted on its assigned volume. Of course, if any of the preceding files have different names or are in different locations on your system, substitute accordingly.

LILO typically defines other operating systems, such as Microsoft Windows or IBM's OS/2, with three commands as in the following:

```
other=/dev/hda2
label=dos
table=/dev/hda
```

The other command specifies the volume with the boot files for the non-Linux operating system. The label command is the same as in the Linux section. The table command specifies the drive with partition information.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_129_0.png)

There are two IDE hard disk controllers on a standard personal computer. You can connect each controller to a "master" and a "slave." The master on the first controller is known as hda; the slave on the first controller is known as hdb. The master on the second controller is known as hdc; the slave on the second controller is known as hdd. If you have one hard disk and a CD-ROM drive, the hard disk is most commonly located on hda, whereas the CD-ROM drive is most commonly located on hdb.

### Custom LILO Commands

You can customize LILO with the append command, which passes messages to your Linux kernel. If you just installed your first Ethernet network card and you know that its IRQ (interrupt request) is set to 12 and its I/O (input/output) address is set to 0x300, you can add the following command to your lilo.conf file:

```
append="ether=12,0x300,eth0"
```

The format for an Ethernet card is ether=IRQ, I/O, device. Because this is your first Ethernet card, the device is eth0. Your second Ethernet card would be eth1.

Alternately, if you have an older Linux kernel, prior to version 2.2.1, you can use the mem command to help Linux recognize your RAM above 64MB. For example, the following command tells Linux to recognize your RAM up to 192MB:

```
append="mem=192M"
```

Linux kernels starting with version 2.2.1 should recognize all of the RAM on your computer.

If you edit LILO in any way, use a text editor. Make sure you have a rescue disk ready with your old LILO, and then run the /sbin/lilo command to load your new lilo.conf file.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_130_0.png)

You can enter append commands directly at the LILO boot: prompt, but without typing "append". For example, if you wanted to boot Linux and help it recognize your RAM up to 192MB, you would use the linux mem=192M command.

### Troubleshooting LILO

The LILO prompt can help you troubleshoot boot problems. For example, you know you have a problem when you only see part of the LILO boot: prompt, as shown here:

```
L:
```

When you see only this part of the prompt, there are two possible causes. You may have moved or deleted the secondary boot loader file, normally /boot/boot.b. Alternately, your BIOS (Basic Input/Output System) may have trouble reading your hard disk. These are also potential causes if all you see is L., LIL?, or LIL-.

Alternately, if you don't see any letters when you expect to see the LILO boot: prompt, it means that your computer is having trouble finding your lilo.conf file. It may even be missing from your MBR.

If your secondary boot loader (boot.b) file is still present, check the configuration of your hard disk against the specifications listed in your BIOS menu. You may also have the problem described in Chapter 4, where the Linux /boot directory is mounted on a volume that ends above cylinder 1023.
