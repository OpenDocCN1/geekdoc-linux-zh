This directive is used to specify a filename for storing the primary server's PID information. This file can be used by scripts to easily determine what the PID of the primary server is. For example, if the PidFile is set as follows:

```
PidFile /usr/local/apache/var/run/httpd.pid
```

I can restart the Apache server by using the kill command as follows:

```
kill -HUP `cat /usr/local/apache/var/run/httpd.pid`
```

Whatever directory you keep this file in, make sure that only the primary server process has write access to that directory. This is a major security issue; allowing other users or processes to write to this directory potentially enables someone unauthorized to take over your primary Web server process UID, which is normally the root account.

# ScoreBoardFile path/filename

This directive is set to a filename that the primary server uses to communicate with its child server processes. This is needed for only a few OS platforms. If you have to use a ScoreBoardFile, then you may see improved speed by placing it on a RAM disk. Consult your OS manuals.

# StartServers number

This directive sets the initial number of child server processes that Apache will launch at startup. Apache can automatically adjust to load, so you don't need to change the default.

# Controlling the Apache server

Apache 1.3.x comes with a nifty shell script called apachectl, which can be used to control the server in many ways. This section discusses this script in detail. However, before you can control Apache, you must become the superuser on your system, unless you have configured Apache to run on a port above 1023.

If you properly set up the inetd configuration for httpd, you don't need to do anything to start or stop the Apache server, because inetd runs it when it receives a request for access on the HTTP port.