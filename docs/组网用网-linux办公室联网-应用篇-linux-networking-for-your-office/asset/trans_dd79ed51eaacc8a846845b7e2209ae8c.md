
launches ftpd with appropriate parameters to let ftpd handle that one session and then quit. (Actually, inetd often uses yet another intermediary program to launch the daemon that does the real work.)

## NOTE

Many Linux distributions ship with versions of daemons intended to be called by inetd. These daemons usually have filenames beginning with in., as in in.ftpd.

The use of inetd allows you to configure which daemons you run by editing a single file—inetd's configuration file, /etc/inetd.conf. Each line in inetd.conf identifies a single network service to be handled by inetd. For instance, here's a line that configures ftp services:

```
ftp stream tcp nowait root /usr/sbin/tcpd /usr/sbin/in.ftpd
```

In the order they appear in the line, the meanings of these fields are

- 1. Service name (ftp)—This is the name of the service. In Linux, services are associated with individual ports in /etc/services. Rather than list port numbers in inetd.conf, service names appear.
- 2. Socket type (stream)—The type of socket, as discussed earlier in this chapter, is specified here.
- 3. Protocol (tcp)—The protocol is the TCP/IP Internet layer protocol (generally tcp or udp).
- 4. Wait/Nowait (nowait)—This field specifies how inetd handles multiple connection requests.
- 5. User (root)—The username under whose authority the service runs. This is generally root or nobody, but in some cases you can specify other users to improve system security.
- 6. Server program (/usr/sbin/tcpd)—In many cases, the server program is /usr/sbin/tcpd. This program then takes as a parameter the name of the program that actually handles the service. If the server program is listed as internal, it's a simple service that's handled internally to inetd.

## Note

> tcpd is part of the TCP Wrappers package. This package can help you to secure your system by screening connections and allowing or denying them based on a variety of criteria. I describe this and other packages that achieve similar results in Chapter 24, "Maintaining a Secure System."

- 7. Server program parameters (/usr/sbin/in.ftpd)—If the server program requires parameters, they come last on the line. When the server program is /usr/sbin/tcpd, the first parameter is the name of the program that actually processes the service requests.

## Tip

> One of the first things you should do after you install any Linux system that's connected to the Internet is to disable unused services. You do this by placing a pound sign (#) at the start of the line in /etc/inetd.conf that configures the service. By default, most Linux distributions come with many services commented out in this way for security purposes, but you should fine-tune these selections. In fact, you can comment out all the services in /etc/inetd.conf except those identified as internal—your computer will still boot and run. The services you're most likely to want include telnet (used for remote logins), ftp (used for remote file access), and linuxconf (on Red Hat and Mandrake systems, this is used for remote system configuration). You might want to use ssh instead of telnet and ftp for greater security, as discussed in Chapter 18, "Logging on Remotely Using ssh or telnet." I discuss setting up daemons for file and printer sharing in the relevant chapters.

Not all daemons run via inetd. Some work better if they're run separately, and come configured to do so. The common lpd, for instance, handles print jobs locally, and isn't an inetd launched daemon, though it is a daemon. Even when a daemon can run via inetd, you may want to run it independently because inetd's processing takes a small amount of time. If a daemon responds to a lot of requests, there's little advantage to placing it in inetd.conf except for the benefits of being able to "wrap" the daemon using TCP Wrappers, and the extra time to process the daemon's work can be a drawback.

## Starting and Stopping Daemons

You may occasionally want to start or stop a daemon without restarting your computer. You might want to do this to change a daemon's configuration, so that it behaves differently, or simply to add or remove a service. Fortunately, this is easy in Linux.

