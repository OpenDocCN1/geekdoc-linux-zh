| Command | Syntax (Example) | Description |
|---|---|---|
| `du` | `du` | Displays disk usage for the current directory and all subdirectories. |
| `echo` | `echo` | Displays a line of text. |
|  | `echo` |  |
|  | `echo $PATH` | Commonly used to display the value of a given environment variable. |
| `e2fsck` | `e2fsck <file system>` | Filesystem check routine for ext2 filesystems. |
| `fdisk` | `fdisk <hard drive>`<br>(hard drive = device) | Used to create and/or manipulate a partition table for a given hard drive. |
| `free` | `free` | Displays the total amount of free and used memory. Also shows swap space usage. |
| `fsck` | `fsck <file system>` | Front-end program that calls filesystem check routines for a specific filesystem type. Defaults to ext2. |
| `fsck.ext2` | `fsck.ext2 <file system>` | See e2fsck. |
| `ftpshut` | `ftpshut` | Shuts down ftp services at a specified time. |
| `insmod` | `insmod <module>` | Inserts a loadable module. |
| `kill` | `kill <PID>` | Kills the specified process. |
| `killall` | `killall <name>` | Kill all processes that are executing the specified command. |
| `lilo` | `lilo` | Reinstalls the boot loader. |
| `lsmod` | `lsmod` | Lists all currently loaded modules. |
| `mke2fs` | `mke2fs <partition>` | Creates an ext2 type filesystem on the specified hard drive partition. |
| `mkfs` | `mkfs <partition>` | Front-end program that calls make filesystem routines for a specific filesystem type. Defaults to ext2. |
| `mkfs.ext2` | `mkfs.ext2 <partition>` | See mke2fs. |
| `mknod` | `mknod <device> type maj min` | Makes device files. |
| `modprobe` | `modprobe <module>` | Used to load a module or a set of dependent modules. |
| `mount` | `mount <device>`<br>`<dirmount point>` | Mounts a filesystem (device) to a specified directory (mount point). |
| `ps` | `ps`<br>`ps aux` | Displays the process table. Process IDs (PID) for currently running jobs can be identified with this command. |
| `pwconv` | `pwconv` | Used to convert a traditional `/etc/` passwd file to use shadow passwords. |