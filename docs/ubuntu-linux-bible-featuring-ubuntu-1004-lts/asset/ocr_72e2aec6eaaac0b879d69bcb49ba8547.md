# Part III: Ubuntu System Administrators

Once this page appears, you can scroll down the page to see additional status information about available backups, any transfer errors that occurred during backups, and other tables that show the status of the pool where backup files are archived and the extent to which existing backups have been compressed to disk space.

To start a backup, click either "Start Full Backup" to start a full (archive) backup of the system, or "Start Incr Backup" to start an incremental backup containing files that have changed since the last backup. A confirmation page appears.

Clicking "Start Full Backup" (or "Start Incr Backup") for an incremental backup queues the backup and displays a link that you can click to return to the main page for host to monitor the status of the backup.

# Restoring from Backups in BackupPC

Thanks to BackupPC's Web orientation and the fact that its backups are stored online on the backup server, restoring files from Backup backups can be done online, by any authorized user whose name is associated with that host in /etc/backuppc/hosts file. BackupPC enables you to browse through online backups, interactively select the files and directories you want to restore, and restore them in various ways.

To begin restoring files or directories, click the name of the full or incremental backup in which you are located. A screen like the one shown in Figure 28-4 appears.



Restoring files and directories in the BackupPC interface

![](bbox=[0.082, 0.595, 0.918, 0.945])