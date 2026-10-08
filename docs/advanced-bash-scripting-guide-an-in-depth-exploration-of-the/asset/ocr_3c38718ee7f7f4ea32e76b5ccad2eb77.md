# Advanced Bash-Scripting Guide

certain process to check if that process is running. Note that if it already exists, the script will likely hang.

Normally, applications create and check for lock files in the `/var/lock` directory. [921] A script can test for the presence of a lock file by something like the following.

```
appname=xyzzip
# Application "xyzzip" created lock file "/var/lock/xyzzip.lock"

if [ -e /var/lock/$appname.lock ];
then
    # Prevent other programs & scripts
    # from accessing files/resources used by xyzip.
```

Much less useful than the lockfile command is ** flock**. It sets an "advisory" lock on a file and then executes a command while the lock is on. This is to prevent any other process from setting a lock on until completion of the specified command.

```
flock $0 > lockfile_$
# Set a lock on the script above line appears in,
#+ while waiting the script to stdout.
```

> Unlike lockfile, flock does not automatically create a lock file.

Creates or borrar device files (may be necessary when installing new hardware on the system). The MAKEDEV utility has all of the functionality of **mknod**, and is easy to use.

# MAKEDEV

Utility for creating device files. It must be run as *root*, and in the /dev directory. It is a sort of advanced version of **mknod**.

# tmpwatch

Automatically deletes files which have not been accessed within a specified period of time. Usually invoked by **cron** to remove log files.

# Backup

**dump, restore**
The **dump** command is an elaborate backup utility, generally used on larger installations and networks. [92] It reads raw disk partitions and writes a backup file in a binary format. Files to be backed up may save to a variety of storage media, including disks and tape drives. The **restore** command restores backups with **dump**.

# fdformat

Perform a low-level format on a floppy disk (/dev/fd0*).

# System Resources

# ulimit

Sets an upper limit on use of system resources. Usually invoked with the **-f** option, which sets a limit on file size (**ulimit -f 1000** files to 1 meg maximum). [94] The **-t** option limits the coredump size (**ulimit -c** eliminates coredumps). The value of ulimit would be set in **/etc/profile** and ~/.bash_profile** (see Appendix H).

Chapter 17. System and Administrative Commands

344