it could potentially grow quite large. Another advantage to separating out this directory is that if you decide to change distributions, you could install the system on the root partition and overwrite what was there but preserve all user settings here.

# /root

This is a special home directory just for the root user. It is separated off from /home, among other reasons, so that it can be available for the root user in case the system needs recovery and wasn't able to mount /home.

# /dev

This is a special directory that contains all of the device files on the system. These files include disk devices, keyboards, mice, and any other devices the system detects. On classic Linux systems these files were pretty static, but on a modern Ubuntu server device files are often created on the fly by the udev program as devices are added or modules are loaded.

# /mnt

The /mnt directory is intended to be a generic location for an administrator to mount a disk temporarily. You might, for instance, mount an NFS share here temporarily so you can copy information to or from your system. In the past a number of systems have also used /mnt for removable media, but the /media directory has been created recently for that purpose.

# /media

In the past there have been a lot of differing standards as to where to mount removable media such as floppy disks, CD-ROMs, and USB drives. Some have advocated extra root directories for this purpose, and others prefer /mnt. Ubuntu uses the /media directory for these devices so it can keep /mnt for temporary mount points for nonremovable media.

# /proc

There are a few virtual file systems under Linux, and /proc is one of the most useful ones. It is not an actual area on disk but instead exists