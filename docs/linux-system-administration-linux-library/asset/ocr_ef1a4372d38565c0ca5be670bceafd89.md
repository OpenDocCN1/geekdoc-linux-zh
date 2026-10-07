# Internet Servers 535

`in.ftpd -1 -a`

The final entry is any parameters that are to be passed to the server. When the “server” is TCP Wrappers, you pass the name of the real server, along with any parameters that server requires. TCP Wrappers then checks that the incoming request is allowed and calls the real server (in.ftpd in this example), along with whatever parameters you specify (as -1 and -a).

In the default inetd.conf file, you'll find entries for most common servers. Most of these entries are commented out with pound signs (#), however. You can therefore uncomment the appropriate entries when you add a server of a particular type. Conversely, if you remove a server or disable it, you can comment out the appropriate line it's active.

> TIP One first step to securing a Linux server is to comment out unnecessary lines from inetd.conf. In fact, none of the servers listed in this file are necessary for Linux to boot. Some servers may sound like they're critically important, but they aren't. The login server, for example, is a very low-security remote login server earlier; it is not required for ordinary text-mode logins or for remote logins via Telnet or SSH. You can go through inetd.conf and comment out all the servers except you're sure that you need.

After you've made changes to /etc/inetd.conf, you must send the server SIGHUP signal to reload its configuration file. You can do this as follows:

```
# ps ax | grep inetd
468 ? S 0:00 inetd
# kill -SIGHUP 468
```

The process ID (468 in the preceding example) may be different on your system. If possible, you should immediately test that your changes take effect. If you added or removed a server, make this test by trying to connect to the server.

# Using xinetd

Although inetd is the most common super server, it's not the only one. One moderately popular inetd replacement is xinetd (pronounced “zi-net-dee”), which can be obtained from http://www.synack.net/xinetd/. Hat 7.0 ships with xinetd rather than

![](bbox=[0.913, 0.747, 0.995, 0.813])