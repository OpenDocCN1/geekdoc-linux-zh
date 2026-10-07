
# The /Proc File System • Chapter 6

an incredible amount of information stored in these subdirectories, but most of it won't be relevant to our investigation. We can, however, confirm the sizes of devices we are preparing to image without any unnecessary system commands.

```
root@localhost block]# ls -1 sda/

drwxr-xr-x 3 root root 0 2008-04-09 17:40 sda
drwxr-xr-x 3 root root 0 2008-04-09 17:39 sda2
-r--r--r-- 1 root root 4096 2008-04-09 17:40 size
```

We see two subdirectories and a file sda that are of note; sda1, sda2, and size.
root@localhost]# cat size
16777216

This corresponds to the full size of our physical disk (8 gigabytes). Now, we can determine where on this 8 gig of our partitions lie. First, sda1 (/boot):
root@localhost]# cat sda1/start
63

Next, sda2 (our LVM which contains all of our non-boot partitions):
root@localhost]# cat sda2/start
4016562
root@localhost]# cat sda2/size
163702335

We can confirm these numbers using “mmls” from the Sleuthkit.
root@localhost tmp]# mmls /dev/sda
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

| Slot | Start | Length | Description |
| :--- | :--- | :--- | :--- |
| 00: | ----- | 000000000 | 000000000 | 000000001 Primary Table (#0) |
| 01: | ----- | 000000001 | 000000062 | 000000062 Unallocated |
| 02: | 00:00 | 0000000063 | 0000401624 | 0000401624 Linux (0x83) |
| 03: | 00:01 | 0000401625 | 0016717859 | 0163702335 Linux Logical Volume Manager (0xe8) |
| 04: | ----- | 0016771860 | 0016772175 | 000005356 Unallocated |

> sleuthkit.org

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_174_0.png)

# Chapter 7

# File Analysis

Solutions in this chapter:

- The Linux Boot Process
- System and Security Configuration Files
- Log Files
- Identifying Other Files of Interest

# The Linux Boot Process

The first step in the Linux boot process is loading the kernel. The kernel is generally found in the /boot directory and will be referenced by the boot loader. Modern Linux distributions will use the Grand Unified Boot Loader (GRUB), some (namely Slackware) will still use the Linux Loader (LILO). Both serve the same purpose: loading the kernel and initiating system up. Let's look at some relevant entries from a sample grub.conf file:

```
default=0
timeout=5
```
This indicates that the default grub entry that will be booted after a 5-second delay isthe first, and in our case, only).

```
title Fedora (2.6.23-fc8)
```
This is the title that will be displayed at the boot menu for this particular GRUB entry (also known as a stanza). This tells GRUB which physical device to look for following data on; hd0, is the first hard drive and the first partition. A dual boot or multi-drive system may have different values, but this is the norm:

```
kernel /vmlinuz-2.6.23-fc8 root=/dev/VolGroup0 quiet
```
This line provides the kernel that will be booted if this stanza is selected, and the appropriate kernel options. You may recognize the boot options from /proc/cmdline. If the output of /proc/cmdline from the running system differed from what was listed here, this would indicate that someone manually edited the boot options.

```
initrd /initrd-2.6.23-fc8.img
```
This provides the location of the initial ramdisk (initrd) that will be used at boot. A ramdisk will generally contain modules that are necessary for boot (device drivers, file system modules, logical volume modules, and so forth) but are not built directly into the kernel. Once the boot loader loads the kernel, the kernel proceeds to initialize the hardware before starting process 1, /sbin/init.

# init and runlevels

Init is the very first process on a Linux system. You may remember looking at its entry in the /proc file – how does it work? There are two general ways of doing things in UNIX-like systems: System V and BSD style. Linux distributions generally follow System V for most things, including init's tasks and processing runlevels. I will be discussing the System V style, as it is the most common. init reads the /etc/initab file and executes the instructions inside. Here is a fairly standard Fedora 8 initab. The runlevels used by RHS are:

```
# Default runlevel.
# 0 halt (Do NOT set initdefault to this)
# 1 Single user mode
# 2 Multiuser, without NFS (The same as 3, if you do not have networking)
# 3 Full multiuser mode
# 4 unused
# 5 X11
# 6 reboot (Do NOT set initdefault to this)
```

```
id:5:initdefault:
```
This section defines the default runlevel the system will boot to. A runlevel describes the state a system is running. At runlevel 1, a certain set of services will run, at runlevel 2, another set, and so on through the runlevels. The seven runlevels are described above, but generally one of two will be the default: 3 (text-mode multi-user with networking) or 5 (graphical multi-user with networking).

```
# System initialization.
::sysinit:/etc/rc.d/rc.sysinit
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
```

> ¹ http://en.wikipedia.org/wiki/System_V
² http://en.wikipedia.org/wiki/BSD

```
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

init then runs the /etc/rc.d/rc.sysinit before running /etc/rc.d/rc 5, based on our default runlevel of 5. /etc/rc.d/rc then proceeds through the /etc/rc.d/ killing starting processes based on the scripts. (See Figure 7.1.)

# Figure 7.1 Contents of rc5.d

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_178_0.png)

> Note that each entry in a directory is a symbolic link to a script in /etc/init.d/, which will be started or stopped on the name of the symlink. Each script contains a myriad of variables and actions that will be taken to start or stop the service gracefully.

```
# Run getty in standard runlevels
1:2345:respawn:/sbin/getty tty1
2:2345:respawn:/sbin/getty tty2
3:2345:respawn:/sbin/getty tty3
4:2345:respawn:/sbin/getty tty4
5:2345:respawn:/sbin/getty tty5
6:2345:respawn:/sbin/getty tty6
# Run getty in standard runlevels
5:initdefault: 
```
Finally, init spawns six virtual terminals and enables the graphical display.![](img/fd8e85097b37559dbc07dc22fd8cb1fe_174_0.png)

As you can see there are numerous places an intruder can set up access to a compromised system. Careful review of all configuration files even on a stripped down system is mandatory; however, we will go into the location and function of some of the more relevant and important system and security files.

# Users, Groups, and Privileges

One of the first things you will likely want to know about a suspect is "Who has access to this machine?" /etc/passwd will tell you
root:x:0:0:root:/bin/bash
bin:x:1:1:bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin/nologin
admin:x:3:4:admin:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/bin/sync
down:x:6:0:shutdown:/sbin/shutdown
halt:x:7:0:halt:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
news:x:9:13:news:/etc/news:/sbin/nologin
uuc:x:10:14:uuc:/var/spool/uuc:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/user/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/sbin/nologin
vcsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
rpc:x:32:32:rpcbind:/var/lib/rpcbind:/sbin/nologin
nnscd:x:28:28:NSCD Daemon:/sbin/nologin
tcpcdump:x:72:72::/sbin/nologin
dbus:x:81:81:System message bus::/sbin/nologin
```
