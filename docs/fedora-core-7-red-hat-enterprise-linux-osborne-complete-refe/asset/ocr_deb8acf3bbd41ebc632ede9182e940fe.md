The `killproc` function shuts down the daemon. The lock file and the process ID file (`httpd.pid`) are then deleted:

```
```bash
killproc httpd
echo
rm -f /var/lock/subsys/httpd
rm -f /var/run/httpd.pid
```
```

The `daemon`, `killproc`, and `status` functions are shell scripts defined in the `functions` script, also located in the `init.d` directory. The `functions` script is executed at the beginning of each service script to activate these functions. A list of these functions is provided in Table 21-5.

```
```bash
. /etc/rc.d/init.d/functions
```
```

# ## Service Script Tags

The beginning of the service script holds tags used to configure the server. These tags, which begin with an initial `#` symbol, are used to provide runtime information about the service to your system. The tags are listed in Table 21-6, along with the service functions. You enter a tag with a preceding `#` symbol, the tag name with a colon, and then the tag arguments. For example, the `processname` tag specifies the name of the program being executed, in this example `httpd`:

```
```bash
# processname: httpd
```
```

If your script starts more than one daemon, you should have a `processname` entry for each. For example, the Samba service starts up both the `smbd` and `nmbd` daemons.

```
```bash
# processname: smbd
# processname: nmbd
```
```

The end of the tag section is indicated by an empty line. After this line, any lines beginning with a `#` are treated as comments. The `chkconfig` line lists the default runlevels

| Init Script Function | Description |
|---|---|
| `daemon [+- nicelvel] program [arguments] [&]` | Starts a daemon, if it is not already running. |
| `killproc program [signal]` | Sends a signal to the program; by default it sends a `SIGTERM`, and if the process doesn’t stop, it sends a `SIGKILL`. It will also remove any PID files, if it can. |
| `pidofproc program` | Used by another function, it determines the PID of a program. |
| `status program` | Displays status information. |

**TABLE 21-5** Init Script Functions