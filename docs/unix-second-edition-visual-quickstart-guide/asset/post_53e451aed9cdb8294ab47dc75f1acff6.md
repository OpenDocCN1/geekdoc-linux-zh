
## Table B.2
### Common Unix Directories and Their Contents

| DIRECTORY | CONTENTS |
|---|---|
| /bin | Essential programs and commands for use by all users. |
| /boot | Files that the system boot loader uses. |
| /dev | Devices (CD-ROM, serial ports, etc.) and special files. |
| /etc | System configuration files and global settings. |
| /etc/skel | Template configuration files for individual users. |
| /etc/X11 | Configuration files and information for the X Window System. |
| /home | Home directories for users. |
| /lib | Essential shared libraries and kernel modules. |
| /mnt | Mount point for temporarily mounted file systems. |
| /opt | Directory for add-on application software packages. |
| /proc | Location of kernel and process information (virtual file system). |
| /root | Home directory for the root user/system administrator. |
| /sbin | Essential programs and commands for system boot. |
| /tmp | Temporary files. |
| /usr/bin | Commands and programs that are less essential for basic Unix system functionality than those in /bin but were installed with the system. |
| /usr/include | Standard include files and header files for C programs. |
| /usr/lib | Libraries for programming and for installed packages. |
| /usr/local | Most files and data that were developed or customized on the system. |
| /usr/local/bin | Locally developed or installed programs. |
| /usr/local/man | Manual (help) pages for local programs. |
| /usr/local/src | Source code for locally developed or installed programs. |
| /usr/sbin | Additional nonessential standard system binaries. |
| /usr/share | Shared (system-independent) data files. |
| /usr/share/dict | Word lists. |
| /usr/share/man | Manual (help) pages for standard programs. |
| /usr/share/misc | Miscellaneous shared system-independent data. |
| /usr/src | Source code for standard programs. |
| /usr/X11R6 | X Window System, Version 11 Release 6. |
| /usr/X386 | X Window System, Version 11 Release 5, on x86 platforms. |
| /var | Changeable data, including system logs, temporary data from programs, and user mail storage. |
| /var/account | Accounting logs, if applicable. |
| /var/cache | Application-specific cache data. |
| /var/cache/fonts | Locally generated fonts. |
| /var/cache/man | Formatted versions of manual pages. |
| /var/crash | Information stored from system crashes, if applicable. |
| /var/games | Variable game data. |
| /var/lock | Lock files created by various programs. |
| /var/log | Log files and directories. |
| /var/mail | User mailbox files. |
| /var/run | Run-time variable files. |

### Common Unix Directories and Their Contents (continued)

| DIRECTORY | CONTENTS |
|---|---|
| /var/spool | General application spool data. |
| /var/spool/cron | Contains cron and at job schedules. |
| /var/spool/lpd | Line-printer daemon print queues. |
| /var/spool/mail | Contains incoming mail for users. |
| /var/state | Variable state information for the system. |
| /var/state/editorname | Editor backup files and state information. |
| /var/state/misc | Miscellaneous variable data. |
| /var/tmp | Temporary files that the system keeps through reboots. |
| /var/yp | Database files that the Network Information Service (NIS) uses. |

## COMMAND FLAGS

This appendix provides a list of many (but certainly not all) Unix commands and programs as well as many of the related command-line flags.

In general, flags offer a thorough selection of options for programs that operate exclusively from command-line input, as well as an overview of the functionality for many other programs. Please keep in mind, however, that command flags only touch the surface of the capabilities of interactive programs (like pico, vi, links, or pine) or particularly complex programs that rely on special expressions (such as grep or tr) or that use multiple files or sources for information (such as procmail).

Table C.1 should provide you with a brief reminder and starting point for learning more about these Unix commands. While the flags we’ve included here work on our systems, they will likely vary somewhat on different systems, different Unix versions or with different shells. Check your local man pages for specifics.

Note that multiple equivalent commands or flags all appear on the same line, separated by commas. Additionally, multiple flags (unless contradictory) can be used with all commands. The [] brackets indicate that one of the options enclosed may be used.
