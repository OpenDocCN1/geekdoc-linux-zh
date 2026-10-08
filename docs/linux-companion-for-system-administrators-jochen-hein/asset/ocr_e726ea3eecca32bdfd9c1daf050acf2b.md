# 2.5.3 /var/games - variable data of games (high scores)

Here, only variable data of games are stored, such as results or high-score lists. Often it is sensible to create a special group (for example games) and make this directory writable for this group. Static data, such as levels or help texts, are stored in the /usr/lib/games directory.

# 2.5.4 /var/local - variable data from /usr/local

This directory is intended to store variable data for programs installed locally by the system administrator. Since the authors of the FHS do not know which programs will be installed locally, no further subdivision of this directory is proposed. The use of this directory is the system administrator's business.

If, the files fit into a category introduced here, they should be stored in that location. This applies, for example, to lock files, which should be stored in /var/lock.

# 2.5.5 /var/lock - lock files

All lock files used for locking devices against multiple use should be created in the /var/lock directory. No lock files should be created in the /usr partition to allow this partition to be mounted-protected.

The name of a lock file begins with LCK..., followed by the name of the device to be locked. Thus, the device /dev/ttyS0, the file /var/lock/LCK..ttyS0 is used.

All lock files should be readable for every user and contain the process number of that process that is locking the device in clear text. Each program can check whether the process that created the lock still exists.

It is sensible to do without the symbolic link /dev/modem and to use the true device instead. Lock files can then be created exclusively for true devices. On the one hand, a device is not going to be addressed under two different names; on the other, for symbolic links, the semantics of the chown system call under Linux does not correspond to that of other systems.

Standardization of this directory would sensibly increase the cross-functionality between different programs whose synchronization is carried out via lock files. This is, first, because all programs create their lock files here, and, second, because the FHS specifies a standard format for the contents of these files.