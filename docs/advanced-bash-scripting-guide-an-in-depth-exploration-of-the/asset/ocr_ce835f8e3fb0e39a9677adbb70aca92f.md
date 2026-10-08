# Advanced Bash-Scripting Guide

mkbootdisk

Creates a boot floppy which can be used to bring up the system if, for example, the MBR (master boot record) becomes corrupted. Of special interest is the ---iso option, which uses mkisofs to create a bootable ISO image for burning a CDR.

mkisofs

The mkbootdisk command is actually a Bash script, written by Erik Troan, in the /sbin directory.

chroot

Creates an ISO9660 file system for a CDR image.

Change ROOT directory. Normally commands are fetched from SPATH, relative to /, the default root directory. This changes the root directory to a different one (and also changes the working directory to there). This is useful for security purposes, when the system administrator wishes to restrict certain users, such as logging in, to a secured portion of the filesystem (this is sometimes referred to as confining a user to a 'chroot jail'). Note that after chroot, the execution path for binaries is no longer valid.

A chroot /opt would cause references to /usr/bin to be translated to /opt/usr/bin. Likewise, chroot /aaa/bbb /bin/ls would redirect future references of ls to /aaa/bbb base directory, rather than as is normal. An Alias XX in the user's ~/.bashrc effectively restricts which portion of the filesystem they may run "XX".

The chroot command is also handy when running from an empty boot floppy (chroot to /dev/fd0), or as an option to use when recovering from a crash system. Other uses include installation from a different filesystem (an rpm option) or running a readonly filesystem from a CD ROM. Invoke only as root, and use with.

> It may be necessary to copy system files to a chroot directory, the normal SPATH can no longer be relied upon.

lockfile

This utility is of the procmail package (www.procmail.org). It creates a lock file, a semaphore that controls a file, device, or resource.

| Definition: A semaphore is a flag or signal. (The usage in railroad, where a colored flag, striped or movable arm semaphore indicated whether a particular track was in use and unavailable for another train.) A UNIX process can check the semaphore to determine whether a particular resource is available/accessible. |

The lock file serves as a flag that a particular file, device, or resource is in use by a process (and is therefore "busy"). The presence of a lock file permits restricted access (or no access) to other processes.

```
lockfile /home/bozo/lockfiles/$0
# Creates a write-protected lockfile prefixed with the name of the script.
lockfile /home/bozo/lockfiles/$($*/).lock
# A safer version of the above, as pointed out by E. Choroba.
```

Lock files are used in such applications as protecting system mail folders from being changed by multiple users, indicating that a port is being accessed, and showing that an instance of Firefox is using its cache. Scripts may check for the existence of a lock file created by a

Chapter 17. System and Administrative Commands

343