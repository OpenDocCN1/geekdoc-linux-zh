Note that a file system cannot be unmounted when it is busy; for example, when there are open files on it, when some process has its working directory there, or when a swap file on it is in use. The offending process could even be unmount—it opens libc, and libc in its turn can open, for example, locale files.

Options for the umount command:

+   - `-v`—Print help message and exit.
+   - `-h`—Print help message and exit.
+   - `-V`—Verbose mode.
+   - `-n`—Unmount without writing in `/etc/mtab`.
+   - `-r`—In case unmounting fails, try to remount read-only.
+   - `-a`—All file systems described in `/etc/mtab` are unmounted. (With umount version 2.7 and later, the proc file system is not unmounted.)
+   - `-t fstype`—Indicate that the actions should only be taken on file systems of the specified type. More than one type can be specified in a comma-separated list. The list of file system types can be prefixed with `no` to specify the file system types on which no action should be taken.
+   - `-f`—Force unmount (in case of an unreachable NFS system). (Requires kernel 2.1.116 or later.)

# THE LOOP DEVICE

The umount command will free the loop device (if any) associated with the mount, in case it finds the option loop=... in `/etc/mtab`. Any pending loop devices can be freed using `losetup -d`, see losetup(8).

# FILES

`/etc/mtab`—Table of mounted file systems

# SEE ALSO

umount(2), mount(8), losetup(8).

# HISTORY

A umount command appeared in Version 6 AT&T UNIX.

# UPTIME

# NAME

`uptime`—Tell how long the system has been running.