# Enabling a Swap Area

To enable swapping, use the swapon command:

```
```
# swapon /swapfile
# swapon /dev/hdc3
```
```

The first example enables swapping on a swap file; the second enables a swap partition.

If you want a swap partition to be activated every time you boot the system, add a line like this to /etc/fstab:

```
```
/dev/hdc3  swap  swap  defaults 0 0
```
```

The swap in the mount_point and type partition informs the bootup scripts that /dev/hdc3 is a swap partition. You can enable swapping on all partitions listed in /etc/fstab like this:

```
```
# swapon -a
```
```

> **Note**
> You cannot change the size of a swap file while it is being used for swap space. You can only do this by disabling swapping on the file, changing its size, rerunning mkswap, and re-enabling swapping.

swapon has a -p option that lets you set the "priority" of a swap space. The option takes an integer argument between 0 and 32767. The higher the number, the higher the priority. Higher-priority swap areas are used in preference to lower-priority ones. If you have both swap partitions and swap files, give the swap partitions a higher priority because they have better performance.

In /etc/fstab, you can put a pri=n entry in the opts field to set the priority of a swap area.

swapon has a very useful -s option, which displays the status of your swap areas:

```
```
$ swapon -s
```
```

```
```
Filename  Type  Size  Used  Priority
/dev/hda4  partition  377520  0  -1
```
```