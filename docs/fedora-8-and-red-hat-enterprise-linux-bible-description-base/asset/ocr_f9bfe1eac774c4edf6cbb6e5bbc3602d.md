# **Including module-specific configuration files**

The following lines cause Apache to load configuration files from the `/etc/httpd/conf.d` directory. This directory contains configuration files associated with specific modules.

```
```
#
# Load config files from the config directory "/etc/httpd/conf.d".
#
Include conf.d/*.conf
```
```

> **CROSS-REFERENCE:** The "Configuring modules and related services (\etc/httpd/conf.d/\conf\*)" section, later in this chapter, describes some of the configuration files in the `conf.d` directory that may interest you.

# **Choosing the server's user and group**

The `httpd` daemon doesn't have to run as the *root* user; the fact that it doesn't run as *root* by default makes your system more secure. By setting *User* and *Group* entries, you can have the `httpd` daemon run using the permissions associated with a different user and group:

```
```
# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.
#
# User/Group: The name (or #number) of the user/group to run httpd as.
#  . On SCO (ODT 3) use "User nouser" and "Group nogroup".
#  . On HP-UX you may not be able to use shared memory as nobody, and
#    the suggested workaround is to create a user www and use that user.
# NOTE that some kernels refuse to setgid(Group) or setuid(IPC_SET)
# when the value of (unsigned)Group is above 60000;
# don't use Group #-1 on these systems!
#
User apache
Group apache
```
```

By default, *apache* is defined as both the user and group for the server. If you change the *User* and *Group* directives, you should specify a nonprivileged entity. This minimizes the risk of damage if your site is compromised. The first daemon process that is started runs as *root*. This is necessary to bind the server to a low-numbered port and to switch to the user and group specified by the *User* and *Group* directives. All other processes run under the user ID (UID) and group ID (GID) defined by those directives.

# **Setting the main server's configuration**

The second section of the `httpd.conf` file relates to directives handled by your main server (the one defined by the *ServerName* directive). In other words, these values are used by the default server and for all virtual hosts, unless they are explicitly changed for a virtual host. To change the same directives for particular virtual hosts, add them within virtual host containers.