Mail protocols are next. If you're not running a mail server, there's no reason for inetd to be listening for mail service requests. Disable them if you're not using them.

```
#pop-2 stream tcp nowait root /usr/sbin/tcpd pop2d
#pop-3 stream tcp nowait root /usr/sbin/tcpd pop3d
#imap stream tcp nowait root /usr/sbin/tcpd imapd
```

The Unix-to-Unix Copy Protocol server is not necessary in many installations, therefore there is no need to enable this service in most situations.

```
#uucp stream tcp nowait uucp /usr/sbin/tcpd/usr/lib/uucp/uucico -1
```

The following line configures bootpd. Bootpd is used by devices that need information on bootup but have no storage media to keep it on between reboots. It is often used to serve diskless workstations and printers. If you are not serving such information, you can disable this service.

```
#bootps dgram udp wait root /usr/sbin/tcpd bootpd
```

Trivial file transfer protocol is set up with the next line. With no arguments, access is limited to the directory /tftpboot. If this directory doesn't exist, no access is granted. Any path arguments are treated as readable directories, so you should be careful to make sure there are no paths that you don't require in the argument list. It is best to disable this service unless you need it.

```
#tftp dgram udp wait root /usr/sbin/tcpd in.tftpd
```

Using the next four services is very risky because they give outsiders information about your system. If you need a finger-type service, you should change the line in inetd.conf to use safe_finger instead of in.fingerd. safe_finger filters out data passed to in.fingerd so that a malicious user can't send arguments to in.fingerd that would break it.

```
#finger stream tcp nowait root /usr/sbin/tcpd in.fingerd
#cfinger stream tcp nowait root /usr/sbin/tcpd in.cfinger
#systat stream tcp nowait guest /usr/sbin/tcpd /bin/ps -auxwx
#netstat stream tcp nowait guest /usr/sbin/tcpd/bin/netstat -f inet
```

The next line is for the identd service. Identd is used by external servers when someone tries to connect to them from your machine. It is supposed to return information about the user and machine attempting the connection, but some information is omitted for security purposes. The -o option tells identd not to return the operating system type. This is a good idea because a hacker learning what operating system you are running is able to tailor attacks specific to that operating system. The -1 option tells identd to use the syslog utility for logging, and the -e option tells identd to return UNKNOWN_ERROR instead of more specific error messages. Many servers will not allow connections if your machine does not return