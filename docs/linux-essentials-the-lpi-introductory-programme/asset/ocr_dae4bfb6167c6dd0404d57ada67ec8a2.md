The “devices” /dev/random and /dev/urandom return random bytes of “crypto-graphic quality” that are created from “noise” in the system—such as intervals between unpredictable events like key presses. Data from /dev/random is suitable for creating keys for common cryptographic algorithms. The /dev/zero file returns an unlimited supply of null bytes; you can use these, for example, to create or overwrite files with the dd command.

# The /etc directory is very important; it contains the configuration files for most programs. Files /etc/initab and /etc/init.d/", for example, contain most of the system-specific data required to start system services. Here is a more detailed description of the most important files—except for a few of them, only user root has write permission but everyone may read them.

/etc/fstab  This describes all mountable file systems and their properties (type, access method, “mount point”).

/etc/hosts  This file is one of the configuration files of the TCP/IP network. It maps the names of network hosts to their IP addresses. In small networks and on freestanding hosts this can replace a name server.

/etc/inittab  The /etc/inittab file is the configuration file for the init program and thus for the system start.

/etc/init.d/*  This directory contains the “init scripts” for various system services. These are used to start up or shut down system services when the system is booted or switched off.

![](bbox=[0.31, 0.46, 0.91, 0.49])

/etc/issue  This file contains the greeting that is output before a user is asked to log in. After the installation of a new system this frequently contains the name of the vendor.

/etc/motd  This file contains the “message of the day” that appears after a user has successfully logged in. The system administrator can use this file to notify users of important facts and events1.

/etc/mtab  This is a list of all mounted file systems including their mount points. /etc/mtab differs from /etc/fstab in that it contains all currently mounted file systems, while /etc/fstab contains only settings and options for file systems that might be mounted—typically on system boot but also later. Even that list is not exhaustive, since you can mount file systems via the command line where and how you like.

![](bbox=[0.31, 0.72, 0.91, 0.78])

/etc/passwd  In /etc/passwd there is a list of all users that are known to the system, together with various items of user-specific information. In spite of the name of the file, on modern systems the passwords are not stored in this file but in another one called /etc/shadow. Unlike /etc/passwd, that file is not readable by normal users.

# This directory is really intended for third-party software— complete packages prepared by vendors that are supposed to be installable without conflicting with distribution files or locally-installed files. Such software packages occupy a subdirectory /opt/(package). By rights, the /opt directory should be completely empty after a distribution has been installed on an empty disk.

1 There is a well-known claim that the only thing all Unix systems in the world have in common is the “message of the day” asking users to remove unwanted files since all the disks are 98% full.