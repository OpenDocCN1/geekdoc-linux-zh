# Command-Line Tools

Using the HFS utilities is fairly easy. You need to know the proper device for the desired volume to use. For example, after installing PowerPC Linux on your Macintosh, you should know the partition number for at least one Mac HFS volume. Note that one limitation of the HFS utilities is that they only work with HFS standard volumes, not new HFS extended volumes.

![](bbox=[0.05, 0.25, 0.12, 0.34])

> Support for the Mac OS HFS+ filesystem has started, but is still in its infancy and no software has been released. The current project (see "Resources" at the end of this chapter) aims to provide some form of support in the Linux 2.4-series kernels.

In order to access an HFS volume, use the mount command, followed by a device name, like this (as root):

```
```
# mount /dev/hda10
Volume name is "hfsboot"

Volume was created on Thu Apr 5 15:59:00 2001
Volume was last modified on Tue Apr 10 15:13:43 2001
Volume has 18280448 bytes free
```
```

You can then get information about the volume by using the hvol command like this:

```
```
$ hvol
Current volume is mounted from:

    /dev/hda10

Volume name is "hfsboot"
Volume was created on Thu Apr 5 15:59:00 2001
Volume was last modified on Tue Apr 10 15:13:43 2001
Volume has 18280448 bytes free
```
```

To list files and directories on the volume, use the hls command:

```
```
$ hls
Desktop Folder  Linux Kernels  System Folder
```
```

# Graphical HFS Tools

For a graphical interface to using and manipulating your mounted HFS volume during an X session, use the xhfs client from the command line like this (as root):

```
```
# xhfs &
```
```