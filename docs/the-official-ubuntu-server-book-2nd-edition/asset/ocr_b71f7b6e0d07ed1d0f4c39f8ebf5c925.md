tools, however, is its ability to scan your hard drives for failures and warn you before a failure actually happens.

The first step is to install the smartmontools package:

```
$ sudo apt-get install smartmontools
```

The package includes a daemon called smartd that can launch at system start-up and start monitoring your drives. By default smartd will not start, so you need to edit /etc/default/smartmontools and uncomment the line that reads

```
# start_smartd=yes
```

Now smartd will start at boot, but you will also want to start it up manually so it's available right now:

```
$ sudo /etc/init.d/smartmontools start
```

By default smartd scans through all of your drives for any that are SMART-enabled and monitors them, so you don't need to perform any special configuration at this point. When smartd detects an error, it runs any scripts it finds under /etc/smartmontools/run.d/. By default there is only one script under that directory, named 10mail, that e-mails the root user so he or she knows of the problem, but you can add any number of custom scripts to this directory as well, and they will be run in alphabetical order. When smartd finds a problem, it executes your script and passes the full path to the error file as an argument, so within your script you can access it via the $1 variable, for instance. Check the /etc/smartmontools/run.d/10mail script for a simple example on which you can base your scripts.

# sysstat

Let's face it, you probably don't have terminals logged in to every system you manage with some tool like top running. Even if you did, you still won't know your system load or RAM statistics while you are asleep. Now some administrators solve this problem by running top via a cron job, but Ubuntu has a better system in place via sysstat. The sysstat package provides a