Mounting a vfat diskette as we did earlier causes the Linux kernel to automatically load the vfat driver into the kernel while it is needed. The kernel module handler loads these drivers, and when they become unused after the filesystem is unmounted, they are unloaded to recover the memory that they occupied. See Chapter 27, “Configuring and Building Kernels,” for more information about kernel modules.

# ## Potential Problems with mount

Any one of several things can cause the mount command to fail, for example:

+   * **Incorrect device name**—It is possible to specify an incorrect device name (that is, a device file that does not exist or one for which a driver is not available in the kernel or for which the hardware is not present).

+   * **Unreadable devices**—Devices can be unreadable either because the devices themselves are bad (for example, empty diskette drives or bad media) or because you have insufficient permissions to mount them. Filesystems, other than those sanctioned by the administrator by listing them with the option user in /etc/fstab, are forbidden to ordinary users and require root privilege to mount them.

+   * **Bad mount point**—Trying to mount a device at a mount point that does not already exist will not work.

+   * **Other errors**—Still more error conditions are possible but unlikely (for example, exceeding the compiled-in limit to the number of mounted filesystems) or self-explanatory (for example, most usage errors for the mount command itself). There are some more unlikely error messages that chiefly relate to the loopback devices.

When you mount a filesystem, the mount point (the point at which the filesystem is to be mounted) must be a directory. This directory doesn’t have to be empty, but after the filesystem is mounted, anything underneath it is inaccessible. Linux provides a singly rooted filesystem, which is in contrast to those operating systems that give each filesystem a separate drive letter. This is more flexible because the size of data block device (hard disk or whatever) is hidden from programs, and things can be moved around. For example, if you have some software that expects to be installed in /opt/umsp, you can install it in /big-disk/stuff/umsp and make /opt/umsp a symbolic link. There is also no need to edit a myriad of configuration files that are using the wrong drive letter after you install a new disk drive.

Many options govern how a mounted filesystem behaves; for example, it can be mounted read-only. There are options for filesystems such as msdos that don’t have any concept of users. The filesystems enable you to give each file a particular file mode (for security or to allow access by everyone). When you mount an nfs filesystem, there is so much flexibility available that the options have a separate man page (man nfs), although the defaults are perfectly reasonable. The nft filesystem is explained in more detail in Chapter 16.

![](bbox=[0.94, 0.43, 0.99, 0.65])