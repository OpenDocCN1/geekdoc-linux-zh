# 3.4 BOOTING TO SINGLE-USER MODE

The beginnings of the boot process are system dependent. Systems with non-Intel processors have custom boot loader software, while PCs are mostly standardized thanks to GRUB.

# Single-user mode with GRUB

You don't need to use the command line to boot single-user mode under GRUB. The GRUB authors realized that boot options should be easily modifiable and decided on the 'a' key as the appropriate tool. At the GRUB splash screen, highlight the desired kernel and press 'a' to append to the boot options. To boot single-user mode, add the single (or -s on Solaris) flag to the end of the existing kernel options. For an example a typical configuration might be

```
grub append= root=LABEL=/rhgb quiet single
```

# Single-user mode on SPARC

To interrupt the boot procedure and enter the OpenBoot PROM on Sun hardware, press the L1 and 'a' keys simultaneously. L1 is sometimes labeled STOP on modern Solaris keyboards. From the boot PROM, you can type -s to enter single-user mode.

![](bbox=[0.165, 0.413, 0.238, 0.443])

To boot an alternative kernel under Solaris, you usually have to type the full Solaris name of the device and the file. The string of characters you see when you do an ls -1 on the /dev file is:

```
% ls -1 /dev/rdsk/c0td0s0
lrwxrwx1 root 55 Jan 15 1998 /dev/rdsk/c0td0s0 -> ..//sbus/1F,0/SUNW,fas@0,880000/sd@0:a,raw
```

To boot the kernel as /kernel/backup on this disk, you'd need to enter the following command at the boot PROM:

```
boot /devices/sbus/1F,0/SUNW,fas@0,0,880000/sd@0:a,raw/kernel/backup
```

Table 3.4 lists some of the most useful commands you can enter from Sun boot PROM and a brief description of their functions.

| Command | Function |
| --- | -- |
| boot /path_to_kernel | Boots an alternative kernel |
| boot -s | Boots into single-user mode |
| boot -r | Reconfigures the kernel and probes for new devices |
| boot -a /etc/system.bak | Makes kernel read /etc/system.bak instead of /etc/system |
| probe-scsi | Shows a list of all attached SCSI devices |