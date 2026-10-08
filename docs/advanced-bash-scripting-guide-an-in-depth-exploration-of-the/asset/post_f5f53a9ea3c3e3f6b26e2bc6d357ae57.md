
# Advanced Bash-Scripting Guide

certain process to check if that process is running. Note that if it already exists, the script will likely hang.

Normally, applications create and check for lock files in the `/var/lock` directory. A script can test for the presence of a lock file by something like the following.

```
appname=xyzzip
# Application "xyzzip" created lock file "/var/lock/xyzzip.lock"

if [ -e /var/lock/$appname.lock ];
then
    # Prevent other programs & scripts
    # from accessing files/resources used by xyzzip.
```

Much less useful than the lockfile command is **flock**. It sets an "advisory" lock on a file and then executes a command while the lock is on. This is to prevent any other process from setting a lock on until completion of the specified command.

```
flock $0 > lockfile_$
# Set a lock on the script above line appears in,
# while waiting the script to stdout.
```

> Unlike lockfile, flock does not automatically create a lock file.

Creates or deletes device files (may be necessary when installing new hardware on the system). The MAKEDEV utility has all of the functionality of **mknod**, and is easy to use.

# MAKEDEV

Utility for creating device files. It must be run as *root*, and in the /dev directory. It is a sort of advanced version of **mknod**.

# tmpwatch

Automatically deletes files which have not been accessed within a specified period of time. Usually invoked by **cron** to remove log files.

# Backup

**dump, restore**
The **dump** command is an elaborate backup utility, generally used on larger installations and networks. It reads raw disk partitions and writes a backup file in a binary format. Files to be backed up may save to a variety of storage media, including disks and tape drives. The **restore** command restores backups with **dump**.

# fdformat

Perform a low-level format on a floppy disk (/dev/fd0*).

# System Resources

# ulimit

Sets an upper limit on use of system resources. Usually invoked with the **-f** option, which sets a limit on file size (**ulimit -f 1000** files to 1 meg maximum). The **-t** option limits the coredump size (**ulimit -c** eliminates coredumps). The value of ulimit would be set in **/etc/profile** and ~/.bash_profile (see Appendix H).

Chapter 17. System and Administrative Commands

# Advanced Bash-Scripting Guide

Judicious use of ulimit can protect a system from the dreaded fork bomb.

```
#!/bin/bash
# This script is for illustrative purposes only.
# Run it at your own peril - it WILL freeze your system.

while true; do
# Endless loop.
  $0 & \
    # This script invokes itself . . .
    # forks an infinite number of times \
    # until the system freezes up because all resources exhausted.
    # This is the notorious 'sorcerer's apprentice' scenario.

  exit 0
# Will not exit here, this script will never terminate.
```

A limit -XX (where XX is the user process limit) in /etc/profile would abort this script when it exceeds the preset limit.

quota

Display user or group quotas.

setquota

Set user or group disk quotas from the command-line.

umask User permissions mask. Limit the default attributes for a particular user. All files created by that user have the attributes specified by umask. The (octal) value to umask defines the permissions disabled. For example, umask 022 ensures new files will have at most 755 permissions (777 AND 022). Of course, the user may change the attributes of particular files using chmod. The usual practice is to use umask in /etc/profile and/or ~/.bash_profile (see Appendix H).

# Example 17. Using umask to hide out file from paging eyes

```
#!/bin/bash
# rot13.sh: Same as "rot13.sh" script, but writes output to "secure" file.

# Usage: ./rot13.sh filename
# or ./rot13.sh filename
# or ./rot13.sh and supply keyboard input (stdin)

umask 177 # File creation mask.
  # Files created by this script
  # will have 600 permissions.

OUTFILE=decrypted.txt # Results output to file "decrypted.txt"
  # which can only be read or written
  # by invoker of script (root).

cat "$@" | tr 'a-zA-Z' 'n-za-MN-AM' > $OUTFILE
  # Input from stdin or a file. Output redirected to file.

exit 0
```

rdev

Get info about or changes to root device, swap space, or video mode. The functionality of rdev has generally been taken over by fifo, but rdev remains useful for setting up a ram disk. This is a dangerous command, misused.

# Chapter

Chapter 17. System and Administrative Commands

# Advanced Bash-Scripting Guide

lsmod

List installed kernel modules.

| Module | Size | Used by |
|---|---|---|
| autof | 9456 | 2 (autoclean) |
| cp13 | 11376 | 0 |
| serial_cs | 5456 | 0 (unused) |
| sb | 34752 | 0 |
| uart401 | 6384 | 0 [sb] |
| sound | 58368 | 0 [cp13 sb uart401] |
| soundlow | 464 | 0 [sound] |
| soundcore | 2800 | 6 [sb sound] |
| ds | 6448 | 2 [serial_cs] |
| 182365 | 22928 | 2 |
| pcmia_core | 45984 | 0 [serial_cs ds 182365] |

> Doing a cat /proc/modules gives the same information.

# insmod

Force installation of a kernel module (use modprobe instead, when possible). Must be invoked as root.

# rmmod

Force unloading of a kernel module. Must be invoked as root.

# modprobe

Module loader that is normally invoked automatically in a startup script. Must be invoked as root.

# depmod

Creates module dependency. Usually invoked from a startup script.

# modinfo

Output information about a loadable module.

```
bash$ modinfo hid
filename: /lib/modules/2.4.20-6/kernel/drivers/hid.o
description: "USB HID"
author: "Andreas Gal, Vojtech Pavlik <vojtech@suse.cz>"
license: "GPL",
```

# Miscellaneous

# env

Runs a program or script with certain variables set (without changing the system). The [variable] lists all environmental settings. The first line of a script (the "shabang") may use env when the interpreter is unknown.

```
#! /usr/bin/perl

print "This script will run,\n"
print "even when I don't find Perl";
```

Chapter 17. System and Administrative Commands
