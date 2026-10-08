# CHAPTER 3 | Security: Facilities for the Boot Process

```
# /etc/fstab: static file system information.
# Use 'blkid -o uuid' to print the princially unique identifier
# for a device; this may be used with UUID= as a more robust way to name
# devices that works if disks are added and removed. See fstab(5).
```

```
# <file system> <mount point> <options> <dump> <pass>
# /proc proc defaults
# / was on /dev/vda3 during installation
UUID=613b0ff5-3c73-4132-800c-da3890abaf55 / ext4 errors=remount-ro
# /boot was on /dev/vda2 during installation
UUID=9197a6b4-db42-4082-aff8-99ec2752 / defaults
# swap was on /dev/vda5 during installation
UUID=#476467ff-9ac3-44c-9840-3cc5f286f swap sw 0
# /mapper/cryptswap1 now swap sw 0
```

FIGURE 3-4
The /etc/fstab file
can use more obscurity.

are are also included to identify the original value device files. The permissions for /etc/fstab make it "world-readable". Any black-hat hacker can read this file and get too much information about what directories are mounted on volumes.
Comments in /etc/fstab are not necessary for mounting directories. You can safely delete them without affecting the boot process.

# Obscurity in Services

Linux services themselves cannot be easily hidden within a system. Many configuration files and scripts are tied to standard file names. If you change a file name or directory, chances are good that you will also need to change some software code. The level of effort required to make such changes is rather high.
Obscurity in services relates normally to the network port on which that service communicates. Standard ports for many services are shown in the /etc/services file. While it's not difficult to change the communications port for many services, you'd also need to change the communications ports for firewalls, clients, and more.
For information on service-related security, read Chapters 6 and 7. After reading those chapters, you may decide that obscurity in services is not worth the effort required to configure it.
Besides, with tools like nmap command, it's not very difficult for a black-hat hacker to identify nonstandard ports for network services. And those nonstandard ports may confuse your users, violating the principles of availability and utility in the CIA triad and Parkerian hexad.