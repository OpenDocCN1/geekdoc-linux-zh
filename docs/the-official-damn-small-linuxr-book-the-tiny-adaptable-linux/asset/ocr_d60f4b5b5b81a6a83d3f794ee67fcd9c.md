boot: dsl nodhcp mydsl=hdal/mydsl restore=hdal secure

Another way of rebooting DSL to include software stored on your hard disk (also from descriptions in the sidebar) is if you create a persistent /opt directory on a hard disk partition. For example, if your persistent /opt directory is on the second partition of your first IDE hard drive, you could boot DSL as follows:

boot: dsl nodhcp mydsl=hdal/mydsl opt=hda2 secure

If you have a large amount of RAM on your computer, you might also consider adding the toram option to the boot prompt. This helps make your slick XAMPP server blazing fast.

# BACKING UP YOUR XAMPP SERVER

The XAMPP service offers a feature that lets you securely back up you XAMPP databases, configuration files, log files, and content (htdocs) files. To do this, you run the lamp command with the backup option as follows:

```
```text
# /opt/lampp/lampp backup mysecretpwd
Backing up databases...
Backing up configuration, log, and htdocs files...
Calculating checksums...
Building final backup file...
Backup finished.
Take care of /opt/lampp/backup/xampp-backup-12-02-07.sh
```
```

The resulting backup file (xampp-backup-??-??-??.sh) is copied to the /opt/lampp/backup directory, from which you can copy it to a backup medium. The password (shown here as mysecretpwd) is the root password for your MySQL server.

If at any point your data becomes corrupted or destroyed, you can restore the backup archive by running it as a shell script. For example, with the preceding example, you could type the following:

```
```text
# sh /opt/lampp/backup/xampp-backup-22-01-04.sh mysecretpwd
Checking integrity of files...
Restoring configuration, log and htdocs files...
Checking versions...
Installed:  XAMPP 1.6
Backup from: XAMPP 1.6
Restoring MySQL databases...
Restoring MySQL user databases...
Backup complete. Have fun!
You may need to restart XAMPP to complete the restore.
```
```