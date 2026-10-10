+   ▸ **condrestart**—The same as the *restart* parameter, except that it restarts the *httpd* server only if it’s actually running.

+   ▸ **status**—This option indicates whether the server is running; if it is, it provides the various PIDs for each instance of the server.

For example, to check on the status of your server, use the command

```
# /etc/rc.d/init.d/httpd status
```

This prints the following for me:

```
httpd (pid 15997 1791 1790 1789 1788 1787 1786 1785 1784 1781) is running...
```

This indicates that the web server is running; in fact, 10 instances of the server are currently running in this configuration.

In addition to the previous options, the *httpd* script also offers these features:

+   ▸ **help**—Prints a list of valid options to the *httpd* script (which are passed onto the server as if called from the command line).

+   ▸ **configtest**—A simple test of the server’s configuration, which reports Status *OK* if the setup is correct. You can also use *httpd*’s *-t* option to perform the same test, like this:

```
# httpd -t
```

+   ▸ **fullstatus**—Displays a verbose status report.

+   ▸ **graceful**—The same as the *restart* parameter, except that the *configtest* option is used first and open connections are not aborted.

Use the *reload* option if you’re making many changes to the various server configuration files. This saves time when you’re stopping and starting the server by having the system simply reread the configuration files.

# ## Controlling Apache with Fedora’s *service* Command

Instead of directly calling the */etc/rc.d/init.d/httpd* script, you can use Red Hat’s *service* command to start, stop, and restart Apache. The *service* command is used with the name of a service (listed under */etc/rc.d/init.d*) and an optional keyword: