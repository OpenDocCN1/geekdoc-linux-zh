```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
message=/boot/message
linear
```

```
image=/boot/vmlinuz-2.6.13-1.1526_FC4-1386
label=linux
initrd=/boot/initrd-2.6.13-1.1526_FC4-1386.img
read-only
root=/dev/hda6
append=root=/hda/
```

```
other=/dev/hda1
optional
label=dos
```

With prompt on, the boot partition appears when the system is booted requiring that any keys are pressed. The timeout value, in this case 50 tenths of a second (5), defines how long to wait for keyboard input before booting the default boot image. The boot line indicates the location of the partition is on the hard disk represented by `/dev/hda` (the first IDE disk).

The map line indicates the location of the map file (/boot/map, default). The map file contains names and locations of kernel images. The install message line tells LILO to display the contents of the /boot/message file when booting (which contains the graphical Fedora boot screen that appears). The linear line causes sector addresses to be generated (instead of sector/head/cylinder addresses).

In the sample file, there are two bootable partitions. The first (image=/boot/vmlinuz-2.6.13-1.1526_FC4-1386) shows an image labeled linux. The root file system (/) for that is partition on /dev/hda6. Read-only indicates that the system is first mounted read-only, although the initrd indicates the location of the initial RAM disk image used to start the system.

The second bootable partition, which is indicated by the word other in this example, is on the /dev/hda partition. Because it is a Windows XP system, it is labeled a DOS file system. The table line indicates the device that contains the partition.

Other bootable images are listed in this file, and you can add another boot image yourself (like one you create from reconfiguring your kernel as discussed in the next section) by installing the new image and changing lilo.conf.