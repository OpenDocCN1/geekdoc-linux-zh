# # Part III
## Administration

You can now back up your entire system by running the `backups.sh` script when logged in as *root*. The script accepts the dump level as its only parameter. If you leave the parameter off, it will automatically assume a Level 0 dump. Thus, the following two commands are equivalent:

```
# backups.sh
# backups.sh 0
```

You may need to customize this script for your situation. For example, I am using the tape device `/dev/nst0`. You might be using a different tape device. Whatever device you use, you should probably use the version of its device name that begins with the letter *n*. That tells the system that after it finishes copying data to the tape, it should *not* rewind the tape. For example, I used `/dev/nst0` instead of `/dev/st0` in the preceding script. If I had used `/dev/st0`, each successive incremental backup would have overwritten the previous one.

Other things that you may change in this script include the partitions being backed up and the dump level at which the tape is ejected. It is common practice to eject the tape after the last incremental backup just before performing a full backup.

The most useful thing about this script is that you can easily configure your system to run it automatically. Simply add a few lines to the root crontab file, and the *cron* daemon will invoke the script on the days and times specified. While logged in as *root*, enter the crontab command with the -e option:

```
# crontab -e
```

This opens the root crontab file in an editor. Add the following lines at the end of the file:

```
0 22 * * 0 /usr/local/bin/backup.sh 0
0 22 * * 1 /usr/local/bin/backup.sh 9
0 22 * * 2 /usr/local/bin/backup.sh 8
0 22 * * 3 /usr/local/bin/backup.sh 7
0 22 * * 4 /usr/local/bin/backup.sh 6
0 22 * * 5 /usr/local/bin/backup.sh 5
0 22 * * 6 /usr/local/bin/backup.sh 4
```

Save and exit the file. The *cron* daemon will now run the backup script at 10:00 p.m. (22:00 in military time) every day of the week. This example implements the dump schedule outlined earlier. A full dump is performed on Sunday, and the tape is ejected when it is done. A new tape should be loaded on Monday, and then incremental backups will be written to that same tape for the rest of the week. The next full dump will be written to the end of that tape, unless someone is around on Sunday to eject and replace the tape before 10:00 p.m. Keep in mind that the person set to receive e-mail for the *root* user will be the one to be notified of the actions of this, or any, *root*-owned cron script.

# # Restoring Backed-Up Files

The `restore` command is used to retrieve files from a backup tape or other medium that was created by `dump`. You can use `restore` to recover an entire file system or to interactively select individual files. It recovers files from the specified media and copies them into the current