
Once it is mounted, you can access files on the CD-ROM as you would in any directory.

Tip You use mkisofs to create a CD-ROM image made up from your files or another CD-ROM.

## Mounting Hard Drive Partitions: Linux and Windows

You can mount either Linux or Windows hard drive partitions with the mount command. However, it is much more practical to have them mounted automatically using the /etc/fstab file as described previously. The Linux hard disk partitions you created during installation are already automatically mounted for you. As noted previously, to mount a Linux hard disk partition, enter the mount command with the device name of the partition and the directory to which you want to mount it. IDE hard drives use the prefix hd, and SCSI hard drives use the prefix sd. The next example mounts the Linux hard disk partition on /dev/hda4 to the directory /mnt/mydata:

```
# mount -t ext3 /dev/hda4 /mnt/mydata
```

You can also mount a Windows partition and directly access the files on it. As with a Linux partition, you use the mount command, but you also have to specify the file system type as Windows. For that, use the -t option, and then type vfat for Windows 95/98/ME (vfat for MS-DOS). For Windows XP, 2000, and NT, you would use ntfs (limited read-only access; write access is experimental and not recommended). In the next example, the user mounts the Windows hard disk partition /dev/hda1 to the Linux file structure at directory /mnt/windows. The /mnt/windows directory is a common designation for Windows file systems, though you can mount it in any directory (such as /mnt/dos for MS-DOS). If you have several Windows partitions, you could create a Windows directory and then a subdirectory for each drive using the drive's label or letter, such as /mnt/windows/a or /mnt/windows/mystuff. Be sure you have already created the directory before mounting the file system.

```
# mount -t vfat /dev/hda1 /mnt/windows
```

## Installing IDE CD-R/RW and DVD R/RW Devices

Linux CD-burning applications all treat CD-R/RW and DVDR/RW drives as if they were SCSI drives. This means that IDE CD-R/RW drives have to emulate SCSI drives for them to be recognized and used by CD or DVD writing software. Even if you want to use an IDE CD-ROM or DVD-ROM in a CD writing applications—say, as just the reader to copy a CD disc—that IDE CD-ROM drive would still have to emulate a SCSI CD-ROM drive. Only SCSI drives (CD-R/RW/ROM or DVDR/RW/ROM) are recognized by Linux CD or DVD writing software. For example, if you have a regular IDE CD-ROM and you want to use it with Linux CD-write software to copy CDs (ripping), you still have to have that IDE CD-ROM emulate a SCSI CD-ROM. Check the CD-Writing HOW-TO at www.tldp.org for more details. A brief description is provided here.

Tip SCSI emulation for IDE devices is implemented in the kernel as SCSI Emulation Support in the IDE, ATA, and ATAPI Block Devices entry, located in the ATA/IDE/MFM/RLL Support window opened from the main kernel configuration menu. Normally, it is compiled as a module.

IDE CD and DVD drives (CD-R/RW/ROM or DVDR/RW/ROM) are recognized as IDE devices during installation and installed as such. However, when you start up your system, you need to instruct the Linux kernel to have the IDE CD and DVD drives emulate SCSI CD or DVD drives. This means that a CD-R drive that would be normally recognized as a /dev/hdc drive has to be recognized as a /dev/scd0 device, the first SCSI CD-ROM drive. You do this by loading the ide-scsi module, which allows an IDE CD drive to emulate a SCSI CD drive.

## SCSI Emulation

You can implement SCSI emulation for IDE CD and DVD drives in one of two ways: by either loading the ide-scsi module as a kernel parameter or specifying the module in the /etc/modules.conf file (/etc/modprobe.conf in 2.5 and 2.6 kernels). You will also have to indicate the IDE drives to emulate. If the ide-scsi module is compiled into the kernel (not as a separate module), you have to load it as a kernel parameter. An ide-scsi module can be loaded either way.

### Tip

During installation, Red Hat will recognize the IDE CD and DVD drives you have installed on your system, and it will include the ide-scsi kernel parameter automatically as part of either your LILO or GRUB boot loader configurations. You do not need to perform any of the specific configuration tasks described in this section.

## Kernel Parameters at Boot Time

As a kernel parameter, you can either manually enter the ide-scsi parameter at the boot prompt or place it in the /etc/grub.conf or /etc/lilo.conf file (depending on whether you are using the GRUB or LILO boot loader) to have it automatically entered. The parameter is read when the system starts up. List each IDE CD or DVD drive that needs to emulate a SCSI drive as using the ide-scsi module. You assign the ide-scsi module to the device name of the IDE CD drive to be emulated. The following example loads the ide-scsi module to have the master IDE drive on the secondary IDE connection (hdc) emulate a SCSI drive:

```
hdc=ide-scsi
```

## Grub and CD Writers

If you installed Red Hat with your IDE CD-R/RW drive already attached, GRUB would have automatically detected it and listed the ide-scsi module for that drive in its boot parameters. You can always manually enter the parameter by typing a at the GRUB boot entry for your Linux system, displayed when you start up your computer. The parameters for your Linux system will be listed. Just add the CD-R/RW ide-scsi module assignment. The following example shows how two IDE CD drives are specified at the Linux boot prompt:

```
grub append> ro root=/dev/hda3 hdc=ide-scsi
```

For the /etc/grub.conf file, add these parameters to the Linux kernel line, just as you would to a boot entry:

```
kernel /boot/vmlinuz-2.4.18-3 ro root=/dev/hda3 hdc=ide-scsi
```
