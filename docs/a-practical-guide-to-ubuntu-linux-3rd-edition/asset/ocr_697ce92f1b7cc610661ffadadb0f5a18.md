# Table 26-1 Directives that you can override in **httpd.conf**

| Column 1 | Column 2 |
|---|---|
| AccessFileName | MaxRequestsPerChild |
| DefaultType | MaxSpareThreads |
| ErrorLog | MinSpareThreads |
| Group | PidFile |
| HostnameLookups | ServerRoot |
| KeepAlive | StartServers |
| KeepAliveTimeout | ThreadsPerChild |
| LockFile | Timeout |
| LogLevel | TypesConfig |
| MaxClients | User |
| MaxKeepAliveRequests |  |

Directives that control log formats, indexing options, MIME handling, and browser bug handling appear after the Include directive for **httpd.conf**, but before the Include directive for /etc/apache2/sites-enabled, which is the last line in **apache2.conf**. You can override these directives on a per-site basis by copying them to individual site files in the sites-enabled directory and modifying them there.

If you manage more than one Ubuntu Web server, it is nice to keep all the customized configuration code separate from the main configuration. That way you can use scp to copy the files to each new server. Or you can keep the custom code under a version control system and check it out to configure a new system. This technique is much easier than using diff to find out what you changed from system to system.

# FILESYSTEM LAYOUT

This section lists the locations and uses of files you will work with to configure Apache and serve Web pages.

The Apache server and related binary files are kept in several directories:

+   - **/usr/sbin/apache2**—The Apache server (daemon).

+   - **/usr/sbin/apache2ctl**—Starts and stops Apache. The apache2 init script calls apache2ctl.

+   - **/usr/bin/htpasswd**—Creates and maintains the password files used by the Apache authentication module (page 945).

+   - **/usr/sbin/rotatelogs**—Rotates Apache log files so that these files do not get too large. See logrotate (page 622) for information about rotating log files.

+   - **/etc/apache2/mods-available**—Holds files containing LoadModule directives (page 928) for their respective modules. The alias.conf file is kept in this directory