# 226 Part II ♦ Running the Show

delivered from some other computer to your Linux box, the remote system must first establish a network connection with your system. Your computer receives the connection request, examines it, sees it labeled for port 25, and thus knows that the connection should be directed to the program that handles e-mail (which happens to be sendmail).

I mentioned that SMTP uses the TCP protocol. Some services use UDP, the User Datagram Protocol. All you need to know how TCP and UDP (for the purpose of this security connection) is that they provide different ways of packaging the information sent over a network connection. A TCP connection provides every detection and retransmission of lost data. UDP doesn't check to ensure that the data arrived complete and intact; it is as as fast way to send non-critical information.

# Disabling Network Services

There are hundreds of services (with official port numbers listed in /etc/services) that could potentially be available and subject to attack upon your Linux system, in reality only a few services are installed and only a handful of those are by default. In Fedora and RHEL systems, most network services are started by the xinetd process or by a start-up script in the /etc/init.d directory. Other services use the xinetd process instead of xinetd.

xinetd and inetd are daemons that listen on a great number of network port numbers. When a connection is made to a particular port, xinetd or inetd automatically starts the appropriate program for service and handles the connection to it.

For xinetd, the configuration file /etc/xinetd.conf is used to provide default settings for the xinetd server. The directory /etc/xinetd.d contains files xinetd what ports to listen on and what programs to start (the inetd daemon, uses only the /etc/xinetd.conf file). Each file in /etc/xinetd.d contains configuration information for a single service, and the file is usually named after the service it covers. For example, to disable the rsync service, edit the rsync file in the / directory and look for a section similar to the following:

```
service rsync {
    disable      = yes
    socket_type   = stream
    wait          = no
    user          = root
    server        = /usr/bin/rsync
    server_args   = -daemon
    log_on_failure += USERID
}
```

Note that the first line of this example identifies the service as rsync. This exactly matches the service name listed in the /etc/services file, causing the service to