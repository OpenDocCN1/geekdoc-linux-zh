**ScriptAlias** *Maps a URI to a directory or file and declares the target to be a server (CGI) script.*

```
ScriptAlias alias pathname
```

where *alias* must match part of the URI the client requested to invoke the ScriptAlias and *pathname* is the absolute pathname of the target of the alias, usually a directory. Similar to the Alias directive, this directive specifies that the target is a CGI script (page 877).

The following ScriptAlias directive from the Fedora/RHEL **httpd.conf** file maps client requests that include `/cgi-bin/` to the `/var/www/cgi-bin` directory (and indicates that these requests will be treated as CGI requests):

```
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
```

Contexts: **server config**, **virtual host**
Default: none
Fedora/RHEL: /cgi-bin/ "/var/www/cgi-bin"

**User** *Sets the UID of the processes that run the servers.*

```
User #userid | username
```

where *userid* is a UID value, preceded by a #, and *username* is the name of a local user. The processes (servers) that Apache spawns are run as the user specified by this directive.

Apache must start as **root** to listen on a privileged port. For reasons of security, Apache’s child processes (servers) run as nonprivileged users. The default UID of –1 does not map to a user under Fedora/RHEL. Instead, Fedora/RHEL’s **httpd** package creates a user named **apache** during installation and sets User to that user.

Context: **server config**
Default: #-1
Fedora/RHEL: apache

**Do not set User to root or 0**

**security** For a more secure system, do not set User to **root** or **0** (zero) and do not allow the **apache** user to have write access to the DocumentRoot directory hierarchy (except as needed for storing data), especially not to configuration files.

# ## SECURITY DIRECTIVES

**Allow** *Specifies which clients can access specified content.*

```
Allow from All | host [host ...] | env=var [env=var ...]
```

This directive, which must be written as **Allow from**, grants access to a directory hierarchy to the specified clients. The directory hierarchy is specified by the container or .htaccess file this directive appears in.