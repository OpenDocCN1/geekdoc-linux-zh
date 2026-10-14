
# The e2fsck Command

This utility checks an ext2/ext3 file system. Some useful arguments taken from man e2fsck are as follows:

- -c—Checks for bad blocks and then marks them as bad.
- -f—Forces checking on a clean file system.
- -v—Verbose mode.

# The badblocks Command

Although not a performance tuning program per se, the utility badblocks checks an (preferably) unmounted partition for bad blocks. It is not recommended that you run this command by itself, but rather allow it to be called by fsck. It should only be used directly if you specify the block size accurately—don’t guess or assume anything.

The options available for badblocks are detailed in the man page. They allow for very low-level manipulation of the file system that is useful for data recovery by file system experts or for file system hacking, but are beyond the scope of this chapter and the average user.

# Disabling File Access Time

Whenever Linux reads a file, it changes the last access time—known as the atime. This is also true for your web server: If you are getting hit by 50 requests a second, your hard disk will be updating the atime 50 times a second. Do you really need to know the last time a file was accessed? If not, you can disable atime setting for a directory by typing this:

```
chattr -R +A /path/to/directory
```

The chattr command changes file system attributes, of which “don’t update atime” is one. To set that attribute, use +A and specify -R so that it is recursively set. /path/to/directory gets changed, and so do all the files and subdirectories it contains.

# Kernel

As the Linux kernel developed over time, developers sought a way to fine-tune some of the kernel parameters. Before sysctl, those parameters had to be changed in the kernel configuration and then the kernel had to be recompiled.

The sysctl command can change some parameters of a running kernel. It does this through the /proc file system, which is a “virtual window” into the running kernel. Although it might appear that a group of directories and files exist under /proc, that is only a representation of parts of the kernel. When we’re the root user (or using the sudo command), we can read values from and write values to those “files,” referred to as variables. We can display a list of the variables as shown in the following. (An annotated list is presented because roughly 250 items [or more] exist in the full list.)

```
# sysctl -A
net.ipv4.tcp_max_syn_backlog = 1024
net.ipv4.tcp_rfc1337 = 0
net.ipv4.tcp_stdurg = 0
net.ipv4.tcp_abort_on_overflow = 0
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_syncookies = 0
net.ipv4.tcp_fin_timeout = 60
net.ipv4.tcp_retries2 = 15
net.ipv4.tcp_retries1 = 3
net.ipv4.tcp_keepalive_intvl = 75
net.ipv4.tcp_keepalive_probes = 9
net.ipv4.tcp_keepalive_time = 7200
net.ipv4.ipfrag_time = 30
```

The items shown are networking parameters, and actually tweaking these values is beyond the scope of this book. If we wanted to change a value, however, the -w parameter is used:

```
# sysctl -w net.ipv4.tcp_retries2=20
```

This increases the value of that particular kernel parameter.

If you find that a particular setting is useful, you can enter it into the /etc/sysctl.conf file. The format is as follows, using the earlier example:

```
net.ipv4.tcp_retries2=20
```

Of more interest to kernel hackers than regular users, sysctl is a potentially powerful tool that continues to be developed and documented.

# TIP

The kernel does a good job of balancing performance for graphical systems, so there’s not a great deal you can do to tweak your desktop to run faster.

Both GNOME and KDE are "heavyweight" desktop systems: They are all-inclusive, all-singing, and all-dancing environments that do far more than browse your file system. The drawback to this is that their size makes them run slow on older systems. On the flip side, Ubuntu also comes with the Xfce desktop, which is a great deal slimmer and faster than the other two. If you find GNOME and KDE are struggling just to open a file browser, Xfce is for you.

# Apache

Despite being the most popular web server on the Internet, Apache is by no means the fastest. Part of the "problem" is that Apache has been written to follow every applicable
