delete those partitions, re-create them with new sizes, and restore your data. Chapter 7 describes partition management, so you should consult it for information on how to manipulate partitions. You can back up data to a tape device or another disk using tar, but chances are you'll need to boot an emergency system to restore the data. Overall, repartitioning a working system to add a swap partition is a process that's best avoided.

If you need to add disk space, though, you can easily add swap space at the same time; just create a swap partition along with the data partitions you want to create, as described in Chapter 7. You can then add an entry to `/etc/fstab` telling the system to use the new swap partition along with an existing swap partition. When you're done, use `top` to verify that FreeBSD has recognized your new swap space.

> Because swap performance is so critical for overall system performance, you should place a swap partition where it can be accessed quickly. A location in the middle of the physical disk (between other partitions) is usually best because such a placement minimizes the time it takes to move the disk head to the swap partition.

# Adding a Swap File

If you're not adding a new disk to your computer, it's possible to add swap space by using a swap file, which is a file that FreeBSD treats like a swap partition. The procedure for adding a swap file is different for FreeBSD 4.x and 5.0. A swap file is likely to be somewhat less efficient than a swap partition because the swap file may be fragmented, increasing head movements. Nonetheless, the simplicity of adding swap space in a file more than makes up for this minor performance hit in many cases. This procedure (especially in FreeBSD 5.0) is simple enough that it can be a good way to add swap space if you need an extraordinary amount of memory on a one-time basis—say, an unusually memory-hungry program that you want to run just once.

# FreeBSD 4.x

+   To add a swap file, follow these steps:

+   1. Rebuild your kernel, as described in Chapter 12, and include the `vn` driver by using this line in your kernel configuration file:

```
pseudo-device vn 1 # vnode driver
```

+   2. Create a vn node device by typing these commands:

```
# cd /dev
# sh MAKEDEV vn0
```

+   3. Create a swap file by using `dd` to create an empty file of the desired size. For instance, to create a 100MB swap file in your root partition, you might type the following command:

```
# dd if=/dev/zero of=/swap0 bs=1048576 count=100
```