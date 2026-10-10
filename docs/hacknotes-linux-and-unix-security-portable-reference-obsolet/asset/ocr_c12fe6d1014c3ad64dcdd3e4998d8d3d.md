New mail received Wed Jan 15 14:36:29 2003;
    unread since Wed Jan 11 14:29:54 2003

No Plan.

An old fingerd (finger daemon) version of Solaris has been known to contain a vulnerability that discloses the list of all usernames on the host if queried with a string such as “a b c d e f g h”:

```
finger 'a b c d e f g h'@host
```

See http://www.securityfocus.com/bid/3457/info/ for more information about this vulnerability.

![](bbox=[0.1, 0.35, 0.15, 0.39])

# Disable Finger

If you are running the finger server, it is strongly recommended that you consider the following suggestions:

+   Consider disabling the finger service if possible. It provides far too much information about your system to local users and intruders. If you use inetd, finger can be disabled by commenting out the appropriate line in /etc/inetd.conf. If you use xinetd, edit the file named finger in the xinetd.d directory and make sure the following line exists:
+   `disable = yes`
+   You must restart inetd or xinetd in order for changes to take effect.

+   If you must run the finger server, configure your firewall to drop incoming connections to port 79. This will prevent users on external networks from querying your hosts.

![](bbox=[0.1, 0.69, 0.15, 0.73])

# HTTP (HyperText Transfer Protocol): 80 (TCP)

HTTP is a stateless protocol used to distribute various hypermedia. It is most widely used to serve WWW (World Wide Web) content.

# Obtain the HTTP Server Banner

In order to grab banner information from HTTP servers, telnet to the port they are listening on and issue the following request:

```
HEAD / HTTP/1.0[enter][enter]
```

For example:

```
(bash)$ telnet www.somecompanyasanexample.com 80
Trying 10.0.0.100...
Connected to www.somecompanyasanexample.com.
```