The parentheses in the command instruct the shell to execute the commands inside them first before piping the output to the second tar command.

# TIP

You can use the following handy tar command in a script (and have it executed by a cron job) that backs up your entire system onto the tape drive (/dev/st0). The /tmp directory, /proc pseudo-filesystem, and any mounted filesystems in /mnt, as well as Squid proxy server's cache files, and the log file for the tar job are excluded from the backup; insert additional --exclude parameters for other directories to be excluded from backup:

```
```bash
tar -cvpf /dev/st0 \
-v "full system backup on `date`" \
--directory / --exclude=mnt --exclude=proc \
--exclude=var/spool/squid \
--exclude=home/root/tar.logfile . > /home/root/tar.logfile
```
```

A logical volume label with the date and time at which the tar command was executed is included in the tarball to aid with identification. (If you have many files to exclude, you can place them in a text file, one name per line, and use the -X file switch.)

tar has a built-in incremental backup option. It uses an ASCII file to keep track of files and directories that were backed up. To use this feature, do the following:

+   1. Create a full backup of the desired directory or directories using the -g option. For example,
+   
+      ```bash
+      tar -czpf /backup/home_full_backup.tgz \
+      -g /backup/home_tracking_file /home
+      ```

+   2. Create daily incremental backups using the following commands:
+   
+      ```bash
+      tar -czpf /backup/home_monday_backup.tgz \
+      -g /backup/home_tracking_file /home
+      tar -czpf /backup/home_tuesday_backup.tgz \
+      -g /backup/home_tracking_file /home
+      ```
+   
+      (and so on for other days)

Because you are using the same “tracking” file, tar is able to tell what files were previously backed up and when. Subsequent tarballs will contain only files that have been modified or created since the last backup (as recorded in the tracking file).