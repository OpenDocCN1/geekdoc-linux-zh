The kill utility sends a SIGHUP (HUP is the shortened name) signal to the named PID. This restarts your inetd server and enables it to reread the configuration files you modified. Now, your inetd configuration is complete.

After you assign the Apache directive ServerType to inetd and configure the /etc/inetd.conf and /etc/services files, the User and Group directives in the httpd.conf file have no effect. However, make sure the username you used in the /etc/inetd.conf file has access privileges both to your Web directories and to where you store the log files for the server.

I recommend that you run Apache as an inetd server only if your system has very little RAM to spare, or if you do not expect to have a high-traffic Web site.

# A port for the standalone server

The Port directive has no effect if you choose to run your Apache server as an inetd process. On the other hand, if you kept the default ServerType setting (standalone), you can use this directive to tell Apache which port address to listen to.

The default HTTP port is 80, and this should be used in typical Web sites. If you are not the root user of the system, however, and want to run the Web server, you need to use a port number greater than 1023 and lower than 65535. All ports below 1024 are considered standard reserved ports and require inetd-level (root-level) access to start a service on these ports. If you are just experimenting with Web servers on a nonroot account on a system, you can use a port higher than the mentioned range as long as it has not already been taken. If you try to use a port address that is already in use by another server, you will get an error message when you try to start the server. Also, if you use any port other than the standard HTTP port 80, you have to supply a port number along with all URL requests to the server. For example, if you set this directive as Port 8080, you need to request resources (such as a page called mypage.html) on this server as follows:

```
http://www.domain.tld:8080/mypage.html
```