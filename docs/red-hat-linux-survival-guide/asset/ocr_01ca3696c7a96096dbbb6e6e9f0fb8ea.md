To terminate Apache automatically when the system is being rebooted, run the following command once:

```
ln -s /etc/rc.d/init.d/httpd /etc/rc.d/rc3.d/K99httpd
```

This ensures that the httpd script is run with the stop argument when the system is shutting down.

# Stopping a standalone Apache server

To stop the Apache server, run /usr/local/apache/bin/apachectl stop command. Apache also makes it convenient for you to find the PID (process ID) of the root Web server process. The PID is written into a file assigned to the PidFile directive. This PID is for the primary httpd process. Do not attempt to kill the child processes manually—the parent process will recreate them as needed.

Another way to stop the Apache server is to run the following command:

```
kill -TERM `cat /usr/local/apache/logs/httpd.pid`
```

This command runs the kill command with the -TERM signal (i.e. -9) for the process ID returned by cat /usr/local/apache/logs/httpd.pid (i.e., cat PidFile) command.

# Restarting a standalone Apache server

To stop the Apache server, run the /usr/local/apache/bin/apachectl restart command.

You can use the kill command, as follows:

```
kill -HUP `cat /usr/local/apache/logs/httpd.pid`
```

When restarted with apachectl restart or by using the HUP signal with kill, the parent Apache process (run as the root user) kills all its children, reads the configuration file, and restarts a new generation of children as needed. This type of restart is sudden to the Web clients that were promised to be served by the then-alive child processes, so you may want to consider using graceful with apachectl instead of restart option and WINCH instead of the HUP signal with the kill command.

![](bbox=[0.08, 0.9, 0.18, 0.98])

This could take some time on a busy site.