in Table 20-5, along with the startup functions. You enter a tag with a preceding # symbol, the tag name with a colon, and then the tag arguments. For example, the processname tag specifies the name of the program being executed, in this example httpd:

# Table 20-5: System V init Script Tags

| Init Script Tags | Description |
|---|---|
| # chkconfig: startlevellist startpriority endpriority | Required. Specifies the default start levels for this service as well as start and end priorities. |
| # description [ln]: description of service | Required. The description of the service, continued with characters. Use an initial # for any added lines. With the ln option, you can specify the language the description is written in. |
| # autoreload: true | Optional. If this line exists, the daemon checks its configuration files and reloads them automatically when they change. |
| # processname: program | Optional, multiple entries allowed. The name of the program or daemon started in the script. |
| # config: configuration-file | Optional, multiple entries allowed. Specifies a configuration file used by the server. |
| # pidfile: pid-file | Optional, multiple entries allowed. Specifies the PID file. |
| # probe: true | Optional, used in place of autoreload, processname, config, and pidfile entries to automatically probe and start the service. |

```
# processname: httpd
```

If your script starts more than one daemon, you should have a processname entry for each. For example, the Samba service starts up both the smbd and nmbd daemons.

```
# processname: nmbd
```

The end of the tag section is indicated by an empty line. After this line, any lines beginning with a # are treated as comments. The chkconfig line lists the default runlevels that the service should start up on, along with the start and stop priorities. The following entry lists runlevels 3, 4, and 5 with a start priority of 85 and a stop of 15:

```
# chkconfig: 345 85 15
```

For the description, you enter a short explanation of the service, using the \ symbol before a newline to use more than one line.

```
# description: Apache Web server
```

With config tags, you specify the configuration files the server may use. In the case of the Apache Web server, there may be three configuration files:

```
# config: /etc/httpd/conf/access.conf
# config: /etc/httpd/conf/httpd.conf
# config: /etc/httpd/conf/srm.conf
```

The pidfile entry indicates the file where the server's process ID is held.

# Service Script Example

As an example, a simplified version of the Web server startup script, /etc.rc.d/init.d/httpd, is