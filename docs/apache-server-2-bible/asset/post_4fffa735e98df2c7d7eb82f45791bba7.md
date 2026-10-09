
# AddDefaultCharset

AddDefaultCharset should be set to the character set that best suits your local needs. If you do not know which character set you should use, you can leave the default alone, find out which character set you should use, and change the default later.

## Starting and Stopping Apache

After you have customized httpd.conf, you are ready to run the server. For this section, I assume that you took my advice (that is, setting --prefix to /usr/local/apache) in the previous chapter. If you did not take my advice, then make sure that you replace all references to /usr/local/apache to whatever is appropriate in the following discussion.

### Starting Apache

Run the /usr/local/apache/bin/apachectl start command to start the Apache Web server. If apachectl complains about syntax errors, you should fix the errors in httpd.conf file and retry.

Also check the %ErrorLog% log file (that is, /usr/local/apache/logs/error_log) for error messages (if any). If you see errors in the log file, you need to fix them first. The most common errors are:

- Not running the server as the root user. You must start Apache as the root user. After Apache is started, it will spawn child processes that will use the User and Group directives-specified UID and GID. Most people are confused by this issue and try to start the server using the user account specified in the User directive.
- Apache complains about being unable to "bind" to an address. Either another process is already using the port that you have configured Apache to use, or you are running httpd as a normal user but trying to use a port below 1024 (such as the default port 80).
- Missing log file paths. Make sure that both %ErrorLog% and %CustomLog% paths exist and are not writable by anyone but the Apache server.
- Configuration typo. Anytime you change the httpd.conf configuration file, run /usr/local/apache/apachectl configtest to verify that you do not have a syntax error in the configuration file.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_80_0.png)

**Tip**

The quickest way to check whether the server is running is to try this command:

```
ps auxx | grep httpd
```

This command uses the ps utility to list all the processes that are in the process queue, and then pipes this output to the grep program. grep searches the output for lines that match the keyword **httpd**, and then displays each matching line. If you see one line with the word *root* in it, that's your primary Apache server process. Note that when the server starts, it creates a number of child processes to handle the requests. If you started Apache as the root user, the parent process continues to run as *root*, while the children change to the user as instructed in the *httpd.conf* file. If you are running Apache on Linux, you can create the script shown in Listing 3-2 and keep it in */etc/rc.d/init.d/* directory. This script allows you to automatically start and stop Apache when you reboot the system.

# Listing 3-2: The httpd script

```
#!/bin/sh
#
# httpd  This shell script starts and stops the Apache server
# It takes an argument 'start' or 'stop' to receptively start
# and stop the server process.
#
# Notes: You might have to change the path information used
# in the script to reflect your system's configuration.

APACHECTL=/usr/local/apache/bin/apachectl

[ -f $APACHECTL ] || exit 0

# See how the script was called.
case "$1" in
    start)
        # Start daemons.
        echo -n "Starting httpd: "
        $APACHECTL start
        touch /var/lock/subsys/httpd
        echo
        ;;
    stop)
        # Stop daemons.
        echo -n "Shutting down httpd: "
        $APACHECTL stop
        echo "done"
        rm -f /var/lock/subsys/httpd
        ;;
    *)
        echo "Usage: httpd {start|stop}"
        exit 1
esac
exit 0
```

> **Tip**
>
> To start Apache automatically when you boot up your system, simply run this command once:
>
> `ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/S99httpd`
>
> This command creates a special link called `S99httpd` in the `/etc/rc.d/rc3.d` (run-level 3) directory that links to `/etc/rc.d/init.d/httpd` script. When your system boots up, this script will be executed with the `start` argument and Apache will start automatically.

### Restarting Apache

To restart the Apache server run `/usr/local/apache/bin/apachectl restart` command.

You can also use the `kill` command as follows:

```
kill -HUP `cat /usr/local/apache/logs/httpd.pid`
```

When restarted with `apachectl restart` or by using the `HUP` signal with `kill`, the parent Apache process (run as root user) kills all its children, reads the configuration file, and restarts a new generation of children as needed.

> **Note**
>
> This type of restart is sudden to the Web clients that were promised service by the then-alive child processes. So, you might want to consider using `graceful` with `apachectl` instead of the `restart` option, and `WINCH` instead of `HUP` signal with the `kill` command. In both cases, the parent Apache process will advise its child processes to finish the current request and then to terminate so that it can reread the configuration file and restart a new batch of children. This might take some time on a busy site.

### Stopping Apache

You can automatically stop Apache when the system reboots, or manually stop it at any time. These two methods of stopping Apache are discussed in the following sections.

## Stopping Apache automatically

To terminate Apache automatically when the system is being rebooted, run this command once:

```
ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/K99httpd
```

This command ensures that the `httpd` script is run with the `stop` argument when the system shuts down.

## Stopping Apache server manually

To stop the Apache server, run the `/usr/local/apache/bin/apachectl stop` command.

Apache server also makes it convenient for you to find the PID of the root Web server process. The PID is written to a file assigned to the `PidFile` directive. This PID is for the primary `httpd` process. Do not attempt to kill the child processes manually one by one because the parent process will recreate them as needed. Another way to stop the Apache server is to run:

```
kill `cat /usr/local/apache/logs/httpd.pid`
```

This command runs the `kill` command with `-TERM` signal (that is, -15) for the process ID returned by the `cat /usr/local/apache/logs/httpd.pid` (that is, `cat %PidFile%`) command.

# Testing Apache

After you have started the Apache server, access it via a Web browser using the appropriate host name. For example, if you are running the Web browser on the server itself, then use `http://localhost/` to access the server. However, if you want to access the server from a remote host, use the fully qualified host name of the server. For example, to access a server called `apache.pcn1td.com`, use `http://apache.pcn1td.com`. If you set the `Port` directive to a nonstandard port (that is, to a port other than 80), then remember to include the `:port` in the URL. For example, `http://localhost:8080` will access Apache server on port 8080.

If you have not made any changes to the default `htdocs` directory, you will see a page such as the one shown in Figure 3-4. This page is shipped with the Apache distribution and needs to be replaced with your own content.

Finally, you want to make sure the log files are updated properly. To check your log files, enter the `log` directory and run the following command:

```
tail -f `path_to_access_log`
```

The `tail` part of the command is a Unix utility that enables viewing of a growing file (when the -f option is specified). Make sure that you change the `path_to_access_log` to a fully qualified path name for the access log. Now, use a Web browser to access the site; if you are already at the site, simply reload the page you currently have on the browser. You should see an entry added to the listing on the screen. Press the reload button a few more times to ensure that the access file is updated appropriately. If you see the updated records, your access log file is working. Press Ctrl+C to exit from the `tail` command session. If you do not see any new records in the file, you should check the permission settings for the log files and the directory in which they are kept.
