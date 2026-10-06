# TABLE 13.4 Important Subdirectories of /etc (continued)

| Subdirectory | Contents |
|--- | --- |
| pam.d | Configuration of PAM, Red Hat's security library |
| pcmcia | Configuration of PCMIA slots and devices |
| ppp | Configuration of PPP services |
| rc.d | System initialization files |
| security | Security configuration |
| skel | User environment template files |
| sysconfig | System configuration |
| X11 | X Window System configuration, including XF86Config file |

# /home: User Home Directories

The /home directory contains home directories of other users than root (whose home directory is /root). By default, a user's directory is a subpriority of /home having the same name as the user's login. However, particularly if a system has many user accounts, you may prefer to structure the /home directory differently. For example, a university might place home directories under /home/student and faculty members' home directories under /home/faculty, mounting disk volumes at these mount points.

# /lib: Shared Libraries and Kernel Modules

The /lib directory contains libraries and modules needed to boot the system and run programs residing in /sbin and /bin directories; other libraries reside in /usr/lib, /usr/X1R6/lib, and elsewhere. Modules reside in subdirectories of /lib/modules; each subdirectory is named according to the version and build number of the kernel with which the modules are associated. For example, modules for build 15 of the Linux 2.2.9 kernel might be found in /lib/modules/2.2.95.