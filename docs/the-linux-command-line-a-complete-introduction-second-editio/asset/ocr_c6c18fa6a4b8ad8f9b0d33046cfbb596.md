| Directory | Comments |
|---|---|
| */lost+found* | Each formatted partition or device using a Linux file system, such as ext3, will have this directory. It is used in the case of a partial recovery from a file system corruption event. Unless something really bad has happened to your system, this directory will remain empty. |
| */media* | On modern Linux systems, the */media* directory will contain the mount points for removable media such as USB drives, CD-ROMs, and so on, that are mounted automatically at insertion. |
| */mnt* | On older Linux systems, the */mnt* directory contains mount points for removable devices that have been mounted manually. |
| */opt* | The */opt* directory is used to install “optional” software. This is mainly used to hold commercial software products that might be installed on the system. |
| */proc* | The */proc* directory is special. It’s not a real file system in the sense of files stored on your hard drive. Rather, it is a virtual file system maintained by the Linux kernel. The “files” it contains are peepholes into the kernel itself. The files are readable and will give you a picture of how the kernel sees your computer. |
| */root* | This is the home directory for the root account. |
| */sbin* | This directory contains “system” binaries. These are programs that perform vital system tasks that are generally reserved for the superuser. |
| */tmp* | The */tmp* directory is intended for the storage of temporary, transient files created by various programs. Some configurations cause this directory to be emptied each time the system is rebooted. |