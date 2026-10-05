
# Global section

The first part of /etc/lilo.conf begins with the instruction boot= specifies where LILO is to be installed. For installation on a diskette, the specification is /dev/fd0. To install LILO into the MBR of the first IDE hard disk, use /dev/hda for the first SCSI disk, /dev/sda.

delay specifies how tens of seconds LILO waits for input. The shortest delay is 0, but you must keep Shift depressed before you start LILO if you do not want to use the default operating system.

prompt has the opposite effect and forces a user input before the boot process is started. In this case, arrow causes the default operating system to be booted. All operating systems can be selected as described above, prompt prevents unintended reboot.

compact allows a particularly fast loading of the kernel (all above, from the diskette), but it does not work on all computers or with hard disk controllers.
The map allows you to specify the file in which the sector numbers of the kernel files and other files are stored. /boot/map is used, which is usually a sensible default setting.

A further option which is often omitted is install specifies the file in which the LILO main program (the second stage loader) is. The default setting is /boot/map and needs to be changed only in rare cases.
The linear option causes the sector addresses in /boot/map not to be stored as CHS tuples (cylinder, head, sector), but as LBA values (Logical Block Addressing). See page 33. When LILO and the BIOS agree on a common interpretation of the hard disk geometry, using linear is the easiest solution.

According to the SuSE database, the linear option reduces the maximum address range depending on the CHS geometry signaled by the BIOS. The reason for this is 16-bit arithmetic used in the calculation of sector numbers. Under unfavorable circumstances - in particular with a CHS geometry of more than 64 sectors per track - as commonly used by current LILO versions - linear allows only a smaller area of the disk to be addressed and it would be possible without this option (which, depending on the BIOS, up to 7.9 Gigabytes).

```
# /etc/lilo.conf (part 1)
# LILO global section
boot=/dev/fd0          # installation in the MBR of a diskette
delay=100             # wait 10 seconds
#prompt                # force input (no automatic start)
#compact               # faster, especially with disks; can cause problems with some hard disks
map=/boot/map          # default setting in any case
install=/boot/boot.b   # default setting in any case
#linear                 # required for some hard disks
```

In some cases (big disks, old BIOS, and so on), LILO has problems with the hard disk geometry. As a first solution, you should try the linear option.

# BOOT DISKETTES/ULO 187

not work. you must use the disk option with its suboption: bios, sectors, heads, and cylinders. Background information on this subject can be found on page 33 and in the LILO documentation.

```
disk=/dev/hdda # additional for for device devhdda
bios=0x80 # 80 for the first disk, 081 for the second, ...nsectors=63 # number of sectors
heads=255 # number of heads
cylinder=522 # number of cylinders
```

# Linux Image

Now to the second part of lilo.conf: here you can specify up to 16 operating system versions that you can choose to run. The first system is used as the default setting. A common feature of all entries is the label command which gives each version name. These names must be entered during the manual selection of the operating system – thus, it is better to choose short and meaningful names without spaces or special characters.

![](img/b30873dd3d753687a59253fb9ad26a0b_214_0.png)

Unless you have a special keyboard table in LILO configuration (keyword keytable, LILO documentation), the US keyboard layout applies for entering label names. Some characters may be located in different positions.

To boot Linux, the image and root commands must be specified in addition label image determines the kernel file, root the partition on which the root directory is located.

vga specifies the VGA mode: extended stands for the extended mode with 50 lines, normal for the standard mode, as for confirmation for booting, and an arbitrary number n > 0 for the VGA mode n. (Warning!) If this VGA mode does not exist or is not supported, you can use Linux correctly.) If you want to use a RAM disk, you can specify its size in Kbytes with ramdisk=.

read-only specifies that the root partition is first mounted read-only. Then, the Init process can, if needed, repair the file system, before it is mounted (and finally) in read-write mode. This option should always be used

With append, additional kernel options can be specified (for example, to circumvent hardware problems). If you use a kernel adjusted to your hardware or a modularized kernel, kernel options are seldom required. The most important options are described on page 48.

```
# /etc/lilo.conf (part 2)
image = /boot/mlinux = kernel file
label = linux
root = /dev/sda8 = root device
read-only
initrd=/boot/initrd = in RedHat with SCSI
vga = extended = text mode 80x50 characters
# alternative: linuxbak for booting an older kernel version
image=/boot/mlinux = kernel file
label = linux
root = /dev/sda8 = root device
read-only
initrd=/boot/initrd = in RedHat with SCSI
vga = extended = text mode 80x50 characters
# alternative: linuxbak for booting an older kernel version
image=/boot/mlinux = kernel file
label = linux
root = /dev/sda8 = root device
```

# CONFIGURATION AND ADMINISTRATION

```
root = /dev/sda8 = root device
read-only
initrd=/boot/initrd = in RedHat with SCSI
vga = extended = text mode 80x50 characters
# alternative: linuxbak for booting an older kernel version
image=/boot/mlinux = kernel file
label = linux
root = /dev/sda8 = root device
```

# Linux on disk

```
root = /dev/sda8 = root device
read-only
initrd=/boot/initrd = in RedHat with SCSI
vga = extended = text mode 80x50 characters
# alternative: linuxbak for booting an older kernel version
image=/boot/mlinux = kernel file
label = linux
root = /dev/sda8 = root device
```

# Windows 9

```
root = /dev/sda8 = root device
read-only
initrd=/boot/initrd = in RedHat with SCSI
vga = extended = text mode 80x50 characters
# alternative: linuxbak for booting an older kernel version
image=/boot/mlinux = kernel file
label = linux
root = /dev/sda8 = root device
```

# Windows 31

```
root = /dev/sda8 = root device
read-only
initrd=/boot/initrd = in RedHat with SCSI
vga = extended = text mode 80x50 characters
# alternative: linuxbak for booting an older kernel version
image=/boot/mlinux = kernel file
label = linux
root = /dev/sda8 = root device
```

# OS/2

```
root = /dev/sda8 = root device
read-only
initrd=/boot/initrd = in RedHat with SCSI
vga = extended = text mode 80x50 characters
# alternative: linuxbak for booting an older kernel version
image=/boot/mlinux = kernel file
label = linux
root = /dev/sda8 = root device
```

# Setting up LILO

To set up LILO, you need a lilo.conf file of the following kind. /boot/mlinuz must point to a kernel that contains all drivers needed to access the root partition. Path and device names need to be adjusted to suit your computer. You may need additional options which have been described in the configuration section (such as initrd RedHat with SCSI systems). Once the configuration is set up, you insert a formatted diskette into the drive and execute lilo.

```
# /etc/lilo.conf
=/dev/fd0 # device of the diskette drive
prompt timeout=100
image=/boot/mlinuz # kernel file
abel=linux root=/dev/hda8 # root device
read-only
initrd=/boot/initrd # RedHat with SCSI
other=/dev/hda1
```
