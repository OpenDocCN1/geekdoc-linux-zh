# Advanced Bash–Scripting Guide

CHange ROOT directory. Normally commands are fetched from $PATH, relative to /, default root directory. This changes the root directory to a different one (and also the working directory to). It is useful for security purposes, for instance when the administrator wishes to restrict users, such as using telneting, to a secured portion of the filesystem it is sometimes restricted by confining a user to a 'chroot jail'. Note that after a chroot, the execution path for system binaries is no longer valid.

A chroot /opt would create references to /usr/bin to be translated to /opt/usr/bin. Likewise, chroot /aaa/bbb /bin/ls would restrict future instances of ls to /aaa/bbb as the base directory, that is normally the case. An alias xx chroot/aaa/bbb is in a user's ~/.bashrc effectively restricts which portion of the filesystem she may run command "XX" on.

The chroot command is also used when running from an empty floppy (chroot to /dev/fd0), or as an option to l when recovering from a system crash. Others use installation from a different filesystem (an rmp option) or running a readonly filesystem from a CD ROM. Invoke only as root, and use with care.

![](bbox=[0.313, 0.366, 0.335, 0.381])

It may be necessary to copy system files to a chrooted directory, where the normal $PATH can no longer be relied upon.

This utility is part of the procmail package (www.procmail.org). It creates a lock file

Lock files are used in such applications as protecting system mail folders from simultaneously being changed by multiple users, indicating that a modem is being accessed, and showing that instance of Netscape is using its cache. Scripts check for the existence of a lock file created by a process to check if process is running. Note that if a script attempts to create a lock file that already exists, the script will likely hang.

Normally, applications create and check for lock files in the /var/lock directory. A script can test for the presence of a lock file by something like the following.

```
appname=xyzip
# Application "xyzip" created lock file "/var/lock/xyzip.lock"

if [ -e "/var/lock/$appname.lock ]
then
```

Creates block or character device files (may be necessary when installing new hardware on the system).

Automatically deletes files which have not been accessed within a specified period of time. Usually-

Chapter 13. System and Administrative Commands