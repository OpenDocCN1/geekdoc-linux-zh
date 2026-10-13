```
telnet stream tcp nowait root /usr/sbin/tcpd
in.telnetd
```

```
pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
```

Figure out what services you must keep and what you can live without. Do not forget to restart inetd services after modifying /etc/inetd.conf. You can use the killall -HUP inetd command to restart it.

# Using the TCP wrapper to secure inetd run services

The configuration lines in /etc/inetd.conf indicate that the server_path part of each line is always /usr/sbin/tcpd and the actual server program is an argument to the tcpd program. For example,

```
pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
```

is functionally equivalent to having the following line:

```
pop-3 stream tcp nowait root /usr/sbin/ipop3d
```

When a POP3 request is received by inetd, the ipop3d server is started in both cases, but the first one is much more secure than the other, because the tcpd program is a TCP wrapper program that enhances security by providing the following services:

+   - Logging service. Logs information about a request by using the syslog facility.
+   - Host-based access control. Provides host-based access control by using pattern matching.
+   - Host name and address verification service. Detects spoofing of host names or addresses when a host is pretending to be some other host.

The TCP wrapper is sufficiently important that it comes as part of the default Red Hat Linux installation. Absolutely no reason exists for not wrapping each of your inetd services with the TCP wrapper.

![](bbox=[0.1, 0.9, 0.18, 0.98])

# Caution

By default, Red Hat Linux does not wrap the Web service for linuxconf using tcpd, because it appears to not work when wrapped with tcpd. This is a very good reason not to run a linuxconf Web service.