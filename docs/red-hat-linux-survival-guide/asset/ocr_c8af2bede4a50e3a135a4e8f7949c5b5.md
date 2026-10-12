# shutdown

Syntax: shutdown [-r] [-h] [-c] [-k] [-t seconds] time [message]

This command allows a superuser or an ordinary user listed in the /etc/shutdown.allow file to shut the system down for a reboot or halt. To reboot the computer now, run the following command:

```
shutdown -r now
```

To halt the system after the shutdown, replace the -r with -h. The -k option allows you to simulate a shutdown event. For example, the following command sends a fake shutdown message to all users:

```
shutdown -r -k now System going down for maintenance
```

The -t option allows you to specify a delay in seconds between the warning message and the actual shutdown event. In such a case, if you decide to abort the shutdown, run shutdown again with the -c option to cancel it.

Note that you can use the HH:MM format to specify the time. For example:

```
shutdown -r 12:55
```

This reboots the system at 12:55. You can also use +minutes to specify time. For example:

```
shutdown -r +5
```

This starts the shutdown process five minutes after you print the warning message.

# uname

Syntax: uname [-m] [-n] [-r] [-s] [-v] [-a]

This command displays information about the current system. For example:

```
uname -a
```