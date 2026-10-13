Table 27-6: System Directories

| Directories | Description |
|---|---|
| /dev | Device files (Chapter 32) |
| /usr/X11 | X Window System configuration files |
| /usr/share | Shared files |
| /usr/share/doc | Documentation for applications |
| /tmp | Directory for system temporary files |

# Program Directories

Directories with "bin" in the name are used to hold programs. The /bin directory holds basic user programs, such as login, shells (BASH, TCSH, and ZSH), and file commands (cp, mv, rm, ln, and so on). The /sbin directory holds specialized system programs for such tasks as file system management (fsck, fdisk, mkfs) and system operations like shutdown and startup (init). The /usr/bin directory holds program files designed for user tasks. The /usr/sbin directory holds user-related system operations, such as useradd to add new users. The /lib directory holds all the libraries your system makes use of, including the main Linux library, libc, and subdirectories such as modules, which holds all the current kernel modules.