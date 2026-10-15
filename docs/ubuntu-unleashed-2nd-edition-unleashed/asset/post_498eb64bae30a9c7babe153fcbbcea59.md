
```
$ sudo cdrecord -scanbus
scsibus1:
    1,0,0     100) 'IDE-DVD ' 'ROM 6116      ' 'DD04' Removable CD-ROM
    1,1,0     101) ' _NEC     ' 'DVD_RW ND-3500AG' '2.86' Removable CD-ROM
    1,2,0     102) *
    1,3,0     103) *
    1,4,0     104) *
    1,5,0     105) *
    1,6,0     106) *
    1,7,0     107) *
```

Here, we see that the CD/DVD writer (in this example, a DVD writer) is present and is known by the system as device 1,1,0. The numbers represent the SCSI bus/target/LUN (logical unit number) of the device. You will need to know this device number when you burn the CD or DVD, so write it down or remember it.

## TIP

An IDE drive used to create CDs and DVDs needs to be emulated as a SCSI drive. Ubuntu does this automatically when you first install it, but in case you need to do it manually, here are the few items you need to configure (assuming that the CD drive is at `/dev/hdd`):

- Add the following line to the `/etc/modules.conf` file:

  ```
  probeall ide-scsi
  ```

- Edit the `/boot/grub/menu.lst` file to add the following to the kernel commands:

  ```
  hdd=ide-scsi
  ```

- Reboot your computer.

These items will load the appropriate modules and provide SCSI emulation. You would no longer refer to the CD drive as `/dev/hdd`, but as `/dev/scd0`. Check the symbolic link for `/dev/cdrom` to make certain that it points to `/dev/scd0`.

However, because Ubuntu uses the 2.6 kernel, SCSI emulation is not necessary, although it is useful information should something not work correctly.

## Creating CDs from the Command Line

In Linux, creating a CD is a two-step process. You first create the iso9660-formatted image, and you then burn or write the image onto the CD. The iso9660 is the default file system for CD-ROMs.

Use the mkisofs command to create the ISO image. The mkisofs command has many options (see the man page for a full listing), but use the following for quick burns:

```
$ mkisofs -r -v -J -l -o /tmp/our_special_cd.iso /source_directory
```

The options used in this example are as follows:

- `-r`—Sets the permission of the files to more useful values. UID and GID (individual and group user ID requirements) are set to zero, all files are globally readable and searchable, and all files are set as executable (for Windows systems).

- `-v`—Displays verbose messages (rather than terse messages) so that you can see what is occurring during the process; these messages can help you resolve problems if they occur.

- `-J`—Uses the Joliet extensions to ISO9660 so that our Windows-using buddies can more easily read the CD. The Joliet (for Windows), Rock Ridge (for UNIX), and HFS (for Mac) extensions to the ISO9660 standard are used to accommodate long filenames rather than the eight-character DOS filenames that the ISO9660 standard supports.

- `-l`—Allows 31 character filenames; DOS will not like it, but everyone else does.

- `-o`—Defines the directory where the image will be written (that is, the output) and its name. The `/tmp` directory is convenient for this purpose, but the image could go anywhere you have write permissions.

- `/source_directory`—Indicates the path to the source directory; that is, the directory containing the files we want to include. There are ways to append additional paths and exclude directories (and files) under the specified path—it is all explained in the man page, if you need that level of complexity. Our simple solution is to construct a new directory tree and populate it with the files we want to copy, and then make the image using that directory as the source.

Many more options are available, including options to make the CD bootable.

After you have created the ISO image, you can write it to the CD with the cdrecord command:

```
$ cdrecord -eject -v speed=12 dev=0,0,0 /tmp/our_special_cd.iso
```

The options used in this example are as follows:

- `-eject`—Ejects the CD when the write operation is finished.

- `-v`—Displays verbose messages.

- `speed=`—Sets the speed; the rate depends on the individual drive's capabilities. If the drive or the recordable medium is poor, you can use lower speeds to get a good burn.

- `dev=`—Specifies the device number of the CD writer (the number I told you to write down earlier).
