# Table 6.2 Standard directories and their contents

| Pathname | OS* | Contents |
| --- | --- | --- |
| /bin | All | Core operating system commands^b |
| /boot | LS | Kernel and files needed to load the kernel |
| /dev | All | Device entries for disks, printers, pseudo-terminals, etc. |
| /etc | All | Critical startup and configuration files |
| /home | All | Default home directories for users |
| /kernel | S | Kernel components |
| /lib | All | Libraries, shared libraries, and parts of the C compiler |
| /media | LS | Mount points for filesystems on removable media |
| /mnt | LSA | Temporary mount points, mounts for removable media |
| /opt | LSA | Optional software packages (not consistently used) |
| /proc | LS | Information about all running processes |
| /root | | Home directory of the superuser (often /) |
| /sbin | All | Commands needed for minimum system operation |
| /stand | H | Stand-alone utilities, disk formatters, diagnostics, etc. |
| /tmp | All | Temporary files that may disappear between reboots |
| /usr | All | Hierarchy of secondary files and commands |
| /usr/bin | All | Most commands and executable files |
| /usr/include | All | Header files for compiling C programs |
| /usr/lib | | Libraries; also, support for standard programs |
| /usr/lib64 | L | 64-bit libraries on 64-bit Linux |
| /usr/local | All | Software you write or install; mirrors structure of **usr** |
| /usr/sbin | All | Less essential commands for administration and repair |
| /usr/share | All | Items that might be common to multiple systems |
| /usr/share/man | All | On-line manual pages |
| /usr/src | LSA | Source code for nonlocal software (not widely used) |
| /usr/tmp | All | More temporary space (preserved between reboots) |
| /var | All | System-specific data and configuration files |
| /var/adm | | Varies: setup records, strange administrative bits |
| /var/log | LSA | Various log files |
| /var/spool | All | Spooling directories for printers, mail, etc. |
| /var/tmp | All | More temporary space (preserved between reboots)

> a = Linux, S = Solaris, H = HP-UX, A = AI.
b. On HP-UX and AI, **/bin** is a symbolic link to **/usr/bin**.
c. The distinguishing characteristic of commands in **/sbin** is usually linked with "static" versions of the system libraries and therefore don't have many dependencies on other parts of the system.

# 6.4 FILE TYPES

Most filesystem implementations define seven types of files. Even when developers add something new and wonderful to the file tree (such as process information under **/proc**), it must be made to look like one of these seven types.