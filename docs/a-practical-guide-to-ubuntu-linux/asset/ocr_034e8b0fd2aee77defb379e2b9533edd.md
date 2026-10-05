# 464 CHAPTER 11 SYSTEM ADMINISTRATION: CORE CONCEPTS

You can test this setup from a remote system by giving the following command:

```
$ rpcinfo -p hostname
No remote programs registered.
```

Replace hostname with the name of the remote system that you changed the hosts.deny file on. The change is immediate; you do not need to kill or restart a daemon.

Add the following line to the hosts.allow file on the server system:

```
portmap: host-IP
```

where host-IP is the IP address of the trusted, remote system that you gave the preceding rpcinfo command. Use only IP addresses with portmap in hosts.allow; do not use names that portmap could get stuck trying to resolve. If you give the same command, rpcinfo should display a list of the servers that RPC knows about, including portmap. See page 747 for more examples.

# Set the clocks

+   The portmap daemon relies on the client's and the server's clocks being synchronized. A simple Dos attack (page 1146) can be initiated by setting the server's clock to the wrong time.

# The inetd and xinetd superservers

The inetd (Internet daemon) daemon and its replacement xinetd (extended Internet daemon; xinetd.org) are called supervisors or service dispatchers because they handle other daemons, such as smbd (Samba) and vsftpd (FTP). These supersvisors listen for network connections. When one is made, they identify a daemon based on the port the connection comes in, set the daemon's standard input and output file descriptors to the socket (page 503), and start the daemon.

Using these supervisors offers two advantages over constantly running daemons that monitor ports. First, the supervisors avoid the need for daemons to run when not in use. Second, they develop to write servers that read from standard input and write to standard output; they handle all socket communication.

The inetd, which originally shipped with 4.3BSD, was not particularly secure. However it opened the possibility that exploitable software could be exposed to the Internet. Its successor, xinetd, introduced access control and logging. This daemon allowed an administrator to limit how a service was available and the origin and number of incoming connections. When compiled with libwrap, xinetd (discussed in the next section).

At a time when CPU was more limited than it is and RAM was more expensive, these supervisors offered the advantage of efficient memory and CPU usage. Systems have slowly moved away from using these supervisors over the past few years. Today a system can easily save the megabytes of memory and the minimal CPU time it takes to keep a daemon running to monitor a port: It takes