Aside from providing greater functionality and capabilities, most third-party backup utilities also allow you to back up Windows, Macintosh, and UNIX systems from your Windows 2000 system. This added benefit will allow you to deploy a single backup solution. Other software vendors, such as Computer Associates and Hewlett Packard, also provide effective third-party backup utilities.

# Summary

Backup and restore operations are essential parts of good system administration. Though time-consuming, if done correctly, they will certainly save time in the long run. In this chapter, we discussed the creation and implementation of a backup/restore system.

# BUILDING A BACKUP SCHEDULE

Determining what you should include in your backup strategy, and when you should back up, can be difficult. Infinite storage space (and time) would make it possible to back up everything, everyday. However, most of us have to rely on selective backups on incremental schedules. When selecting what to back up, you need to consider the following categories of data:

+   - System files.
+   - Off-the-shelf software.
+   - Replicated data.
+   - Sensitive data.

Incremental backups are necessary to balance backup needs with available storage space. Remember that a restore may require multiple volumes to perform.

# UNIX BACKUPS

The simplest backup tool in UNIX is the tar command. Though not designed for large backup routines, it is excellent for quickly creating portable archives of directories or even partitions. Each UNIX variant comes with some form of backup utility. Tables 13.8 and 13.9 list the variant-dependent backup routines. In this chapter, we focused on the cross-platform Amanda utility, a very robust and powerful multi-vendor UNIX backup system, and a project at the University of Maryland. Amanda will also support Windows platforms if you have SAMBA installed in your infrastructure.