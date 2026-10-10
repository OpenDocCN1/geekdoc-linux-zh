# **Table 3.2** Critical Linux Directories

| Linux Directory | Purpose |
| :--- | :--- |
| `/` | Pronounced "root," the root directory is the top-tier directory. It is the most important directory and is required to boot the Linux system. It contains core directories and files. This includes utilities, configuration files, bootloader information, and start-up information required for the initialization of the Linux system. |
| `/bin` | The /bin directory contains Linux commands used by the system administrator and users. The commands in this directory are also accessible when the system is in single-user mode. |
| `/dev` | A unique feature about Linux operating systems is its treatment of devices (for example, terminals). The Linux system treats devices as directories (folders). The /dev directory is used within the Linux environment to mount devices. |
| `/etc` | To control the execution of programs and support the dynamic Linux environment, the /etc directory is used. This directory contains Linux system and application configuration files. |
| `/media` | The /media directory is used to mount removable media (for example, floppy disks, CD/DVD drives, and USB/Thumb Drives) for access by the system administrator and users. |
| `/mnt` | The /mnt directory, similar to the /media directory, is used to temporarily mount filesystems. |
| `/proc` | The /proc directory functions as a virtual filesystem for system processes and the Linux kernel. |
| `/root` | The /root directory, not to be confused with the root directory, is the home directory assigned to the root user account. |
| `/sbin` | The /sbin directory is used to contain Linux utilities that are used only by the Linux system administrator (for example, root). It contains executables for critical booting, restoring, recovering, and/or repairing the Linux system. |
| `/usr/bin` | The /usr/bin directory, unlike the /sbin directory, contains the primary Linux executable commands on this system. Linux users and the root user can execute the commands in this directory. |
| `/usr/lib` | The /usr/lib directory contains software libraries and packages for programs. This includes object files and internal binaries that are platform-specific. |
| `/usr/lib64` | The /usr/lib64 directory performs the same function as the /usr/lib directory, but for an alternative binary format. This directory supports the 64-bit architecture. |

(Continued)