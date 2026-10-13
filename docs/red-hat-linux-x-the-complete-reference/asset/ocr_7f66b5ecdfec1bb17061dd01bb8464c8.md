# Tux

Tux, the Red Hat Content Accelerator, is a static-content Web server designed to be run very fast from within the Linux kernel. In effect, it runs in kernel space, making response times much faster than standard user-space Web servers like Apache. As a kernel-space server, Tux can handle static content such as images very efficiently. At the same time, it can coordinate with a user-space Web server, like Apache, to provide the dynamic content, like CGI programs. Tux can even make use of a cache to hold previously generated dynamic content, using it as if it were static. The ability to coordinate with a user-space Web server lets you use Tux as your primary Web server. Anything that Tux cannot handle, it will pass off to the user-space Web server.

> Note Tux is freely distributed under the GNU Public License and is included with many distributions.

The Tux configuration file is located in `/proc/sys/net/tux`. Here you enter parameters such as **serverport**, **max_doc_size**, and **logfile** (check the Tux reference manual at [www.redhat.com/support/manuals](http://www.redhat.com/support/manuals) for a detailed listing). Defaults are already entered. **serverport**, **clientport**, and **documentroot** are required parameters that must be set. **serverport** is the port Tux will use-80 if it is the primary Web server. **clientport** is the port used by the user-space Web server Tux coordinates with, like Apache. **documentroot** specifies the root directory for your Web documents (`/var/www/html` on Red Hat).

Ideally, Tux is run as the primary Web server and Apache as the secondary Web server. To configure Apache to run with Tux, the port entry in the Apache `httpd.conf` file needs to be changed from 80 to 8080:

```
Port 8080
```

You can start, stop, and restart the server with the **service** command and the `/etc/rc.d/init.d/tux` script. Several parameters like `DOCROOT` can be specified as arguments to this Tux command. You can enter them in the `/etc/sysconfig/tux` file.

> Note You can also run Tux as an FTP server. In the `/proc/sys/net/tux` directory, you change the contents of the file **serverport** to 21, **application_protocol** to 1, and **nongle** to 0, and then restart Tux. Use the **generatetuxlist** command in the document root directory to generate FTP directory listings.