| Directories | Description |
|---|---|
| /bin | System-related programs |
| /sbin | System programs for specialized tasks |
| /lib | System libraries |
| /etc | Configuration files for system and network services and applications |
| /home | The location of user home directories and server data directories, such as Web and FTP site files |
| /mnt | The location where CD-ROM and floppy disk files systems are mounted (Chapter 30) |
| /var | The location of system directories whose files continually change, such as logs, printer spool files, and lock files (Chapter 30) |
| /usr | User-related programs and files; includes several key subdirectories, such as /usr/bin, /usr/X11, and /usr/doc |
| /usr/bin | Programs for users |
| /dev | Device files (Chapter 32) |
| /usr/X11 | X Window System configuration files |
| /usr/share | Shared files |
| /usr/share/doc | Documentation for applications |
| /tmp | Directory for system temporary files |

# TABLE 27-6 System Directories

# Program Directories

Directories with “bin” in the name are used to hold programs. The /bin directory holds basic user programs, such as login, shells (BASH, TC SH, and ZSH), and file commands (cp, mv, rm, ln, and so on). The /sbin directory holds specialized system programs for such tasks as file system management (fsck, fdisk, mkfs) and system operations like shutdown and startup (init). The /usr/bin directory holds program files designed for user tasks. The /usr/sbin directory holds user-related system operations, such as useradd to add new users. The /lib directory holds all the libraries your system makes use of, including the main Linux library, libc, and subdirectories such as modules, which holds all the current kernel modules.

# Configuration Directories and Files

When you configure different elements of your system, like users, applications, servers, or network connections, you make use of configuration files kept in certain system directories. On Red Hat, configuration files are placed in the /etc directory, with more specific device and service configuration files located in the /etc/sysconfig directory.