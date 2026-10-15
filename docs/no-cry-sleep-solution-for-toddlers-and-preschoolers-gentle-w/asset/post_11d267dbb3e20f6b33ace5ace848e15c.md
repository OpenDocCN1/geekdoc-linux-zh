
If you want to shut down the swat server, you can use the off option. This will change the disable line in /etc/xinetd.d/swat to read "disable=yes".

```
chkconfig swat off
```

The same procedure works for other xinetd services such as the POP3 server and finger.

## Removing and Adding Services with chkconfig

If you want a service removed entirely from the entire startup and shutdown process in all runlevels, you can use the --del option. This removes all startup and shutdown links in all the runlevel directories.

```
chkconfig --del httpd
```

You can also add services to chkconfig management with the --add option. chkconfig will create startup links for the new service in the appropriate startup directories, /etc/rc.d/rcn.d. If you have previously removed all links for a service, you can restore them with the add option.

```
chkconfig --add httpd
```

## Configuring xinetd Services for Use by chkconfig

Default runlevel information should be placed in the startup scripts that are to be managed by chkconfig. Red Hat has already placed this information in the startup scripts for the services that are installed with its distribution. You can edit these scripts to change the default information if you wish. This information is entered as a line beginning with a # sign and followed by the chkconfig keyword and a colon. Then you list the default runlevels that the service should start up on, along with the start and stop priorities. The following entry lists runlevels 3 and 5 with a start priority of 85 and a stop of 15. See the section on Service Script Tags for more information:

```
# chkconfig: 35 85 15
```

So when a user turns on the httpd service with no level option specified, chkconfig will start up httpd at runlevels 3 and 5.

```
chkconfig httpd on
```

## How chkconfig Works

The chkconfig tool works by creating startup and shutdown links in the appropriate runlevel directories in the /etc/rc.d directory. For example, when chkconfig adds the httpd service at runlevel 5, it creates a link in the /etc/rc.d/rc5.d directory to the startup script httpd in the /etc/rc.d/init.d directory. When it turns off the Web service from runlevel 3, it creates a shutdown link in the /etc/rc3.d directory to use the script httpd in the /etc/rc.d/init.d directory to make sure the Web service is not started. In the following example, the user turns on the Web service (httpd) on runlevel 3, creating the
startup link in rc5.d S85httpd, and then turns off the Web service on runlevel 3, creating a shutdown link in rc3.d K15httpd.

```
chkconfig -level 5 httpd on
ls /etc/rc.d/rc5.d/httpd
/etc/rc.d/rc5.d/S85httpd
chkconfig -level 3 httpd off
ls /etc/rc.d/rc3.d/httpd
/etc/rc.d/rc3.d/K15httpd
```

## Service Scripts: /etc/init.d

Most server software using RPM Red Hat packages will automatically install the startup scripts and create the needed links in the appropriate rcN.d directories, where N is the runlevel number. Startup scripts, though, can be used for any program you may want run when your system starts up. To have such a program start automatically, you first create a startup script for it in the /etc/rc.d/init.d directory, and then create symbolic links to that script in the /etc/rc.d/rc3.d and /etc/rc.d/rc5.d directories. A shutdown link (K) should also be placed in the rc6.d directory used for runlevel 6 (reboot).

## Service Script Functions

A simplified version of the startup script httpd uses on Red Hat systems is shown in a later section. You can see the different options, listed in the /etc/rc.d/init.d/httpd example, under the case statement: start, stop, status, restart, and reload. If no option is provided (*), the script use syntax is displayed. The httpd script first executes a script to define functions used in these startup scripts. The daemon function with httpd actually executes the /usr/sbin/httpd server program.

```
echo -n "Starting httpd: "
daemon httpd
echo
touch /var/lock/subsys/httpd
```

The killproc function shuts down the daemon. The lock file and the process ID file (httpd.pid) are then deleted:

```
killproc httpd
echo
rm -f /var/lock/subsys/httpd
rm -f /var/run/httpd.pid
```

The daemon, killproc, and status functions are shell scripts defined in the functions script, also located in the inet.d directory. The functions script is executed at the beginning of each startup script to activate these functions. A list of these functions is provided in Table 20-4.

```
./etc/rc.d/init.d/functions
```
