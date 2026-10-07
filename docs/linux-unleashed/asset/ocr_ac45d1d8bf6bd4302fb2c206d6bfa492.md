# Deleting Users

Just like adding new users, deleting users can be done with an automated script or manually. The automated script `deluser` or `userdel` asks which user you want to delete, and then removes the entry from the `/etc/passwd` file. Some scripts also clean out the spool and home directory files, if you want. You must make any deletions to the `/etc/passwd` file when logged in as root.

If you delete users manually, simply remove their entries from the `/etc/passwd` file. Then you can clean up their directories to clear disk space. You can completely delete all their files and their home directory with the following command:

```
rm -r /home/userdir
```

/home/userdir is the full pathname of the user’s home directory. Make sure there are no files you want to keep in that directory before you blow them all away!

Next, you should remove the user’s mail spool file, which is usually kept in /usr/spool/mail/username. For example, to remove the user walter’s mail file, issue the following command:

```
rm /usr/spool/mail/walter
```

The spool file is a single file, so this command cleans up the entries properly. To finish off the mail cleanup, check that the user has no entries in the mail alias files (usually /etc/aliases) or you can force all mail for that user to another login (such as root). To make any changes to the `/etc/aliases` file effective, you must run the `newaliases` command.

Finally, clean up the user’s `cron` and `at` jobs. You can display the user’s `crontab` file using the `crontab` command.

If you need to retain the user for some reason (such as file ownerships, a general access account, or accounting purposes), you can disable the login completely by placing an asterisk in the password field of the `/etc/passwd` file. That login can never be used once an asterisk is in the password field. If you need to reactivate the account, simply run the `passwd` command.

The process for manually deleting a user (or using an automated script that doesn’t clean up directories and files) is as follows:

+   1. Remove the user’s entry from `/etc/passwd` and `/etc/group`.
2. Remove the user’s mail file and any mail aliases.