If you want the most recent, experimental version of Apache for testing, check Red Hat's Rawhide distribution, which is also available on the Fedora FTP server (http://download.fedorahat.com/pub/fedora/linux/core/development/). This distribution is experimental and always contains the latest versions of all RPMs. However, note that the Apache package might depend on new functionality available in other RPMs. Therefore, you might need to install many new RPMs to be able to use packages from Rawhide. If you still want to use an Apache version from the Rawhide distribution for testing, a better option might be to download the source code RPM (SRPM) and compile it yourself. That way, you avoid dependencies on other new packages.

> **CAUTION**
> 
> You should be wary of installing experimental packages, and never install them on production servers (that is, servers used in “real life”). Very carefully test the packages beforehand on a host that isn’t connected to a network!

After you have obtained an Apache RPM, you can install it with the command-line rpm tool by typing the following:

```
`rpm -Uvh latest_apache.rpm`
```

where `latest_apache.rpm` is the name of the latest Apache RPM.

The Apache RPM installs files in the following directories:

+   > `/etc/httpd/conf/`—This directory contains the Apache configuration file, httpd.conf. See the section “Configuring Apache for Peak Performance” later in this chapter for more information.
+   > `/etc/rc.d/`—The tree under this directory contains the system startup scripts. The Apache RPM installs a startup script named `httpd` for the web server under the `/etc/rc.d/init.d` directory. This script, which you can use to start and stop the server from the command line, also automatically starts and stops the server when the computer is halted, started, or rebooted.
+   > `/var/www/`—The RPM installs the default server icons, Common Gateway Interface (CGI) programs, and HTML files in this location. If you want to keep web content elsewhere, you can do so by making the appropriate changes in the server configuration files.
+   > `/var/www/manual/`—If you’ve installed the `apache-manual` RPM, you’ll find a copy of the Apache documentation in HTML format here. You can access it with a web browser by going to http://localhost/manual/.
+   > `/usr/share/man/`—Fedora’s Apache RPM also contains man pages, which are placed underneath this directory. For example, the `httpd` man page is in section 8 of the man directory.