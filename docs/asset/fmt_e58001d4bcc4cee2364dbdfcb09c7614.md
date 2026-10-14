
To mount a floppy disk to a specific directory, use `mount` and give as arguments the device name of the floppy drive (usually `/dev/fd0` for one-floppy systems) and the name of the directory to mount to.

⇒ To mount the floppy in the first floppy drive to `~/tmp`, type:

```
$ mount /dev/fd0 ~/tmp [RET]
```

Once you have mounted a floppy, its contents appear in the directory you specify, and you can use any file command on them.

⇒ Here are two ways to use this.

- To list the contents of the base directory of the floppy mounted on `/floppy`, type:

  ```
  $ ls /floppy [RET]
  ```

- To list the contents of the entire directory tree on the floppy mounted on `/floppy`, type:

  ```
  $ ls -iR /floppy [RET]
  ```

NOTES: You can copy files to and from the directory tree that the floppy is mounted on, make and remove directories, and do anything else you could on any other directory tree. But remember, before you remove it, you must first unmount it.

### 24.3.3 Unmounting a Floppy Disk

Use `umount` to unmount a floppy disk, using the name of the directory it is mounted on as an argument.

⇒ To unmount the floppy that is mounted on `/floppy`, type:

```
$ umount /floppy [RET]
```

NOTES: You can't unmount a disk if your current working directory, the directory you are in, is somewhere in that disk's directory tree.³ In this case, trying to unmount the disk will give the error that the `/floppy` filesystem is in use; change to a different directory that isn't in the `/floppy` directory tree, and then you can unmount the disk.

Sometimes when you unmount a floppy, the light on the floppy drive will go on and remain on for a few seconds after it has been unmounted. This is because Linux sometimes keeps changes to files in memory before it writes them to disk; it’s making sure that the files on the floppy are up-to-date. Simply wait until the light goes off before you remove the floppy from the drive.

## 24.4 Using Data CDs

As with a floppy disk, before you can use a data CD (“compact disc”) on your system, you must first mount it on an empty directory. You then unmount it from the directory before you can eject the CD from the CD drive (you can also eject the disc using software—see Recipe 22.1.6 [Ejecting an Audio CD], page 480).

**NOTES:** To use audio CDs, see Chapter 22 [Audio Compact Discs], page 477.

### 24.4.1 Mounting a Data CD

To mount a data CD on the system, use `mount` with the `/cdrom` option.⁴

⇒ To mount a data CD on the system, type:

```
$ mount /cdrom [RET]
```

This command makes the contents of the data CD available from the `/cdrom` directory tree. You can use any Linux file command on the files and directories on a data CD, but you can only write to one if it is a CDRW disc.

Like the `/floppy` directory, the use of the `/cdrom` directory is a standard practice and convenient, but not necessary—you can mount disks in whatever empty directory you like. (You could even, for example, mount discs from the CD drive to `/floppy` and mount floppy disks to `/cdrom`, but why would anyone do that!)

To mount a data CD to a specific directory, use `mount` and give as arguments the name of the device file in `/dev` corresponding to the CD drive, and the name of the directory to mount to. This directory must already exist on the filesystem, and it must be empty. If it doesn’t exist, use `mkdir` to create it first (see Recipe 5.1.2 [Making a Directory], page 130).

Most Linux systems are set up so that the device file of the first CD drive is `/dev/cdrom`, but the name of the device file may be different, especially if you have a SCSI CD-ROM drive.

⁴ This works if your administrator has set up the CD drive filesystem for user access—see Recipe A.6.3 [Letting Users Access Hardware Peripherals], page 718.

⇒ 要将 CD 驱动器中的光盘挂载到 `/usr/local/share/clipart` 目录，请键入：

```
$ mount /dev/cdrom /usr/local/share/clipart [RET]
```

CD 驱动器中光盘的内容随后将可在 `/usr/local/share/clipart` 目录树中使用，然后你就可以像使用其他任何文件一样使用数据 CD 上的文件和目录。

⇒ 以下是一些使用方法。

- 要浏览数据 CD 内容的目录树图，请键入：
