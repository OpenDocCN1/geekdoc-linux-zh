# Access Control

tcpd controls access to services using the language described in the manual pages hosts_access(5) and hosts_options(5). tcpd normally uses two access files, `/etc/hosts.allow` and `/etc/hosts.deny`, but you can place all of the access control information in a single file for ease of maintenance.

For example, suppose you want to allow access to services only for hosts in `local.domain`, but not for any other hosts. Place these lines in `/etc/hosts.allow`:

```
ALL: .local.domain : ALLOW
ALL: ALL : DENY
```

The first match always determines whether or not access is granted. In this case, any host in `local.domain` (note the leading period in the pattern) will be allowed access to all services. All other hosts will be denied access.

Each line in `/etc/hosts.allow` looks something like this:

```
daemon_list : client_list : option : option ...
```

`daemon_list` is a list of services. For services in `/etc/inetd.conf`, use the name of the daemon program. For example, for Telnet service, the service name is `tn.teln`etd, because that is the argument to the tcpd program. You can list several daemons, separated by blanks.

In addition, the EXCEPT operator can be used in daemon and client lists. For example, to deny access to all services except FTP, use

```
ALL EXCEPT ftp : ALL : DENY
```

`client_list` is a space-separated list of client machines. Each entry in the list can take one of the following forms:

+   * A string that begins with `.` (period). A hostname matches if the last components of its fully qualified domain name match the string.

+   * A string that ends with `.` (period). A hostname matches if the first portion of its IP address matches the string. For example, `192.168.` matches any machine whose IP address begins with `192.168`.

+   * An expression of the form `n.n.n.n/m.m.m.m`, which is interpreted as a network/netmask pair. For example, `192.168.4.0/255.255.255.128` matches addresses from `192.168.4.0` through `192.168.4.127`.

In addition, you can use special keywords to match hosts:

+   * ALL matches any host (and any daemon in `daemon_list`).