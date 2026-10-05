
# 194 CONFIGURATION AND ADMINISTRATION

Now you can execute LILO, with the DOS partition still being mounted.
A restart, LILO loads the kernel file from the DOS partition and then starts Linux.

The problem with this kind of LILO installation is that LILO must be able to rely on the fact that the location of the kernel file is not changed. LILO does not store the file name, but the sector number at which the file starts. If you defragment the DOS partition or move, copy, or do other things to the LILO directory, the location of the file on disk (thus, the file starts) can change. LILO will no longer find the kernel file, and the boot process will fail.
Remedy: you must start Linux with a boot disk, mount the DOS partition and execute LILO once again. This will reinstall LILO.

If you install a new kernel, you must mount the DOS partition again, copy the new kernel file into it and re-execute LILO. In contrast to a ‘normal’ LILO configuration, the file /boot/vmlinuz does not play any role at all – only the file counts as /desc/lilo/vmlinuz.

# Starting LILO with the Windows boot manager

Windows NT 4.0 uses its own boot manager which functions in a similar way to LILO and is usually installed in the MBR of the first hard disk the first partition. With this boot manager, you can start various NT versions and sometimes also existing Windows 9x.

In version 0.20, LILO is not capable of starting Windows itself if the boot sector by NT has been overwritten by LILO. Therefore, this section describes the opposite: the Windows NT boot manager stays where it is, but gets equipped with an additional menu entry for starting LILO. Thus, at computer start-up, you can easily decide between NT and LILO. (Inside LILO you may again have several options to choose from, for example, Linux kernels).

In my opinion, this is by far the most elegant way of booting Linux, because with Windows re-installations and updates (Service Packs, and so on) no problems are to be expected.

The boot manager and associated files are always installed in the first partition of the hard disk. This section assumes that the partition is a DOS (or Windows 9x) partition, but not an NTFS partition.

The following procedure should theoretically also work with NTFS partitions – however, due to lack of suitable configuration, this would not be tested. In any case, this would make the LILO set-up more complicated, because currently Linux provides no possibility for writing files to an NTFS partition. You would therefore need to copy the file bootsec onto a diskette, restart the computer under NT and then copy bootsec. to the NT partition and edit BOOT.INI.

# BOOT DISKETES/LILO 195

If you have accidentally overwritten the NT boot manager with LILO, you can either try to use lilo to restore the boot sector, or you need to start the Windows NT setup program with the installation disks and restore the boot sector with the emergency disk. Even if you have the required diskettes, this is a time consuming expensive.

> TIP

# LILO configuration

The first step is to use dd to copy the boot sector of the Linux root partition of your hard disk into a file. Which partition this is is determined by rdev (in the example below,/dev/hda8). Please be extremely careful when entering the dd command! With incorrect parameters, dd can cause a lot of damage.

```
# rdev
/dev/hda8
# dd if=/dev/hda8 bs=512 count=1 of=/boot/bootsec.lin
```

You may edit /etc/lilo.conf in such way that lilo does not change the boot sector of a hard disk or diskette, but the /boot/bootsec.lin described above. The remaining LILO settings are the same as with a LILO installation in the MBR of a hard disk (see pages 183 and 191). Thus, when you execute lilo the next time, only the bootsec.lin is changed.

```
# /etc/lilo.conf
boot=/boot/bootsec.lin
# ... all other settings as before
```

The next step is to teach the NT start program NTLDR that, as well as various Microsoft products, there is something called Linux. All files required for the startup process are in the first partition of the first hard disk (independently from the hard disk/partition in which NT itself is installed). Therefore, bootsec.lin needs to be copied into that partition.

If this partition is a FAT partition (a traditional DOS/Windows file system), you can mount this partition into the file system with mount and simply copy bootsec.lin into its root directory. However, if this partition is an NTFS partition, you need to copy bootsec.lin onto a DOS disk, start NT, and copy the file from the diskette to the NTFS partition under NT.

Now, you need to edit the NTLDR configuration file BOOT.INI (do not forget to create a backup file!) this file is also located in the root partition of the first hard disk. (In detail, the file may look different depending on your hardware configuration). For reasons of space, long lines may be split across two lines; \ is used as a separator. In BOOT.INI, these lines must be kept together!

```
[loader]
timeout=0
default=multi(0)disk(0)disk(1)partition(2)\WINNT4
[Operating systems]
multi(0)disk(0)partition(2)\WINNT4=
  "Windows NT Workstation, Version 4.0"
```

# CONFIGURATION AND ADMINISTRATION

multi(0)disk(1)partition(2)\WINNT4="Windows NT Workstation, Version 4.0" [VGA Mode] /base/video

Now, you append an additional line to the end of the file, namely:
C:\bootsec.lin\LILO

If you carry this option under Linux, you will need to be careful that you are using the correct newline. (Under DOS/Windows, an additional Ctrl-M is used. With most editors, input of this character is a long matter). The easiest solution is to copy an arbitrary line and edit it. During copying, the Ctrl-M at the end of the line is preserved.

When you restart your computer, LILO is shown in an additional line besides existing systems. When you select this option, NTLDR starts. There you have all possibilities of LILO, that is, depending on your configuration, you may choose between different kernels.

# Starting Linux from DOS (LOADIN)

With LOADIN you can start Linux within DOS. Via appropriate configuration of AUTOEXEC.BAT, DOS can be set up such way that after booting you can choose between Linux and DOS. In this respect, LOADIN is a true alternative to LILO. The biggest advantage of LOADIN is that you do not have to touch your boot sector. The disadvantage is that DOS needs to be the operating system (a DOS window under Windows is *not* sufficient). LOADIN cannot be used on computers where only NT is installed.

# Preparation

The use of LOADIN assumes that you know the device name of your root partition. If you are not sure, execute df and write down the name of the file system (in the following example, this would be /dev/sda1).

```
root# df
Filesystem 1024-blocks Capacity Mounted on
dev/sda1 303251 261723 91 /
dev/sd0 584650 584560 0 /cdrom
dev/sda2 303251 114286 173304 /home
dev/sda3 189963 /usr/local
```

Furthermore, you need a copy of the kernel file that can be read under DOS. You must copy this file into a DOS partition. The easiest way is to mount the DOS partition C: into the Linux file system and copy the kernel file (generic) into it. A safe place would be the C:\LOADIN directory which can, if necessary, create under Linux. In the mount command, instead of /dev/sda1, you must specify the name of the first DOS partition. If you do not know its name, just execute fdisk -l.

# BOOT DISKETTES/LILO 197

```
root# mkdir /dsc
root# mount -t msdos /dev/sda1 /dsc
root# mkdir /dsc/loadlin
root# cp /boot/vmlinuz /dsc/loadlin
root# cp /cdrom/dosutils/loadlin.exe /dsc/loadlin
root# umount /dsc
```

# Calling loadlin manually

The preparations under Linux are now over. Exit Linux with Ctrl-Alt-Del and boot DOS. If you normally work with Windows, exit Windows It is not sufficient to open a DOS window under Windows. In Windows 95, you can boot directly under DOS: simply press the F key during start-up and select the corresponding option. You can now try loadlin under DOS:

- > C:
- > LOADLIN /C
- > SMARTDR (keys for Windows 3.1)
- > LOADLIN vmlinuz root=/dev/sda1 ro

Instead of dev/sda1, you must specify the device name of your Linux root partition. If you need additional parameters for starting the kernel, you have to specify these as well (see page 48). If you want to work under Linux in text mode with 50 characters, the option to be used is vbox=-2

> Please note once you have started Linux you can only get back to DOS through a restart. Save all open files, exit Windows properly and so on. If you use Windows 3.1, the command SMARTDR carries out all write operations on the hard disk that might have remained open.

# Automatic start of Windows 95 or Linux

Up to this point, starting Linux from DOS still looks rather laborious. A first improvement could be to write a batch file that starts loadlin with all parameters. It would be even more elegant if immediately starting the computer, a menu up in which you could select between DOS/Windows and Linux. Such a configuration is possible for DOS 6.0 (to start either Windows 3.1 or Linux) and for DOS 7.0 to start Windows 95 or Linux.

> This section only describes the version for Windows 95. If you are still running DOS 6.0, please consult dosutils/LOADLIN.doc/manual.txt for the necessary steps. The configuration is as same as the one for Windows 95, though it uses a different syntax.

The Windows 95 boot process is controlled through two text files: C:\MSDOS.SYS and C:\CONFIG.SYS. Both files are write-protected and generally invisible. If you work with the Explorer, you must use VIEW OPTIONS to specify
