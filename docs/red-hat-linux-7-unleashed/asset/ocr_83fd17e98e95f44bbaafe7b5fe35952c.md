# Caution

> You should be wary of installing experimental packages, especially on servers that are used in "real life." Very carefully test the packages beforehand!

After you have obtained an Apache RPM, you can install it with the command-line rpm tool by typing the following:

```
rpm -Uvh latest_apache.rpm
```

where *latest_apache.rpm* is the name of the latest Apache RPM.

For more information on installing packages with RPM, see Chapter 21, "Linux System Administration."

The Apache RPM installs files in the following directories:

+   * `/etc/httpd/conf`\u2014This directory contains all the Apache configuration files, which include *access.conf*, *httpd.conf*, and *srm.conf*. See the section on configuration files later in this chapter.
+   * `/etc/rc.d/`\u2014The tree under this directory contains the system startup scripts. The Apache RPM installs a complete set for the Web server. These scripts, which you can use to start and stop the server from the command line, will also automatically start and stop the server when the computer is halted, started, or rebooted. See Chapter 9, "System Startup and Shutdown," for information about these startup scripts.
+   * `/var/www`\u2014The RPM installs the default server icons, CGI programs, and HTML files in this location. If you want to keep Web content elsewhere, you can do so by making the appropriate changes in the server configuration files.
+   * `/var/www/html/manual/`\u2014If you have installed the Apache manual RPM, you will find a copy of the Apache documentation in HTML format here. You can access it with a Web browser by going to `http://localhost/manual/`.
+   * `/usr/share/man`\u2014The RPM contains manual pages, which are placed in this directory.
+   * `/usr/sbin/`\u2014The executable programs are placed in this directory. This includes the server executable itself, as well as various utilities.
+   * `/usr/bin/`\u2014Some of the utilities from the Apache package are placed here\u2014for example, the *htpasswd* program, which is used for generating authentication password files.