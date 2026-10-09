
## Navigating the File System

In this section we shall look at the file organization of Red Hat Linux 9 in general, based on the various utilities that are available and also the location of configuration files. The root file system is indicated by the /. Let us list the contents of the root file system:

```
$ ls -F /
bin/ dev/ home/ lib/ misc/ opt/ root/ tftpboot/ usr/
boot/ etc/ initrd/ lost+found/ mnt/ proc/ sbin/ tmp/ var/
```

The end-user utility programs are organized under the /bin, /usr/bin, and /usr/local/bin directories. The tables below list some of the common programs under these directories. It is very useful to ensure that these directories are set in the PATH environment variable.

> *Remember, you can get full information on each of these by querying their man pages, and abridged details by typing the command followed by --help.*

Let's look at each of these directories in some detail.

### Commands Found in the /bin Directory

The following are all commands, located in the /bin directory:

| Command | Description |
| :--- | :--- |
| awk | Pattern scanning and processing language |
| bash | The Bourne-again shell |
| cat | Concatenates files and prints on to standard output |
| chgrp | Changes the group ownership |
| chmod | Changes file access permissions |
| chown | Changes file ownership permissions |
| cp | Copies files and directories |
| cpio | Copies files to and from archives |
| csh | C-shell |
| cut | Removes sections from each line of input |
| date | Prints the current date and timestamp. Super user may set the date and time |
| dd | Converts and copies files |
| df | Displays disk usage for file systems |
| dmesg | Displays startup messages |
| echo | Displays a line of text |
| ed | An old text editor |
| grep | Regular expression matching program |
| gzip | GNU zip program for compressing files |
| kill | Terminates running processes |
| ln | Creates links to files and directories |
| ls | Lists files |
| mail | Command-line mail client |
| mkdir | Creates a directory |
| more | Paginates a file |
| mount | Maps a file system to a directory |
| mv | Moves a file from one location to another; same as re-naming a file |
| netstat | Prints network statistics |
| ping | Checks for the network reachability of other machines on the network. |
| ps | Lists currently running processes |
| pwd | Displays current working directory |
| rm | Removes files |
| rmdir | Removes directories |
| sed | Stream editor can be used to edit files, output of programs etc. |
| sh | Bourne shell |
| sleep | Delays for a specific amount of time |
| sort | Sorts the lines of input |
| su | Changes identity of a user |
| tar | Archiving program |
| tcsh | Enhanced C shell |
| touch | Updates the time-stamp on a file |
| umount | Unmount a currently mounted file system |
| uname | Prints system information |
| vi | A text editor |

### Commands Found in the /usr/bin Directory

The following are also commands, and they’re located in the /usr/bin directory:

| Command | Description |
| :--- | :--- |
| at | Queue jobs for later execution |
| bc | A bench calculator |
| cc | C-compiler. This command is a symbolic link to the GNU C-compiler gcc. |
| clear | Clears the screen |
| crontab | Maintains a list of tasks to be performed later |
| du | Reports disk usage for a directory and subdirectories |
| emacs | An editor |
| F77 | Fortran compiler |
| file | Prints file type |
| find | File-searching utility |
| finger | Looks up user information |
| ftp | File transfer program |
| gcc | GNU C-compiler |
| gdb | GNU debugger |
| gftp | Graphical FTP client |
| gimp | GNU Image manipulation and painting program |
| gmake | Maintains a group of programs. This command is a symbolic link to the GNU make command gmake. |
| head | Displays the first few lines of a file |
| ispell | Interactive spell checker |
| lpr | Spools print jobs |
| man | Displays manual pages for commands |
| nslookup | Looks up DNS information of a host |
| passwd | Changes the password of a user |
| telnet | Telnet client allows remote logins |
| wall | Sends a message to the terminals of all users currently logged on |
| wc | Counts words, lines and characters of input text |
| which | Displays the full path of commands |
| who | Displays the list of users currently logged on to the system |

### System Configuration Files Found in the /etc Directory

The next batch of files are system configuration files, located in the `/etc` directory and its subdirectories. This table contains some of the more commonly modified ones:

| File | Description |
| :--- | :--- |
| exports | Lists the file systems to be exported via NFS |
| ftpaccess | Configuration file for ftpd |
| group | Lists the various groups on the system and each of their members |
| hosts | Lists the hostname and IP addresses of machines |
| host.conf | Used by the DNS resolver library |
| motd | Contains the message of the day |
| passwd | Contains user information for all users on the system |
| shadow | Contains the encrypted passwords of the user |
| xinetd.conf | Configuration file for the xinetd daemon |

### Administrative Binaries Found in the /sbin and /usr/sbin Directories

Administrative binaries can be found under /sbin and /usr/sbin. Below is a list of commands from the /sbin directory.

| Binary | Description |
| :--- | :--- |
| arp | Prints the ARP (Address Resolution protocol) table of a machine. |
| cardmgr | PCMCIA device manager |
| chkconfig | Manages runlevel information for system services |
| debugfs | Ext2 File system debugging utility |
| dhclient | DHCP client |
| e2fsck | Ext file system diagnosis and repair tool |
| fdisk | Disk partitioning utility |
| fuser | Displays the ids of processes using the specified files |
| ifconfig | Configures network interfaces |
| insmod | Installs loadable kernel modules |
| lspci | Lists all PCI devices on this systems |
| lsnpp | Lists all PNP devices on this system |
| mkfs | Creates a new file system on a partition |
| modprobe | Detects and manages loadable modules. |
| route | Display and sets system routing table |
| sysctl | Displays or changes system parameters |

The following list contains some of the files from the `/usr/sbin` directory:

| Binary | Description |
| :--- | :--- |
| adduser | Creates a new user |
| automount | Configures mount points for autofs |
| chpasswd | Updates password file in batch mode |
| chroot | Runs command with the root set to a new root |
| gpm | Mouse-based cut and paste utility for virtual consoles |
| groupadd | Adds a new group |
| in.fingerd | Finger daemon |
| in.ftpd | FTP daemon |
| in.identd | identd daemon |
| in.telnetd | Telnet daemon |
| kudzu | Configures new hardware |
| pppd | PPP daemon |
| squid | HTTP caching server |
| tcpdump | TCP/IP diagnostics tool |
| vipw | Password file editor |
| zdump | Dumps timezone information |

### Other Important Files

The `/usr/local/bin` directory usually houses new programs as and when they are installed.

Shared libraries (that is, libraries that contain common functions used by multiple programs at the same time without multiple in-memory copies) reside in the `/lib`, `/usr/lib`, and `/usr/local/lib` directories. It is often a good idea to ensure that the `LD_LIBRARY_PATH` environment variable contains these directories. This variable is not set by default, although it can be set in the `.bashrc` file or other startup files.

The `/boot` directory contains bootable images of Linux kernels. Below is an extract from a typical listing (here, the `vmlinuz` entries are the kernel binaries):

```
$ ls /boot
boot.b
chain.b
config-2.4.18-14
config-2.4.18-17.8.0
...
vmlinuz-2.4.18-14
vmlinuz-2.4.18-17.8.0
vmlinuz-2.4.18-19.8.0
```

Transient and temporary files can be found under `/var/tmp` and `/tmp`. The `/tmp` directory is cleaned up by startup scripts after every reboot, whereas the `/var/tmp` directory is not. This behavior may dictate for some programmers the choice of using `/var/tmp` as opposed to `/tmp`.

Files related to peripherals such as devices can be found under the `/dev` directory. By convention, various peripherals such as CD-ROM drives and floppy drives are mounted under the `/mnt` directory. We shall see more on this directory in a later section.

The `/proc` directory provides a file system abstraction to the processes currently running on the system. Each process has a directory assigned to it and several files under it which contain information about the process. For more details you should refer to the `proc` manual page by invoking the command `man proc`.

And finally, as we first discovered in Chapter 2, the users' home directories are typically created under `/home`.
