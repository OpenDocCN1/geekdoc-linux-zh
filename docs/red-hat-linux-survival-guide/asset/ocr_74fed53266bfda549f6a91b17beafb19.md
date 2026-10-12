4. Restart sendmail using the `/etc/rc.d/init.d/sendmail restart` command.

Now sendmail will listen to your non-loopback network interface as well as the loopback interface.

# Starting and stopping sendmail

Although you have not yet configured the sendmail server, you can still run it. To start sendmail manually, you can run the following command:

```
/usr/sbin/sendmail -qqueue_processing_interval
```

You have to replace the queue_processing_interval with a time. Typically, the time is specified in minutes or hours. For example, to have sendmail process the mail queue every 15 minutes, you can use -q15m; or, as another example, to process the queue every hour you could use -q1h. You can also specify seconds (s), days (d), or weeks (w). For example, you can specify -q1h30m so that sendmail processes the query every hour and a half.

![](bbox=[0.1, 0.72, 0.18, 0.82])

> If you do not have a full-time Internet connection, you may use /usr/sbin/sendmail -bd -o DeliveryMode=d to start sendmail in deferred mode, which avoids the use of DNS until it is run again via /usr/sbin/sendmail -q. If you connect periodically, you can put /usr/sbin/sendmail -q in a cron job so that when your connection is up, the queue is processed automatically.

If you want sendmail to start automatically after each boot, make sure you create a symbolic link (starting with Sxx where xx is a number) from your default run level directory to the /etc/rc.d/init.d/sendmail script. For example, to run sendmail after each boot for a multiuser system (run level 3), I can create the following symbolic link:

```
ln -s /etc/rc.d/init.d/sendmail /etc/rc.d/rc3.d/S85sendmail
```

This symbolic link ensures that sendmail starts automatically after each boot. If you take a look at this script, you will see that sendmail is started with the -bd option, which starts it as a daemon, a background process. You may wish to modify the /etc/rc.d/init.d/sendmail script to reflect the queue interval requirements for your site. You might