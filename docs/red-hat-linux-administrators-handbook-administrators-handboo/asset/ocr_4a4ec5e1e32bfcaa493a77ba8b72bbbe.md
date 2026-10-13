To halt the system after the shutdown, replace -r with -h. The -k option allows you to simulate a shutdown event without actually doing it. For example,

```
shutdown -r -k now System going down for maintenance
```

sends a fake shutdown message to all the users. The -t option allows you to specify a delay, in seconds, between the warning message and the actual shutdown event. In such a case, if you decide to abort the shutdown, use the -c option and run shutdown again to cancel it.

Note that you can use the HH:MM format to specify the time. For example,

```
shutdown -r 12:55
```

reboots the system at 12:55. You can also use +minutes to specify time. For example,

```
shutdown -r +5
```

starts the shutdown process five minutes after the warning message has been printed.

# uname

Syntax:

```
uname [-m] [-n] [-r] [-s] [-v] [-a]
```

The uname command displays information about the current system. For example,

```
uname -a
```

```
Linux picaso.nitec.com 2.0.36 #1 Tue Oct 13 22:17:11 EDT
1998 1586 unknown
```

The -m option displays the system architecture (for instance, i586). The -n option displays the host name (for instance, picaso.nitec.com). The -r option displays the release version of the OS (for instance, 2.0.36). The -s option