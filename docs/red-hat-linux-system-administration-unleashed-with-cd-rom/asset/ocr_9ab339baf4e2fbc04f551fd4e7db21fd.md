Compiling xinetd locally will enable you to build it against the libwrap library which tcpd uses to perform access control. When it is built against libwrap, it will check incoming connections against /etc/hosts.allow and /etc/hosts.deny before performing its own access control. In Red Hat 6, the libwrap library is available in the tcp_wrappers package.

# Configuring xinetd

xinetd is configured with its own /etc/xinetd.conf file, which uses a different syntax from that of inetd. Both the RPM package and the source provide a sample configuration file, and there is also a program itox, which can translate an existing /etc/inetd.conf file to the syntax needed by xinetd. (The Red Hat package renames this program to inetd2xinetd.) You can say

```
itox < /etc/inetd.conf > xinetd.conf.generated
```

to produce a valid xinetd.conf file of your existing configuration, ready for editing and tweaking.

The /etc/xinetd.conf file contains a series of multi-line entries. The format is as follows:

```
service service-name
{
    attribute = value ...
    ...
}
```

Each entry relates to a single service, identified by the service-name. A service may have a number of attributes, each of which can be adjusted with an assignment operator and a new value (or group of values). There are actually three types of assignments: "=", "-=", and "+=". Most attributes only support the simple "=" assignment operator, but those which are in fact a set of values use "-=" to remove an item from the set, and "+=" to add a new item.

The attributes that correspond to the fields in the normal /etc/inetd.conf are as follows.

+   - socket_type—This can take the value stream, dgram, or raw, just as the equivalent field in /etc/inetd.conf.
+   - protocol—The protocol name from /etc/protocols, as for /etc/inetd.conf. It may be omitted, in which case the default protocol for the service will be used.
+   - wait—This can be either yes or no, equivalent to wait or nowait, respectively, in /etc/inetd.conf.