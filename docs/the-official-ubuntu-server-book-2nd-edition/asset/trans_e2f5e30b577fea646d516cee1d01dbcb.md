
keeps track of the PID of the service it starts so that when it needs to stop the service, it knows the PID to kill. The convention is to keep track of these PIDs in the /var/run/ directory, and if you look there on your Ubuntu system, you will see a number of .pid files (or directories that store .pid files) that contain the PIDs for various system services.

Generally speaking, when you install a new service on your machine, not only should it set up its init script and appropriate symlinks for each runlevel, it should also typically start the service once the package installation is complete. Now those of you who come from a Red Hat background are probably accustomed to using the service and chkconfig command-line tools to manage services. I have good and bad news for Red Hat administrators. The bad news is that currently Ubuntu has not ported chkconfig to Ubuntu. The good news is that it has ported the service command and there is a discouraged but available alternative to chkconfig as well.

The service tool basically provides a shorthand way to start and stop services. Instead of typing sudo /etc/init.d/networking restart, you can type sudo service networking restart. Red Hat has a very handy tool known as chkconfig that an administrator can use to enable and disable services. On a Red Hat system if you wanted to disable the named service, for instance, you could type sudo chkconfig named off and the chkconfig script would remove all of the relevant symlinks within /etc/rc.d for you. If you wanted to enable the service, you could just type sudo chkconfig named on.

Unfortunately, Ubuntu does not yet have a chkconfig-like tool. The closest thing to it is a program known as update-rc.d. It’s important to know that this script was designed for use by packages, not by users as its syntax shows. The original intention was to make it easy for a package to create all of the symlinks it needed upon installation and remove all of the symlinks upon package removal. That having been said, there are some basic arguments to update-rc.d you can use to get similar behavior to chkconfig. To disable an init script from starting up, type sudo update-rc.d -f servicename remove, and to enable a script type sudo update-rc.d servicename defaults.

## Write Your Own Init Script

Ultimately when you administer servers, you may need to run your own custom programs at start-up. The simple way to do this is to put the script in /etc/rc.local so it is run at the end of the boot process. However, if you have a more sophisticated script that needs to both start at boot time and stop as part of system shutdown, then you will want to write a custom init script. While you could certainly wing it and write one from scratch, Ubuntu has made the process much easier for you with a cheat sheet init script called skeleton on which you can base your init script. First make a copy of the skeleton init script and name the file after your service:

```
$ sudo cp /etc/init.d/skeleton /etc/init.d/myservice
$
```

Then edit your copy of the skeleton file and replace the generic placeholders you find in the file with custom information for your service:

```
### BEGIN INIT INFO
# Provides:          skeleton
# Required-Start:    $remote_fs
# Required-Stop:     $remote_fs
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Example initscript
# Description:       This file should be used to construct
#                    scripts to be placed in /etc/init.d.
### END INIT INFO

# Author: Foo Bar <foobar@baz.org>
#
# Please remove the "Author" lines above and replace them
# with your own name if you copy and modify this script.
```

After you change the generic entries in the comments, what you change in the rest of the init script really depends on the complexity of your application. For basic applications you should concern yourself only with the series of environment variables that follow the initial set of comments:

```
PATH=/sbin:/usr/sbin:/bin:/usr/bin
DESC="Description of the service"
NAME=daemon executable name
DAEMON=/usr/sbin/$NAME
DAEMON_ARGS="--options args"
PIDFILE=/var/run/$NAME.pid
SCRIPTNAME=/etc/init.d/$NAME
```
