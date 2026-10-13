# ### /sbin

The /sbin directory contains system and administration utilities or binaries. Utilities for partitioning a hard drive, checking the integrity of a filesystem, creating a new filesystem, and shutting down or rebooting the system are all stored in this directory.

# ### /tmp

Temporary files are stored in this directory. Often, applications need to use temporary files with certain functions or when installing. These temporary files are stored in the /tmp directory.

# ### /usr

The /usr directory is intended for shareable, read-only data. It is the major section of the filesystem, but it can be configured to reside on a secondary machine. The majority of documentation is located in the /usr/doc directory. The complete source tree for the Linux kernel is located in the /usr/src directory.

# ### /var

The /var directory is set up to hold variable data. It contains spool directories for mail, news, print jobs, and other files, as well as other administrative files. All data logged by specific processes are stored in the /var directory.

# ### /dev/shm

Before moving on, one filesystem that mounts to the /dev directory by default (but can be mounted anywhere, including in the root directory) is the shm directory. This directory should never be used for anything. The kernel makes use of this filesystem for shared memory access. You can occasionally see a file or two written here that later disappear. The amount of shared memory available is calculated by the kernel at bootup, when the shared memory filesystem is mounted. It will be a portion of the entire virtual filesystem available to the kernel. Its size can be varied through /proc/sys/kernel/shmmax, but if you are not familiar with this filesystem, it is best to leave the value as-is.

> > **Caution**
> >
> > If you are splitting your filesystem across multiple disks or partitions, the following directories must be in the root filesystem:
> > - `/bin`, `/dev` (unless using the new devfs in lieu of `/dev`), `/etc`, `/lib`, `/root`
> > - `/tmp`, `/var` (but some subdirectories of `/var`, such as the spool/mail subdirectory, are often NFS mounted from a central mailhost)
> > - Also, some filesystems cannot be NFS-mounted (unless you are using a totally disk-less client)

You can determine what is mounted on your filesystem in one of several ways. The first way is to use df. This command shows you how much disk space is free for use on each mounted filesystem; however, not all filesystems will be shown.