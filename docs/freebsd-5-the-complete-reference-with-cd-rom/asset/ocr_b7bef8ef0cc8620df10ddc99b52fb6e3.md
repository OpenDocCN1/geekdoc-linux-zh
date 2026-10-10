by examining the /etc/rc.conf file, which should have the following line if inetd is enabled:

```
inetd_enable="YES"
```

If you prefer to use sysinstall, you can set this line by activating the inetd option in the Network Services Menu accessible from the FreeBSD Configuration Menu. You can also type ps ax | grep inetd in your shell to see if inetd is currently running. If it's not, type inetd -ww to run it. (The -ww options enable TCP Wrappers, which is a separate package that inetd uses to provide security for the servers it handles. Chapter 29 describes TCP Wrappers in more detail.)

The inetd configuration file is /etc/inetd.conf. This file consists of a series of lines, each of which takes the following form:

```
service type protocol wait user server options
```

Lines that begin with pound signs (#) are comments and are ignored. The meanings of each of the fields in a noncomment line are as follows:

+   * **service** The first field is the service name, as specified in /etc/services. This setting defines the port number to which inetd will listen for this service. For instance, the line that begins with telnet lists to port 23 because /etc/services links port 23 to the telnet name, as described earlier, in “Standard Port Number Assignments.”

+   * **type** The second field usually consists of one of two words: stream or dgram. These words refer to some low-level details of how the server handles a connection.

+   * **protocol** The third field is usually tcp or udp, for TCP or UDP packet types. The standard FreeBSD inetd.conf also includes examples of tcp6, which are TCP services for IPv6 (Chapter 14 briefly describes IPv6, which is rare in 2002). Other values are possible, but unusual.

+   * **wait** The fourth field is either wait or nowait, and identifies how a datagram (dgram in the type field) server launches itself—whether it disconnects immediately from the calling program or remains connected until it finishes its work.

+   * **user** The fifth field is critically important because it defines the username under which inetd launches a server. If a server doesn't need root privileges to operate, you can reduce the security risks of running the server by running it as some other user, such as nobody (a standard low-privilege account) or an account created specifically for use by a server.