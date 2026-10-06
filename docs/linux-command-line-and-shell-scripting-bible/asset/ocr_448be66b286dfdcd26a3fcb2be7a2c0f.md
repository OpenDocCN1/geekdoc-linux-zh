# Part I The Linux Command Line

# The killall command

The killall command is a powerful way to stop processes by using their names rather than the PID numbers. The killall command allows you to use wildcard characters as well, making it a very useful tool when you've got a system that's gone awry.

> CAUTION Be extremely careful using the killall command when logged in as the root user. It's easy to get carried away with wildcard characters and accidentally stop important system processes. This could lead to a damaged filesystem.

# Monitoring Disk Space

Another important task of the system administrator is to keep track of the disk usage on the system. Whether you're running a simple Linux desktop or a large Linux server, you'll need to know how much space you have for your applications.

There are a few command line commands you can use to help you manage the media environment on your Linux system. This section describes the core commands you'll likely run into during your system administration duties.

# Monitoring media

As discussed in Chapter 3, the Linux filesystem combines all media disks into a single virtual directory. Before you can use a new media disk on your system, you need to place it in the virtual directory. This task is called mounting.

In today's graphical desktop world, most Linux distributions have the ability to automatically mount specific types of removable media. A removable media device is a medium that (obviously) can be easily removed from the PC, such as CD-ROMs, floppy disks, and, USB memory sticks.

If you're not using a distribution that automatically mounts and unmounts removable media, you'll have to do it yourself. This section describes the Linux command line commands to help you manage removable media devices.

# The mount command

Oddly enough, the command used to mount media is called mount. By default, the mount command displays a list of media devices currently mounted on the system:

```
$ mount
dev/mapper/VolGroup0-LogVol100 on / type ext3 (rw)
proc on /proc type proc (rw)
sys on /sys type sysfs (rw)
devpts on /dev/pts devpts (rw,gid=5,mode=620)
/dev/sda1 /boot type ext3 (rw)
```