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

![](bbox=[0.12, 0.7, 0.22, 0.85])

There are two IDE hard disk controllers on a standard personal computer. You can connect each controller to a "master" and a "slave." The master on the first controller is known as hda; the slave on the first controller is known as hdb. The master on the second controller is known as hdc; the slave on the second controller is known as hdd. If you have one hard disk and a CD-ROM drive, the hard disk is most commonly located on hda, whereas the CD-ROM drive is most commonly located on hdb.

# Custom LILO Commands

You can customize LILO with the append command, which passes messages to your Linux kernel. If you just installed your first Ethernet network card and you know that its IRQ (interrupt request) is set to 12 and its I/O (input/output) address is set to 0x300, you can add the following command to your lilo.conf file:

```
append="ether=12,0x300,eth0"
```