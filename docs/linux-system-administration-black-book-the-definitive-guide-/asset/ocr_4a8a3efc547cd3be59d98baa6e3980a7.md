# # Setting Up Web Server Acceleration

To set up Web server acceleration, do the following:

+   1. Log in as root to the machine you installed Squid on.
+   2. Type “/vi /etc/squid/squid.conf” to open the Squid configuration file for editing.
+   3. Type “/http_port” to search down to the port setting line.
+   4. Type “i” to enter Insert mode.
+   5. Change the current port value so the line is:

```
http_port 80
```

+   6. Type “/httpd_accel” and press Enter to search down to the Web acceleration section of the Squid configuration file.
+   7. Using Squid for Web acceleration means having the cache server step in for any URL requests before the Web server gets involved. Continue down to to:

```
#httpd_accel_host hostname
#httpd_accel_port port
```

+   8. Uncomment these two lines. For the first line, change **hostname** to the name of the machine that hosts the Web server, such as this:

```
httpd_accel_host www
```

+   9. Change **port** to the port number that the Web server listens on. For example:

```
httpd_accel_port 80
```

+   10. Turning on the acceleration feature actually turns off Web proxying. If you want to use Web proxying, first go to the following line:

```
#httpd_accel_with_proxy off
```

+   11. Change this line to the following to turn Web proxying back on:

```
httpd_accel_with_proxy on
```