
## Enabling and Disabling xinetd Services with chkconfig

Unlike system-config-services, **chkconfig** can also enable or disable **xinetd** services. Simply enter the **xinetd** service with either an **on** or **off** option. The service will be started up or shut down, and the disable line in its **xinetd** configuration script in the **/etc/xinetd.d** directory will be edited accordingly. For example, to start swat, the Samba configuration server, which runs on **xinetd**, you simply enter:

```
chkconfig swat on
chkconfig --list swat
    swat                on
```

The **swat** configuration file for **xinetd**, **/etc/xinetd.d/swat**, will have its disable line edited to no, as shown here:

```
disable=no
```

If you want to shut down the swat server, you can use the **off** option. This will change the disable line in **/etc/xinetd.d/swat** to read “disable=yes”.

```
chkconfig swat off
```

The same procedure works for other **xinetd** services such as the POP3 server and **finger**.

## Removing and Adding Services with chkconfig

If you want a service removed entirely from the entire startup and shutdown process in all runlevels, you can use the **--del** option. This removes all startup and shutdown links in all the runlevel directories.

```
chkconfig --del httpd
```

You can also add services to **chkconfig** management with the **--add** option; **chkconfig** will create startup links for the new service in the appropriate startup directories, **/etc/rc.d/rcn.d**. If you have previously removed all links for a service, you can restore them with the **add** option.

```
chkconfig --add httpd
```

## Configuring xinetd Services for Use by chkconfig

Default runlevel information should be placed in the service scripts that are to be managed by **chkconfig**. Red Hat and Fedora have already placed this information in the service scripts for the services that are installed with its distribution. You can edit these scripts to change the default information if you wish. This information is entered as a line beginning with a # sign and followed by the **chkconfig** keyword and a colon. Then you list the default runlevels that the service should start up on, along with the start and stop priorities. The following entry lists runlevels 3 and 5 with a start priority of 85 and a stop of 15. See the section “Service Script Tags” for more information:

```
# chkconfig: 35 85 15
```

Thus, when a user turns on the **httpd** service with no level option specified, **chkconfig** will start up **httpd** on runlevels 3 and 5.

```
chkconfig httpd on
```

### How chkconfig Works

The **chkconfig** tool works by creating startup and shutdown links in the appropriate runlevel directories in the `/etc/rc.d` directory. For example, when **chkconfig** adds the **httpd** service at runlevel 5, it creates a link in the `/etc/rc.d/rc5.d` directory to the service script **httpd** in the `/etc/rc.d/init.d` directory. When it turns off the Web service from runlevel 3, it creates a shutdown link in the `/etc/rc.d/rc3.d` directory to use the script **httpd** in the `/etc/rc.d/init.d` directory to make sure the Web service is not started. In the following example, the user turns on the Web service (**httpd**) on runlevel 3, creating the startup link in `rc5.d`, `S85httpd`, and then turns off the Web service on runlevel 3, creating a shutdown link in `rc3.d`, `K15httpd`.

```
chkconfig -level 5 httpd on
ls /etc/rc.d/rc5.d/*httpd
/etc/rc.d/rc5.d/S85httpd
chkconfig -level 3 httpd off
ls /etc/rc.d/rc3.d/*httpd
/etc/rc.d/rc3.d/K15httpd
```

## Service Scripts: /etc/init.d

Most software using RPM packages will automatically install any appropriate service scripts and create the needed links in the appropriate `rcn.d` directories, where `n` is the runlevel number. Service scripts, though, can be used for any program you may want run when your system starts up. To have such a program start automatically, you first create a service script for it in the `/etc/rc.d/init.d` directory and then create symbolic links to that script in the `/etc/rc.d/rc3.d` and `/etc/rc.d/rc5.d` directories. A shutdown link (`K`) should also be placed in the `rc6.d` directory used for runlevel 6 (reboot).

### Service Script Functions

A simplified version of the service script **httpd** used on Red Hat and Fedora systems is shown in a later section. You can see the different options, listed in the `/etc/rc.d/init.d/httpd` example, under the *case* statement: *start*, *stop*, *status*, *restart*, and *reload*. If no option is provided (*\**), the script usage syntax is displayed. The **httpd** script first executes a script to define functions used in these service scripts. The **daemon** function with **httpd** actually executes the `/usr/sbin/httpd` server program.

```
echo -n "Starting httpd: "
daemon httpd
echo
touch /var/lock/subsys/httpd
```

The `killproc` function shuts down the daemon. The lock file and the process ID file (`httpd.pid`) are then deleted:

```bash
killproc httpd
echo
rm -f /var/lock/subsys/httpd
rm -f /var/run/httpd.pid
```

The `daemon`, `killproc`, and `status` functions are shell scripts defined in the `functions` script, also located in the `init.d` directory. The `functions` script is executed at the beginning of each service script to activate these functions. A list of these functions is provided in Table 21-5.

```bash
. /etc/rc.d/init.d/functions
```

### Service Script Tags

The beginning of the service script holds tags used to configure the server. These tags, which begin with an initial `#` symbol, are used to provide runtime information about the service to your system. The tags are listed in Table 21-6, along with the service functions. You enter a tag with a preceding `#` symbol, the tag name with a colon, and then the tag arguments. For example, the `processname` tag specifies the name of the program being executed, in this example `httpd`:

```bash
# processname: httpd
```

If your script starts more than one daemon, you should have a `processname` entry for each. For example, the Samba service starts up both the `smbd` and `nmbd` daemons.

```bash
# processname: smbd
# processname: nmbd
```

The end of the tag section is indicated by an empty line. After this line, any lines beginning with a `#` are treated as comments. The `chkconfig` line lists the default runlevels that the service should start up on, along with the start and stop priorities. The following entry lists runlevels 3, 4, and 5 with a start priority of 85 and a stop of 15:

```
# chkconfig: 345 85 15
```

For the description, you enter a short explanation of the service, using the \ symbol before a new line to use more than one line.

```
# description: Apache Web server
```

With **config** tags, you specify the configuration files the server may use. In the case of the Apache Web server, there may be three configuration files:

```
# config: /etc/httpd/conf/access.conf
# config: /etc/httpd/conf/httpd.conf
# config: /etc/httpd/conf/srm.conf
```

The **pidfile** entry indicates the file where the server’s process ID is held.

### Service Script Example

As an example, a simplified version of the Web server service script, */etc/rc.d/init.d/httpd*, is shown here. Most scripts are much more complicated, particularly when

**Table 21-5 Init Script Functions**

| Init Script Function | Description |
|---|---|
| `daemon [+- nicelvel] program [arguments] [&]` | Starts a daemon, if it is not already running. |
| `killproc program [signal]` | Sends a signal to the program; by default it sends a `SIGTERM`, and if the process doesn’t stop, it sends a `SIGKILL`. It will also remove any PID files, if it can. |
| `pidofproc program` | Used by another function, it determines the PID of a program. |
| `status program` | Displays status information. |

**Table 21-6 Init Script Tags**

| Init Script Tags | Description |
| :--- | :--- |
| **# chkconfig:** *startlevellist startpriority endpriority* | Required. Specifies the default start levels for this service as well as start and end priorities. |
| **# description [ln]:** *description of service* | Required. The description of the service, continued with `\` characters. Use an initial # for any added lines. With the ln option, you can specify the language the description is written in. |
| **# autoreload: true** | Optional. If this line exists, the daemon checks its configuration files and reloads them automatically when they change. |
| **# processname:** *program* | Optional, multiple entries allowed. The name of the program or daemon started in the script. |
| **# config:** *configuration-file* | Optional, multiple entries allowed. Specifies a configuration file used by the server. |
| **# pidfile: pid-file** | Optional, multiple entries allowed. Specifies the PID file. |
| **# probe: true** | Optional, used in place of **autoreload**, **processname**, **config**, and **pidfile** entries to automatically probe and start the service. |
