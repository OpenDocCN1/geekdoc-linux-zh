# # 10.4 Directory Tree and File Systems

A Linux system's directory tree usually extends over more than one partition on disk, and removable media like CD-ROM disks, USB keys as well as portable MP3 players, digital cameras and so on must be taken into account. If you know your way around Microsoft Windows, you are probably aware that this problem is solved there by means of identifying different ‘drives’ by means of letters—on Linux, all available disk partitions and media are integrated in the directory tree starting at “/”.

In general, nothing prevents you from installing a complete Linux system on a single hard disk partition. However, it is common to put at least the /home directory—where users’ home directories reside—on its own partition. The advantage of this approach is that you can re-install the actual operating system, your Linux distribution, completely from scratch without having to worry about the safety of your own data (you simply need to pay attention at the correct moment, namely when you pick the target partition(s) for the installation in your distribution’s installer.) This also simplifies the creation of backup copies.

On larger server systems it is also quite usual to assign other directories, typically /tmp, /var/tmp, or /var/spool, their own partitions. The goal is to prevent users from disturbing system operations by filling important partitions completely. For example, if /var is full, no protocol messages can be written to disk, so we want to keep users from filling up the file system with large amounts of unread mail, unprinted print jobs, or giant files in /var/tmp. On the other hand, all these partitions tend to clutter up the system.

+   ☀ More information and strategies for partitioning are presented in the Linup Front training manual, *Linux Administration I*.

The /etc/fstab file describes how the system is assembled from various disk partitions. During startup, the system arranges for the various file systems to be made available—the Linux insider says “mounted”—in the correct places, which you as a normal user do not need to worry about. What you may in fact be interested in, though, is how to access your CD-ROM disks and USB keys, and these need to be mounted, too. Hence we do well to cover this topic briefly even though it is really administrator country.

To mount a medium, you require both the name of the device file for the medium (usually a block device such as */dev/sda1*) and a directory somewhere in the directory tree where the content of the medium should appear—the so-called *mount point*. This can be any directory.

+   ☀ The directory doesn't even have to be empty, although you cannot access the original content once you have mounted another medium “over” it. (The content reappears after you unmount the medium.)

+   ⚠ In principle, somebody could mount a removable medium over an important system directory such as /etc (ideally with a file called *passwd* containing a *root* entry without a password). It is why mounting of *file systems* in arbitrary places within the directory tree is restricted to the system *administrator*, who will have no need for shenanigans like these, as they are already *root*.

+   ☀ Earlier on, we called the “device file for the medium” */dev/sda1*. This is really the first partition on the first SCSI disk drive in the system—the real name may be completely different depending on the type of medium you are using. Still it is an obvious name for USB keys, which for technical reasons are treated by the system as if they were SCSI devices.

With this information—device name and mount point—a system administrator can mount the medium as follows: