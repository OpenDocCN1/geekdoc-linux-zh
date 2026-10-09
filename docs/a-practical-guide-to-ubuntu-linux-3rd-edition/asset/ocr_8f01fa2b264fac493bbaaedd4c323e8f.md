**MultiViews**—Allows MultiViews (page 936).

**SymlinkScanOwnerMatch**—The same as FollowSymlinks but follows the link only if the file or directory being pointed to has the same owner as the link.

The following Options directive from the Ubuntu `sites-available/default` file sets the Indexes, FollowSymlinks, and MultiViews options and, because the <Directory> container specifies the `/var/www` directory hierarchy (the document root), affects all content:

```
<Directory /var/www/>
    Options Indexes FollowSymlinks MultiViews
...
```

+   Context: directory
+   Specify in `httpd.conf` or `sites-available/*`
+   Default: All
+   Ubuntu: various

**ScriptAlias** Maps a URL to a directory or file and declares the target to be a server (CGI) script.

```
ScriptAlias *alias pathname*
```

where *alias* must match part of the URL the client requested to invoke the ScriptAlias. The *pathname* is the absolute pathname of the target of the alias, usually a directory. Similar to the Alias directive, this directive specifies the target is a CGI script (page 942).

The following ScriptAlias directive from the Ubuntu default file maps client requests that include `/cgi-bin/` to the `/var/lib/cgi-bin` directory (and indicates that these requests will be treated as CGI requests):

```
ScriptAlias /cgi-bin/ "/usr/lib/cgi-bin/"
```

+   Contexts: server config, virtual host
+   Specify in `sites-available/*`
+   Default: none
+   Ubuntu: `/cgi-bin/` `/usr/lib/cgi-bin/`

**User** Sets the UID of the processes that run the servers.

```
User *userid* \| *username*
```

where *userid* is a UID value, preceded by #, and *username* is the name of a local user. The processes that Apache spawns are run as the user specified by this directive.

# **Do not set User to root or 0**

For a more secure system, do not set User to *root* or 0 (zero) and do not allow the **www-data** user to have write access to the DocumentRoot directory hierarchy (*except* as needed for storing data), especially not to configuration files.