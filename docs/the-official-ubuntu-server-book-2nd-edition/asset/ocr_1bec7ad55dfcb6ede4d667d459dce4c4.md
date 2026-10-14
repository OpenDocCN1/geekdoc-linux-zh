forget the password later on, you can use the `htpasswd` command against the `/etc/backuppc/htpasswd` file.

After the installer completes, open a Web browser and point it to the `/backuppc` directory on that host, so if your host was 10.1.1.7, you would point it to http://10.1.1.7/backuppc/. You will be prompted for login credentials, so use the login and password you were given during the install. Once you are logged in, you will see the default BackupPC admin page as shown in Figure 7-1.

# BackupPC Storage

As with any other backup server, BackupPC needs a lot of storage. All of the backups are ultimately stored under `/var/lib/backupc`. so if you have a separate disk (or set of disks in a RAID) for BackupPC, this is a good place to mount it. Let’s assume you have a second SCSI partition at `/dev/sdb1` that you want to use for BackupPC. First move the old directory out of the way, mount the new drive, and copy over the current `/var/lib/backuppc`

![](bbox=[0.235, 0.535, 0.87, 0.872])

**Figure 7-1** Default BackupPC Web interface