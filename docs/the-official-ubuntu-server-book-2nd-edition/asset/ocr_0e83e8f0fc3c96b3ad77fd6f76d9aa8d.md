# rsync Tweaks

While most of the default rsync options should be fine for the average user, there are a few extra options you might want to enable depending on your environment.

# Checksum Seed

If your host is relatively new, it should have a version of rsync greater than or equal to 2.6.3 (if you aren’t sure what version you have, type rsync --version). If so, you can take advantage of the --checksum-seed option, which can cache rsync’s checksums and overall speed up the rsync process. To do this you need to add that option to the RsyncArgs and RsyncRestoreArgs option in your BackupPC configuration.

To add this setting from the Web, click Web Config in the sidebar, then the Xfer link. Then scroll down to the RsyncArgs option where you can see each individual option on its own line. At the end of these options is an Add button. Click that and add --checksum-seed=32761. Then scroll down and add the same option to the RsyncRestoreArgs section.

To make the same change on the command line, open /etc/backuppc/config.pl in a text editor and find the line with $Conf(RsyncArgs). Each rsync option is on its own line, but if you are still using the config.pl that came with the package, you will see this option commented out:

```
#' --checksum-seed=32761' ,
```

Just remove the # from the beginning of that option. If you don’t see the commented-out option, just add a line below the last RsyncArgs option that reads

```
' --checksum-seed=32761' ,
```

Then move down to the RsyncRestoreArgs section (generally it’s the next option) and do the same thing for this option.

# One File System

By default, BackupPC traverses all of the file systems on the host and backs up absolutely everything. There are circumstances when you might not want that to be the default behavior, especially in a cluster when you can easily replace the main system files by rebuilding the