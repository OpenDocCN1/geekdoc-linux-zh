Lastly, when executing the script, the user is given several options for checking the handling of the sendmail daemon. This particular daemon can be queried with one of four commands: *start*, *stop*, *restart*, and *status*. If you are currently within the `/etc/rc/init.d/` directory, the command `./sendmail restart` will stop and then restart the sendmail daemon. The following is an example followed by the options associated with the sendmail daemon:

```
/etc/rc.d/init.d/sendmail start | stop | restart | status
```

# TIP

The period and forward slash are required for commands located in the current directory. Sometimes, simply typing the command by itself produces an error, but placing the period and forward slash before it tells the computer that the program to be executed is located in the same directory. This applies only if the program is also not located in the user's path.

Likewise, you could give the entire path to the script, as in `/etc/rc.d/init.d/sendmail restart`, but it is sometimes easier simply to change directories into the same location and then place the two characters, a period and a forward slash, ahead of the command.

It is normally not a good idea to add the "." or single period to the PATH variable even though it makes command executions easier. This is a gaping security hole and should be avoided. Suppose I as an untrusted user make a script called "ks" in /tmp and then somehow entice root to "cd /tmp" (as I know he, the administrator, often mistypes "is" as "ks".) And supposing "ks" is a script that trashes the system. In other words, "" in the path allows untrusted executables to be accidentally executed.

# Restarting Daemons

Restarting a daemon is required any time changes have been made either to the script itself or to any variables required by the program, such as configuration files. Using sendmail again as an example, if you add any new domain to your machine's virtuser table or add a domain that has permission to relay through your machine, the sendmail daemon will need to be restarted. The daemon must reread its configuration files and then incorporate the new settings into the daemon when it is restarted.

Another method of reinitializing the daemon is to use one of the several signals to the process. The process ID number is sent a HUP signal (short for *hangup*),