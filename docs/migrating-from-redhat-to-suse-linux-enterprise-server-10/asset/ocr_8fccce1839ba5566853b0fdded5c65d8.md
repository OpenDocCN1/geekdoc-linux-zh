The INIT INFO block at the beginning of the script for a service describes in which runlevel the service should start or stop and what services should run as a prerequisite:

```
### BEGIN INIT INFO
# Provides:     syslog
# Required-Start: network
# Should-Start:   earlysyslog
# Required-Stop:  network
# Default-Start:  2 3 5
# Default-Stop:
# Description:    Start the system logging daemons
### END INIT INFO
```

The INIT INFO block is used by the program insserv to determine in which runlevel subdirectories links need to be placed and what numbers need to be put after K and S.

> For details on the program insserv, enter man 8 insserv.

The entry Default-Start determines in which runlevel directories links are to be placed. The entry Required-Start determines which services have to be started before the one being considered.

After editing the INIT INFO block, enter insserv -d service (default) to create the needed links and renumber the existing ones as needed.

To remove all links for a service (disabling the service), stop the service (if it is running) by entering /etc/init.d/service stop, and then enter insserv -r service (remove).

Within the INIT INFO block, the use of certain variables is possible. These are explained and defined in /etc/insserv.conf.