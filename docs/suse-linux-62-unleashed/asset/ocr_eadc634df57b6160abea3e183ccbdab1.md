of every modifiable filesystem (except NFS and Samba partitions) or data may be lost.
directories /boot, /dev, and /proc have special roles, which are explained in Chapter 18,
“Managing Filesystems”.

In the early stages of the boot sequence, only the root filesystem is available, and therefore nothing outside the root partition should be necessary to start a session for the root user. This sometimes influences the choice of where to put files.

# # Essentials of /bin and /sbin

Most of the essential programs for using and maintaining Linux are stored in the /bin and
sbin directories. The bin in the names of these directories comes from the fact that executable programs are binary files.

The /bin directory holds the most commonly used essential user programs, such as the following:

+   - login
- Shells (bash, tcsh)
- File manipulation utilities (cp, mv, rm, ln, tar)
- Filesystem utilities (dd, df, mount, sync)
- System utilities (uname, hostname, arch)

In addition to these types of programs, the /bin directory also contains other GNU utilities such as gzip and gunzip.

The /sbin directory holds essential maintenance or system programs, such as the following:

+   - fsck
- fdisk
- mkfs
- shutdown
- lilo
- init

The main difference between the programs stored in /bin and /sbin is that nearly all of the programs in /sbin are executable only by root (one exception is the ifconfig command). By default, the /sbin and /usr/sbin directories are not included in normal users’ PATH.