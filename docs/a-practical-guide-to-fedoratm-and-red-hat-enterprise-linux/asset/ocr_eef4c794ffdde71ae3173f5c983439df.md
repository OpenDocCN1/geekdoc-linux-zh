# FILESYSTEM LAYOUT

This section lists the locations and uses of files you can work with to configure Apache and serve Web pages.

The Apache server and related binary files are kept in several directories:

+   - `/usr/sbin/httpd`—The Apache server (daemon).

+   - `/usr/sbin/apachectl`—Starts and stops Apache.

+   - `/usr/bin/htpasswd`—Creates and maintains the password files used by the Apache authentication module (page 972).

+   - `/usr/sbin/rotatelogs`—Rotates Apache log files so that these files do not get too large. See logrotate (page 618) for more information.

+   - `/etc/htpd/modules`—Holds module binaries. Two of the most frequently used module binary files are mod\_perl.so (mod\_perl package) and mod\_wsgi.so (mod\_wsgi package). This directory is a symbolic link to `/usr/lib64/htpd/modules` (page 968).

By default, /etc/htpd is the ServerRoot (page 955); all Apache configuration files are kept in this directory hierarchy, specifically in the /etc/htpd/conf and /etc/htpd/conf.d directories:

+   - `/etc/htpd/conf/httpd.conf`—Holds configuration directives. This file is the main Apache configuration file. The discussion of configuration directives starts on the next page.

+   - `/etc/htpd/conf/magic`—Provides MIME (page 1261) file type identification (the MIME hints file). It is not normally changed. See magic number (page 1259) for more information.

+   - `/etc/htpd/conf.d`—Holds configuration files.

+   - `/etc/pki/tls/certs`—Holds files and directories used by mod\_ssl (page 970).

Log files are kept in /var/log/htpd (there is a symbolic link to /etc/htpd/logs):

+   - `/var/log/htpd/access_log`—Logs requests made to the server.

+   - `/var/log/htpd/error_log`—Logs request and runtime server errors.

+   - `/var/log/htpd/ssl\_\*_log`—Holds mod\_ssl logs.

Web documents (including the Web pages displayed by client browsers), custom error messages, and CGI scripts are kept in /var/www by default:

+   - `/usr/share/htpd/error`—Holds error documents in several languages. By default, Fedora/RHEL displays hardcoded error messages. See ErrorDocument (page 953).

+   - `/usr/share/htpd/icons`—Holds icons used to display directory entries. This directory is aliased to /icons in the autoindex.conf file.