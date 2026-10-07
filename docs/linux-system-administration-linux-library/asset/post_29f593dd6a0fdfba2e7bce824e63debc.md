
# Disaster Recovery Techniques

## Install Disk

There are two flavors of boot disks these days. The first is used to boot into the installation and is typically referred to as an install disk. These days, most CD-ROM distributions provide a bootable CD-ROM, removing the need for a boot disk. Still, if your computer does not allow booting from a CD-ROM or if your CD-ROM is not functioning, you will need to create a boot disk by copying the correct boot image to floppy. If your distribution does not come with a ready-made boot disk, you must create one using one of the boot images, since boot.img is the most commonly used boot image. There is also bootnet.img for installing from a non-PCMCIA device. pcmia.img image is available for installation via PCMCIA device like Ethernet adapters or hard drives.

Since the install disks allow you to boot your system and use a virtual terminal, they can be used to repair flaws, but some of the same restrictions apply as single-user mode. The boot disk contains only kernel image, so all initialization is performed using the system's own files. There are several ways to create an install floppy. If you have a working system, you may create the disk by using WRITE.EXE. This binary is located in /sbin/. To execute it, create the command and tell it which of the images you wish to write to and which device to write to.

If you are lucky enough to have Linux or other machine available, you can create the disk with a variation of the following command:

```bash
dd if=/mnt/cdrom/images/boot.img of=/fd0
```

On some systems, you'll need to specify block size. See the man page for the dd command and also use the cat command as follows:

```bash
cat /mnt/cdrom/images/boot.img >/fd0
```

You must not use the cp command, because the idea is to transfer the raw image without formatting, and the cat command requires a formatted disk.

![](img/4fb67eb64.png)

## Emergency Boot Floppy

The second type of boot floppy is a standalone boot image created specifically for your system after an install or by running /mkboot. This disk is typically referred to as an emergency boot floppy. It contains a root filesystem along with customized boot data provided by the distribution. The standalone boot floppy can be used to boot your system if you cannot or wish to run LILO or some other boot manager. It is important to remember that the boot floppy uses files on the existing system when it boots. It needs to find the second-stage boot loader, which is typically /boot/boot.b, and kernel image on the computer. If the problem you are trying to fix is one of these files, you'll need to use Red Hat's rescue mode.

## Rescue Mode

A Linux distribution's rescue mode boots a small but complete Linux system independent of the installed Linux system. From this mode, you can mount the computer's devices, edit configuration files, run a number of repair functions depending upon the problem. Since single-user mode and boot disks depend upon files from the installed system itself and certain types of problems cannot be fixed rescue mode is the only way to fix some problems you'll encounter. This section focuses upon Red Hat's rescue mode, but the principles are the same for other distributions.

If LILO has been overwritten by another operating system, you cannot boot from the kernel and initialization scripts on your hard drive, because there is no way to access them; so you need to use rescue mode. If hardware problems make it impossible to boot using your initialization scripts, use rescue mode and mount the drive to retrieve whatever you can before it dies. If you have made a mistake in /etc/fstab and incorrectly given the mount point for /partition, you can use rescue mode to edit the file and reboot. You can use rescue mode to recover a complete tape backup to a new hard disk after one has died.

To boot into rescue mode, you need to boot from a Red Hat boot disk or by booting a floppy containing either the PCMCIA boot image or the bootnet. When you reach the boot prompt, simply type linux rescue. When the system boots, you will be in rescue mode and will have a Bash prompt. You will be able to run any of the following commands:

| | | | |
| :--- | :--- | :--- | :--- |
| anaconda | gzip | mkfs.ext2 | ps |
| badblocks | head | mknod | python |
| bash | hwclock | mkraid | python15 |
| cat | ifconfig | mkswap | raidstart |
| chatter | init | mlabel | raidstop |
| chmod | insmod | mmd | rcp |
| chroot | less | mmount | rlogin |
| clock | loader | move | rm |
| collage | ls | modprobe | rmod |
| cp | lsattr | mount | route |
| cpio | lsmod | mpartition | rpm |
| dd | mattrib | mrd | rsh |
| ddcprobe | mattblocks | mread | sed |
| depmode | mbadblocks | mren | sh |
| df | mcd | mshowfat | sync |
| e2fsck | mcopy | mt | tac |
| fdisk | mdel | mtools | tail |
| fsk | mdtree | mtype | tar |
| fsck.ext2 | mdir | mv | touch |
| ftp | mdu | mzip | traceroute |
| genhdlist | mformat | open | umount |
| gnome-pty-helper | minfo | pico | uncpio |
| grep | mkdir | ping | uniq |
| gunzip | mk2fs | probe | zcat |
