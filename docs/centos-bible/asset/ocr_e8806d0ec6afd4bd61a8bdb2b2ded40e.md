a backed-up file. Mike Rubel has an excellent procedure for doing rsysn snapshots at www.mikerubel.org/computers/rsync_snapshots, entitled "Fast Automated Snapshot-Style Backups with Linux and Rsync."

Another useful feature is the limit option, which can prevent rsync commands from consuming too much of the available network bandwidth. For example, limit-100 would limit the maximum transfer rate to 100 KB/s (kilobytes per second).

# ## Choosing Backup Tools

While the rsync command is one of the best choices for doing backups, it is by no means the only tool available. Many Linux systems administrators use a variety of commands for doing backups, often writing scripts to combine commands to work together. They might group together files in a single archive using tar or cpio, compress files to backup using bzip2 or gzip, or write whole directory structures of files using mkisofs.

Descriptions of backup tools in this chapter focus on those that are particularly designed for backups. The dump and restore commands are traditional UNIX commands for backing up and restoring files. The mkisofs and cdrecord commands can combine to gather a file system into an ISO image and copy that image to CD or DVD. As for networked backup features, the Amanda facility is described later in this chapter. The pax facility provides a means of creating cpio and tar archives.

If the tools for backing up files described in this chapter are not exactly what you are looking for, there are many Open Source backup facilities that you can add to your CentOS system. Here are a few examples.

+   * **Bacula** (www.bacula.org) — Bacula is a tool for managing network backups. It includes features to make it easy to recover files that have been lost or damaged. Support for backup media includes tape, CD, and hard-disk media.

+   * **Mondo Rescue** (www.mondorescue.org) — Mondo supports backups from LVM, RAID, ext2, ext3, JFS, XFS, Reiserfs, and VFAT file systems. Backups can be done to CD-R, CD-RW, NFS, or hard disk.

+   * **BackupPC** (http://backuppc.sourceforge.net) — BackupPC is useful for backing up both Linux and Windows systems over a network. Using BackupPC, you can extract backups using Samba, tar (over ssh, rs, or nfs), or rsync.

# ## Selecting a Backup Strategy

While it is tempting to do the quick-and-easy backup, backing up important data requires more planning and forethought. There are several approaches you can take to backing up your data.