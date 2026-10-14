The Linux Cookbook: Tips and Techniques for Everyday Use:

+   - To peruse a directory tree graph of the CD-ROM's contents, type:

```
```bash
$ tree /usr/local/share/clipart | less RET
```
```

+   - To change to the root directory of the CD-ROM, type:

```
```bash
$ cd /usr/local/share/clipart RET
```
```

+   - To list the contents of the root directory of the CD-ROM, type:

```
```bash
$ ls /usr/local/share/clipart RET
```
```

# 25.4.2 Unmounting a CD-ROM

Use umount to unmount a CD-ROM; give as an argument the name of the directory it's mounted on.

+   - To unmount the disc in the CD-ROM drive mounted on `/cdrom`, type:

```
```bash
$ umount /cdrom RET
```
```

> **NOTE:** As with unmounting any kind of filesystem, make sure that none of the files on the disc are in use, or you won't be able to unmount it. For example, if the current working directory in a shell is somewhere inside the `/cdrom` directory tree, you won't be able to unmount the CD-ROM until you change to a different directory.