# 34  
CHAPTER

# # Backup Management: rsync, Amanda, and dump/restore

Backup operations have become an important part of administrative duties. Several backup tools are provided on Linux systems, including Anaconda and the traditional dump/restore tools, as well as the rsync command for making individual copies. Anaconda provides server-based backups, letting different systems on a network back up to a central server. The dump tools let you refine your backup process, detecting data changed since the last backup. Table 34-1 lists Web sites for Linux backup tools.

# ## Individual Backups: archive and rsync

You can back up and restore particular files and directories with archive tools like tar, restoring the archives later. For backups, tar is usually used with a tape device. To automatically schedule backups, you can schedule appropriate tar commands with the cron utility. The archives can be also compressed for storage savings. You can then copy the compressed archives to any medium, such as a DVD disc, a floppy, or tape. On GNOME you can use File Roller to create archives easily (Archive Manager under System Tools). The Kdat tool on KDE will back up to tapes, a front end to tar. See Chapter 10 for a discussion of compressed archives.

If you want to remote-copy a directory or files from one host to another, making a particular backup, you can use rsync, which is designed for network backups of particular directories or files, intelligently copying only those files that have been changed, rather than the contents of an entire directory. In archive mode, it can preserve the original ownership and permissions, providing corresponding users exist on the host system. The following example copies the /home/george/myproject directory to the /backup directory on the host rabbit, creating a corresponding myproject subdirectory. The -t specifies that this is a transfer. The remote host is referenced with an attached colon, rabbit:

```
rsync -t /home/george/myproject rabbit:/backup
```