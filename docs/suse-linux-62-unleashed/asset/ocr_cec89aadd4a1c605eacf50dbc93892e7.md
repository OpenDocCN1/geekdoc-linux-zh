# SUSE System Administration
Part III

"just files," you could use cat to store data on the tape, but this is not very flexible. A great many programs are particularly or designed with tape drives in mind:

+   - tar This is widely used for creating archives in regular files but was originally created for making tape backups. For fact, tar stands for tape archiver. Archives made by tar can be read on a wide variety of systems.

+   - cpio Another program principally intended for backups and so on, cpio stands for copy-in-out. The GNU version of cpio, which is used by Linux distributions, supports every different data formats—some of which are its "native" format, that are varieties of tar archives, and are obsolete. If you want to unpack an unknown archive, cpio, along with file and dd, is very useful.

+   - dump The dump utility is of use to system administrators because it backs up an ext2 filesystem by raw access to the block device on which the filesystem exists. (For reason, it is better to do this when the filesystem is neither mounted or is read-only.) This has the advantage, among other things, the access times of the backed-up directories are left unmodified. (GNU tar will also do this.) Although tapes written with dump are not always readable on other versions of UNIX, unlike those written with tar and cpio, dump is a popular choice.

+   - dd Designed for blockwise I/O, dd is a general-purpose tool for doing file manipulations and can often be useful.

+   - afio A variant of cpio, afio compresses individual files into the backup. For backups, this is preferable to tar's compression of the whole archive because a small tape error can make a compressed tar archive useless, although a tar archive that is compressed doesn't have this vulnerability. afio isn't widely used outside the Linux world.

+   - Amanda is a powerful backup system that schedules, organizes, and executes backups for you. It uses either tar or dump to do the actual work and effortlessly allow you to automate all the backups for one machine or a multiple. One of its most useful features is its ability to perform fast backups across the network from several client machines to a single server machine containing a tape drive. More information about Amanda is available at http://www.umd.md/projects/amanda.

+   - BRBRU (Backup and Restore Utility) is a commercial product for making backups.