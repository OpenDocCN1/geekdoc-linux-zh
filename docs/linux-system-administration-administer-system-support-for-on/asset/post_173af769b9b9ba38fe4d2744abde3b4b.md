
on a directory. Sockets are device files that open a network connection. These include printers, TCP/IP sessions such as telnet and FTP, and Network File System (NFS). These enable two computers or devices to talk to each other through networking.

The named pipes relate to processes. With a regular pipe ( | ), you need to use a command that is using the same process. For example,

```
$ ls | sort | head -5
```

This set of pipes takes the output of ls through the sort command. Then that output is again piped through the command head -5. The result is the first five sorted items on a directory listing. All of these commands take place during the same process. A named pipe allows the operating system to pipe different processes.

Table 4-1 lists file types.

### TABLE 4-1 FILE DESCRIPTORS

| File type | Explanation |
| :--- | :--- |
| - | File |
| d | Directory |
| l | Symbolic Link |
| c | Special Character |
| b | Block file |
| s | Socket |

## Properties

Device files don't magically appear (though they may seem to)—but neither can you create them the same way you would create a file or directory. You must use mknod, a command designed specifically for creating device files or other special files. The mknod command syntax is fairly simple:

```
mknod devicename [c] [b] majornumber minornumber
```

To create a device, first decide whether it's a block (b) or special character (c). After that, define the major number and minor number. (The major number is the type of device, such as a SCSI hard drive or mouse; the minor number is the specific device within the type of device.)

![](img/8ad518fddafc7f5e73715a2604b61d50_125_0.png)

Unlike System V UNIX operating systems, Linux does not associate a character file with a block file for hard drives.

For example, if you want to create the device file for a SCSI drive /dev/sda. In Linux, the major number for SCSI is 8. The minor number is a modulus of 16. An entire hard drive’s minor number is zero, the first partition would be 1, the second partition would be 2, and so on.

```
# mknod /dev/sda b 8 0
```

You can find the list of your major numbers for character and block devices in /proc/devices. You can also recover deleted devices from the /dev directory. For example, if you accidentally delete the secondary SCSI drive /dev/sdb, you can recover your loss by using the mknod command as follows:

```
# mknod /dev/sdb1 b 8 1
```

## Named Pipes

Named pipes represent another special capability. A *pipe* can take the output of one process over to another process, which can then use the output for its own purposes—but normally both processes must be related (that is, they must have the same parent process). A *named pipe*, however, can be used by processes that don’t have the same parent process. Additionally, any process allowed to read the data sent to the named pipe can itself be read by any process. This capability allows the piping of unrelated processes enhancing versatility.

For example, the *finger* command accesses a file called .plan and .project. Someone who wants to run an executable through the .plan file would have to use a named pipe, using the `mknod` command to create it:

```
# mknod FIFO p
```

The p after the filename defines the special file as a named pipe. In this case, the named pipe occurs in a command that mentions the exact process that makes named pipes so useful: FIFO (First In, First Out). In this process, the first data written to the pipe is also the first data read from it.

## Mounting Devices

The `mount` command is designed to attach devices with directories under the / directory. Any device will work; it doesn't necessarily have to be in the /etc/fstab. To mount a device, use the mount command with the -t option.

The /etc/fstab file looks something like this:

```
/dev/hda1      /       ext2       defaults      1      1
/dev/hda2      /usr    ext2       defaults      1      1
/dev/hda3      /var    ext2       defaults      1      1
/dev/hdc       /cdrom  iso9660    ro            0      0
none           /proc   proc       defaults      0      0
```

The command resembles this example:

```
mount -t filetype device directory
```

Thus, if you wanted to mount a CD-ROM, you could use the following command:

```
# mount -t iso9660 /dev/cdrom /cdrom
```

This specific command mounts an ISO 9660-format CD-ROM to the directory /cdrom. If a different device is already on /cdrom, it's hidden until the device /dev/cdrom is unmounted.

If you want to make the file systems mount simultaneously, use the -F option with -a. This form of the command causes the mount processes to fork. Consider the following command:

```
# mount -a -F -t msdos
```

This particular mount command forks the mounts of all file systems that correspond to the type msdos in the /etc/fstab. Though the command mounts all file systems of the specific file type simultaneously, it does have limitations. In particular, you cannot use -F to mount two directories that are dependent on each other. An example would be two partitions, one on /usr and the other on /usr/bin- sorry, mount won't do it.

You can, however, mount the system as read-only or read-write. To do so, pass the options -o ro or -o rw as shown here:

```
# mount -o ro /dev/fd0 /floppy
```

This command mounts the floppy drive as read-only. If you want to include other options when you mount a device, you can. If, for example, you want to let your users mount a device as read-only, you can do so with the -o option. The -o option is a handy way to add other options; you can also put them into the /etc/fstab file in the fourth field.

The defaults for mounting a device are `rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, and `async`. If you want to enable the defaults, pass the option `defaults`. The following command uses the `-o` option to do so:

```
# mount /dev/hda2 -o defaults
```

If you need to mount file systems that are already mounted, you can use the `remount` option to do so. It’s a handy capability if you’re changing a mount flag (`ro`, `user`, and so on) on a particular file system. Table 4-2 lists mounting types and options.

### TABLE 4-2 MOUNTING OPTIONS

| Mounting Type | Should be done | Shouldn't be done |
| :--- | :---: | :---: |
| Mount files synchronously? | `sync` | `async` |
| Mount file as writable? | `rw` | `ro` |
| Update inode access time? | `atime` | `noatime` |
| Mount with -a option? | `auto` | `noauto` |
| Is it a character or block device? | `dev` | `nodev` |
| Need to be root? | `nouser` | `user` |
| Allow SUID bits? | `suid` | `nosuid` |
| Execute binaries? | `exec` | `noexec` |

The computer recognizes floppy drives without adding any drivers to the kernel. Currently, 1.2MB and 1.44MB drives are supported—but expect the support for 1.2MB drives to go away soon; new PCs don’t use them.

Floppy-drive device files are noted by `fd`. For example, the first floppy drive on your system is `/dev/fd0` (Slackware Linux counts the same way arrays are counted in C—starting with zero). The second floppy drive would be `/dev/fd1`, and so on.

## Floppy Drives

If you want to use your floppy drive after installing Linux, you have only a few steps to take:

- 1. Become root.
- 2. Make a directory in which to mount the floppy drive.
- 3. Stick in the disk.
- 4. Mount the directory.

I have one floppy drive, so I can show you the steps I go through to mount it on a Linux system. First, to look at what's already mounted, use the mount command.

```
# mount
/dev/hda1 on / type ext2 (rw)
/dev/hda2 on /home type ext2 (rw)
/dev/hda3 on /opt type ext2 (rw)
none on /proc type proc (rw)
```

Look - no floppy drive mounted (you can't see /dev/fd0 on the list of drives). If I'm mounting the drive for the first time, I would have to create a directory to serve as a mount point for the floppy drive (say, one creatively called /floppy). You can call your drive whatever you want - /dosa (since the drive is recognized as msdos file format), /fred, /mom - and our practical example looks like this:

```
# mkdir /floppy
```

When you've created the directory, mount the drive:

```
# mount /dev/fd0 /floppy/
```

If it mounts properly, you won't see any error messages and you'll return to the prompt. If you want to double-check to see whether your drive mounted properly, type the mount command again. The result would resemble the following snippet:

```
# mount
/dev/hda1 on / type ext2 (rw)
/dev/hda2 on /home type ext2 (rw)
/dev/hda3 on /opt type ext2 (rw)
none on /proc type proc (rw)
/dev/fd0 on /floppy type msdos (rw)
```

The drive is mounted; if you do an ls on the /dev/fd0 next, here's what you get:

```
# ls /dev/fd0
/dev/fd0
```

Not much. What you need to do is an ls on the mount point - in this case, /floppy, as follows:
