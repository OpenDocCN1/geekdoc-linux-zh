# Listing 12-1  Continued

```
rm -f /var/lock/subsys/httpd
;
*)
echo "Usage: httpd {start|stop}"
exit 1
esac
exit 0
```

I put this script in the /etc/rc.d/init.d directory and made the following symbolic links:

+   /etc/rc.d/rc3.d/S80httpd -> /etc/rc.d/init.d/httpd.sh
+   /etc/rc.d/rc3.d/K80httpd -> /etc/rc.d/init.d/httpd.sh

When the system starts up, it loads the Apache server automatically. The script also stops the Apache server at system shutdown or reboot.

# Stopping the server

To stop the server, run the apachectl script as follows:

```
/path/to/apache/bin/apachectl stop
```

# Restarting the server

To restart the server, run the apachectl script as follows:

```
/path/to/apache/bin/apachectl restart
```

To perform a graceful restart, run the apachectl script as follows:

```
/path/to/apache/bin/apachectl graceful
```

For the curious, the restart command sends a SIGHUP signal to Apache, and the graceful command sends a SIGUSR1 signal instead. Because the latter is user-defined (by the Apache developers), it is much more agreeable to the running server.