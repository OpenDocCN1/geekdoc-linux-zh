```
mdir a:\
```

I can use mcopy to copy the file "autoexec.bat" from the root directory to the floppy to my
current directory on Linux:

```
mcopy a:\autoexec.bat
```

You have to be root to be able to write to a floppy.

Type "mtools" to the supported commands in the rich mtools set, which parallel the most popular
DOS commands (for example: mformat, mtype, mren, mmove, mdel, mrd, mattib, ...), and
manual pages if you have problems using them. For example:

```
man mtype
```

will show how to display a content of a text file on a DOS partition.

To access DOS drives other than a or b; you have to configure mtools as to indicate
devices with other DOS "drive letters". This is quite easy--just edit and modify the
file /etc/mtools.conf. I typically use pico to do it (as the root):

```
pico /etc/mtools.conf
```

For example, my /etc/mtools.conf contains a line like this:

```
drive c: file="/dev/hda1"
```

which instructs the mtools that the partition "dev/hda1" will be called "c:" The setup of
/etc/mtools.conf requires uncommenting (removing the "#" at the beginning of the line)
ad adjusting the appropriate entry.

# 4.2 Mounting works when I am root. Can a normal user mount?

You have to edit the file /etc/fstab as root to give the normal users the permission to mount a
drive. For example I can use the pico editor to do this:

```
pico -w /etc/fstab
```

The option "-w" turns off the long line wrap.

Here is the content of my /etc/fstab:

```
/dev/hda2 /ext2 defaults 1 1
/dev/hdc3 /home ext2 defaults 1 2
/dev/hdc2 /usr ext2 defaults 1 2
/dev/hdc4 swap defaults 0 0
/dev/fd0 /mnt/floppy auto noauto,users,rw 0 0
/dev/cdrom /mnt/cdrom auto noauto,user,ro 0 0
/dev/sda4 /mnt/zipdrive vfat noauto,user,rw,exec 0 0
```