
PostgreSQL uses a backup mechanism similar to MySQL's in that it provides a command-line dump tool called `pg_dump` that dumps one or more databases to the command line. In its simplest form it behaves a lot like the `mysql` dump command. To back up a database named `test`, created by your user, you could type

```
$ pg_dump test > test_backup.sql
```

The main database user for PostgreSQL is the `postgres` user, so you are more likely to do backups as that user:

```
$ sudo -u postgres pg_dump test > test_backup.sql
```

To back up all PostgreSQL databases, use the `pg_dumpall` command instead:

```
$ sudo -u postgres pg_dumpall > all_databases_backup.sql
```

Restoring PostgreSQL databases works much like MySQL except you use the `psql` tool. Here is how you would restore each of the backups I did previously:

```
$ psql test < test.sql
$ sudo -u postgres psql test < test.sql
$ sudo -u postgres psql < all_databases_backup.sql
```

## PostgreSQL Backup Cron Job

The cron job to back up PostgreSQL is very similar to the one for MySQL, except in this case there's no need to set up any `/root/my.cnf` files. You just need to create a new file called `/etc/cron.daily/postgresqlbackup` containing the following:

```
#!/bin/sh

/usr/bin/sudo -u postgres /usr/bin/pg_dumpall >
/root/all_databases_backup-`date +%A`.sql
```

Then you would make the script executable with `chmod a+x /etc/cron.daily/postgresqlbackup`. Now every night when the `cron.daily` scripts run, this script will run as well. Changing how many backups you keep is as easy as changing the `date` command within the backticks. If you wanted only one backup, you can just remove the backticks and everything between them. If you wanted to keep a month's worth of backups, for instance, just replace `%A` with `%d`, which will output the day of the month starting with 01.

## BackupPC

One of the simpler but still powerful backup programs for Ubuntu is called `BackupPC`. `BackupPC` is written in Perl and can make use of `tar` and `rsync` to back up Linux and UNIX hosts, and it can mount and back up SMB shares. Unlike many other backup programs, `BackupPC` does not necessarily back up a particular machine at the same time every day. This software was designed with networks of desktops that power off at the end of the day in mind, so as you add hosts, it probes them to see if they are up. If `BackupPC` is able to back them up during the evening backup window it will, but if it can't, it will attempt to back up the host during the day.

A nice feature of `BackupPC` is that it not only compresses files it has backed up, it also scans through all of the files daily and, where it sees duplicates, creates a hard link. Since a lot of servers tend to have the same system files, this method means that you can squeeze a lot more data on a lot less disk. `BackupPC` is packaged for Ubuntu, so you can use your package manager to install it:

```
$ sudo apt-get install backuppc
```

`BackupPC` includes a Web-based interface you can use to manage backup jobs, view logs, and restore files, so it will include the Apache packages it needs if they aren't already installed. During the install process you will be prompted to select a Web server for `BackupPC`. Unless you set up your own Web server ahead of time and know what you are doing, select `apache2` here. `BackupPC` uses Apache `htpasswd` accounts to password-protect the page, and the installer creates a `backuppc` user and outputs a random password to the screen, so be sure to jot it down. If you forget to do that or forget the password later on, you can use the `htpasswd` command against the `/etc/backuppc/htpasswd` file.
