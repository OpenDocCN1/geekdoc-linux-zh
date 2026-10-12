Of course, if a system has multiple Ethernet interfaces and you want to use a main server for each interface, you don’t need to use IP aliases.

+   - The IP addresses must have host names associated with them. For the above configuration files, `192.168.1.100` is associated with `prod.domain.com` and `192.168.101` is associated with `stage.domain.com`.

A system that has such IP addresses bound to its interface(s) can now run two main Apache daemons by using the following commands:

```
/usr/local/apache/bin/httpd -f conf/httpd-100.conf
/usr/local/apache/bin/httpd -f conf/httpd-101.conf
```

If you run the `ps auxww | grep httpd | grep root | grep conf` command you will see two main Apache servers running as the root user.

# Authenticating and Authorizing Users

The mod_auth module is Apache’s default authentication module. This module allows you to authenticate users whose credentials are stored in text files, typically with a text field containing a username and encrypted password. You can also use a text file to create user groups, which can be used to create authorization rules.

![](bbox=[0.07, 0.78, 0.17, 0.87])

> I recommend that you use mod_auth-based authentication for small numbers of users only, say for a few hundred users or so. My personal experience shows that when a text file reaches even a low few thousands (1K3K) usernames, lookup performance goes down dramatically. Therefore, if you have a very large user base, I do not recommend this module.

This module is compiled into Apache by default. You can use `/usr/local/apache/bin/httpd -l` to verify if this module is already compiled into your Apache binary. If not, you have to use the `--enable-module=auth` option with the configure script and recompile and install