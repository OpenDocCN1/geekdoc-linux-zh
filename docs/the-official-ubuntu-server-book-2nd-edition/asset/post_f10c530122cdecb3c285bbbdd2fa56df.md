
very well. This makes /etc very easy to back up, and it takes very little space to do so. I highly recommend that if you don’t back anything else up on your system you at least back up /etc.

- **/var**

The /var directory was designed to store files and directories that could be variable in size and change frequently. The idea is to give the administrator the ability to mount /var as its own large partition and potentially as a partition on faster disks than the rest of the system. Under /var you will find system logs, mail spools, Web server documents, and other files that could grow or change frequently. While the /bin, /sbin, and even /usr directories might be pretty consistent across servers, the /var directory could vary widely across different servers depending on what the servers do.

- **/var/log**

All system logs are stored under /var/log. As any seasoned administrator knows, logs not only vary in size, but they have a tendency to grow out of control when the system is either under load or has a problem. This is yet another reason why you might want to mount /var as a separate partition—if your logs do grow out of control (and trust me, at some point they will), you will fill up /var but won’t fill up / and crash the system.

- **/var/spool**

This directory contains subdirectories that store such information as user crontabs, printer spools, and mail spools. If you run a mail server in particular, this directory will become very important to you, as it can grow quite large if the server spools a lot of mail for delivery.

- **/var/www**

This directory won’t exist on all systems, but if you run a Web server it will be the default place for the Web server’s docroot and cgi-bin directories.

- **/home**

Here you will find the home directories for all of the users you have added to the system. If you plan on having an active set of users log in to the server, you might want to mount this as a separate partition as it could potentially grow quite large. Another advantage to separating out this directory is that if you decide to change distributions, you could install the system on the root partition and overwrite what was there but preserve all user settings here.

## /root

This is a special home directory just for the root user. It is separated off from /home, among other reasons, so that it can be available for the root user in case the system needs recovery and wasn't able to mount /home.

## /dev

This is a special directory that contains all of the device files on the system. These files include disk devices, keyboards, mice, and any other devices the system detects. On classic Linux systems these files were pretty static, but on a modern Ubuntu server device files are often created on the fly by the udev program as devices are added or modules are loaded.

## /mnt

The /mnt directory is intended to be a generic location for an administrator to mount a disk temporarily. You might, for instance, mount an NFS share here temporarily so you can copy information to or from your system. In the past a number of systems have also used /mnt for removable media, but the /media directory has been created recently for that purpose.

## /media

In the past there have been a lot of differing standards as to where to mount removable media such as floppy disks, CD-ROMs, and USB drives. Some have advocated extra root directories for this purpose, and others prefer /mnt. Ubuntu uses the /media directory for these devices so it can keep /mnt for temporary mount points for nonremovable media.

## /proc

There are a few virtual file systems under Linux, and /proc is one of the most useful ones. It is not an actual area on disk but instead exists in RAM. Under this directory you will find live system information. For instance, every process that is created on the system gets a directory under /proc that corresponds to its PID. Within that directory are a number of other files and directories that contain live information about that process. In addition to information about processes, /proc also stores virtual files related to the kernel process itself. You can query such things as the options passed to the kernel at boot (/proc/cmdline) or view settings for different kernel devices or other settings. A number of the kernel /proc files can also be used to not only read settings, but set them by writing to the corresponding file.

## /sys

The /sys directory is a virtual file system much like /proc. The files within /sys provide information about devices and drivers on your system, and the file system was created in part so that these sorts of files would no longer clutter up /proc. As with /proc, not only do many of the files within /sys provide information about parts of the system, but you can also write to various files to change settings on the fly.

## /tmp

The /tmp directory is a special directory set aside to store temporary files. Every user has permission to create files under /tmp, but any files users create are readable and writable only to their user and group (and of course root). A number of programs on the system will use /tmp to store temporary state information. In fact, this use of /tmp provides a common headache for administrators because user programs sometimes store too much information in /tmp and fill up the root partition. It’s important to use /tmp only for storage of temporary files, as this directory is wiped out every time the system boots.

## Networking

Linux networking is a topic that could fill a number of books, so I won’t attempt to document everything an administrator needs to know about networking here. Instead I will provide some basic information you will need to know to change network settings under Ubuntu.
