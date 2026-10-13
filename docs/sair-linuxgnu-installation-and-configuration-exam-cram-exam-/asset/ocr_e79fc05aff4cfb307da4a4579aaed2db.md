directory. For example, you can type the following command to get to the scripts that start a number of Linux daemons:

```
cd /etc/rc.d/init.d/
```

The forward slash in front of the first directory makes this the absolute path. You can type this command from anywhere in Linux to get to this directory. Sometimes, you may accidentally type the command without the forward slash:

```
cd etc/rc.d/init.d/
```

In this case, Linux looks for these directories under your home directory. For example, if your home directory is /home/mj, this command makes Linux look for the /home/mj/etc/rc.d/init.d directory. Unless you keep a copy of these files deep in your home directory, Linux won't find anything.

![](bbox=[0.1, 0.62, 0.22, 0.73])

> A directory listing with the first forward slash is an absolute path; without the first forward slash, it is a relative path.

Linux has many directories and subdirectories. If you need to know where you are in the filesystem hierarchy, type the following command:

```
pwd
```

The pwd (present working directory) command returns your current directory.

# Mounted Drives as Directories

Removable drives are by definition located on different partitions. Because you don't always have a floppy or a CD in their drives, Linux generally does not mount these drives when you start or reboot your computer. Mounted drives can be read-only or read/write. If you want to mount your floppy drive, put a floppy in the drive, and then type the following command:

```
mount /dev/fd0 /mnt/floppy
```

The /dev/fd0 parameter is the name of the device driver assigned to your floppy drive. If you have two floppy drives, you may have to use /dev/fd1. The /mnt/floppy parameter is the directory from where you can access files on your CD-ROM.