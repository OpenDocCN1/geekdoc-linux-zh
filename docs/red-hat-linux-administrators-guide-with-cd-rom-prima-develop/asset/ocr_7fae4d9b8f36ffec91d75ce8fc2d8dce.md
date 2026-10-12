The -r flag is a removal option. Rather than manually removing the user's cron entry in the /var/spool/cron directory, root can execute the following command to wipe out joe's entire crontab file quickly and easily:

```
crontab -u joe -r
```

This is a quick way to clean up files left over by a defunct or malicious user.

The command field does not always need to include the absolute path to a unique binary command. It can, along with the binary, also have several flags working together. You can create various commands and string them together by using the pipe character (|). Here, for example, is a sample crontab line that might be used to kill any stray instances of sendmail running at a late hour:

```
0 2 * * *   kill -9 "ps aux | grep sendmail | awk '{print $2}'"
```

This cron job is run at 2 a.m. every morning and will kill any sendmail daemons it finds. The user can have the sendmail daemon start up the next morning by entering the following crontab line right below the preceding one:

```
0 6 * * *   /etc/rc.d/init.d/sendmail start
```

This statement calls upon the sendmail daemon to start up promptly at 6 A.M. and to continue for the next 20 hours until it is killed again at 2 A.M.

If you want to be verbose in the method of starting the sendmail daemon, you could also type the following, which better demonstrates the use of flags and options in a cron entry:

```
0 6 * * *   /usr/lib/sendmail -bd -qlh
```

This statement also starts up sendmail at 6 A.M. as a daemon process and queues up the mail every hour.

The syntax and use of sendmail are covered in more detail in Chapter 18, “Sounding Off on Linux.”

# Filtering Users

The cron program also provides a way to filter out those users who should be denied the use of cron files. This is a useful capability for administrators seeking to limit the amount of personalized jobs on a busy or congested system. The cron.allow and the cron.deny files specify who may or who may not use cron. In the Red Hat Linux distribution you may have to create them since they are not