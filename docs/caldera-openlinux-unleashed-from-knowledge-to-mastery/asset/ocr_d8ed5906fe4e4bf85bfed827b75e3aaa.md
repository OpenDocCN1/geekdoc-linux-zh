OpenLinux ships with a version of Apache, but its version is likely to be several versions old due to Apache's rapid release schedule. You can obtain the latest version OpenLinux maintains from `ftp://ftp.calderasystems.com/pub/OpenLinux/updates/2.2/`current/RPMS`.

You can also obtain Apache as an RPM file from `http://rurus.w3.org/linux/RPM/`, or you can get the very latest source from the Apache Web site and, in true Linux tradition, build it for yourself.

This chapter covers the Apache version in OpenLinux: version 1.3.4.

# # Server Installation

You probably already have the Apache server on your computer, if you went through the standard installation. If not, you can install Apache with RPM or by building the source code yourself. You can install the RPM with the command-line *rpm* tool, by typing the following:

```
rpm -Uvh apache-VERSION.rpm
```

where VERSION is the Apache version number (for example, `apache-1.3.4-4.rpm`).

The Apache RPM installs files in the following directories:

+   *   `/etc/httpd/apache/conf/` This directory contains all the Apache configuration files, which include `access.conf`, `httpd.conf`, and `srm.conf`. See the section on configuration files later in this chapter.
+   
+   *   `/etc/rc.d/` The tree under this directory contains the system startup scripts. The Apache RPM installs a complete set for the Web server. These scripts, which you can use to start and stop the server from the command line, will also automatically start and stop the server when the workstation is halted, started, or rebooted.
+   
+   *   `/home/httpd/` (from *rpm*) *rpm* installs the default server icons (`/home/httpd/apache/icons/`), CGI programs (`/home/httpd/cgi-bin/`), HTML files (`/home/httpd/html/`), HTML manual (`/home/httpd/apache/doc/manual/`), and support binaries (`/home/httpd/bin/`) in this location. If you want to keep Web content elsewhere, you can do so by making the appropriate changes in the server configuration files.
+   
+   *   `/usr/doc/` and `/usr/man/` *rpm* contains manual pages and readme files, which are placed in these directories. As is the case for most RPM packages, the readme file and other related documentation are placed in a directory under `/usr/doc`, which is named for the Apache server version.

![](bbox=[0.86, 0.5, 0.95, 0.65])