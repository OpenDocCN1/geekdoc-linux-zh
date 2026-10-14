
## shadow-utils -- (Version 980403, 604K)

The shadow-utils package includes the necessary programs for converting UNIX password files to the shadow password format, plus programs for managing user and group accounts. The pwconv command converts passwords to the shadow password format. The pwunconv command un-converts shadow passwords and generates an /etc/passwd file (a standard UNIX password file). The pwck command checks the integrity of password and shadow files. The lastlog command prints out the last login times for all users. The useradd, userdel and usermod commands are used for managing user accounts. The groupadd, groupdel and groupmod commands are used for managing group accounts.

## shapecfg -- (Version 2.0.36, 6K)

The Shapecfg program configures and adjusts traffic shaper bandwidth limiters. Traffic shaping means setting parameters to which traffic should conform - setting the standards for bandwidth consumption. To use Shapecfg, you must have also installed the kernel which supports the shaper module (kernel versions 2.0.36 or later and late 2.1.x kernels). Install the shapecfg package if you want to set traffic bandwidth parameters, and if you have the appropriate kernel.

## termcap -- (Version 9.12.6, 424K)

The termcap package provides the /etc/termcap file. /etc/termcap is a database which defines the capabilities of various terminals and terminal emulators. Certain programs use the /etc/termcap file to access various features of terminals (the bell, colors, and graphics, etc.).

## tmpwatch -- (Version 1.5.1, 9K)

The tmpwatch utility recursively searches through specified directories and removes files which have not been accessed in a specified period of time. Tmpwatch is normally used to clean up directories which are used for temporarily holding files (for example, /tmp). Tmpwatch ignores symlinks, won't switch filesystems and only removes empty directories and regular files.

## utempter -- (Version 0.3, 21K)

Utempter is a utility which allows programs to log information to a privileged file (/var/run/utmp), without compromising system security. It accomplishes this task by acting as a buffer between root and the programs.

## util-linux -- (Version 2.9o, 960K)

The util-linux package contains a large variety of low-level system utilities that are necessary for a Linux system to function. Among many features, Util-linux contains the fdisk configuration tool and login program. You should install util-linux for its essential system tools.

## vixie-cron -- (Version 3.0.1, 57K)

The vixie-cron package contains the Vixie version of cron. Cron is a standard UNIX daemon that runs specified programs at scheduled times. Vixie cron adds better security and more powerful configuration options to the standard version of cron.

## yp-tools -- (Version 2.1, 161K)

The Network Information Service (NIS) is a system which provides network information (login names, passwords, home directories, group information) to all of the machines on a network. NIS can enable users to login on any machine on the network, as long as the machine has the NIS client programs running and the user's password is recorded in the NIS passwd database. NIS was formerly known as Sun Yellow Pages (YP). This package's NIS implementation is based on FreeBSD's YP and is a special port for glibc 2.x and libc versions 5.4.21 and later. This package only provides the NIS client programs. In order to use the clients, you'll need to already have an NIS server running on your network. An NIS server is provided in the ypserv package. Install the yp-tools package if you need NIS client programs for machines on your network. You will also need to install the ypbind package on every machine running NIS client programs. If you need an NIS server, you'll need to install the ypserv package on one machine on the network.

## Daemons

This section contains packages associated with the daemon processes that run under Red Hat Linux.

### ORBit -- (Version 0.4.2, 1,273K)

ORBit is a high-performance CORBA ORB (object request broker). It allows programs to send requests and receive replies from other programs, regardless of the locations of the two programs. You will need to install this package and
