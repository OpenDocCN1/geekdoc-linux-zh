# 594 Linux Administration: A Beginner's Guide

But if you just want to log into the remote host without needing to change your
login at the remote end, simply run ssh, like so:

```
[root@server-A ~] # ssh server-B
```

With this command, you will be logged in as the root user at server-B.
Of course, you can replace the hostname with a valid IP address, like

```
[root@server-A ~] # ssh yyang@192.168.1.50
```

To connect to a SSH server that is also listening on an IPv6 address (e.g.,
2001:DB8::2), you could

```
[root@server:2001~DB8::] ~# ssh -6 yyang@2001:DB8::
```

![](bbox=[0.084, 0.337, 0.163, 0.403])

> TIP If you don't have a remote server to test your ssh/scp/sftp connections, you
an easily switch all references to server-A or server-B to localhost. Similarly,
y can also switch all references to remote IP addresses from 192.168.1.150 to the
loopback IP address of 127.0.0.1. Where localhost and 127.0.0.1 refer to,
course, to your local server.

# Creating a Secure Tunnel

This section covers what is commonly called the 'poor man's virtual private network'
(VPN). Essentially, you can use SSH to create a tunnel from your local system to a remote
system. This is a feature when you need to access an intranet or another system
that is not exposed to the world outside our internet. For example, you can use ssh to
a file server machine that will set up the port forwarding to the web server.
Let's imagine a scenario like the described next with the following components:

+   - Inside The inside component consists of the entire local area network (LAN)
192.168.1.0 network). It houses various servers and workstations that are
accessible by other hosts on the inside. Let's assume that one of the internal
servers on the LAN hosts has a web-based accounting application. The internal web
server's hostname is "accounts" with an IP address of 192.168.1.100.

+   - Middle In the middle, we have our main component—a system with two
network interfaces. The system's hostname is serverA. One of the interfaces is
connected directly to the Internet. The other interface is connected to the LAN of
company.

On serverA, assume the first interface (the wide area network, or WAN,
interface) has a public/routable-type IP address of 1.1.1.1 and the second
interface has a private-type IP address of 192.168.1.1. The second interface of
server is connected to the LAN (192.168.1.0 network), which is completely cut
off from the Internet.

The only service that is allowed and running on the WAN interface of serverA
is the ssh daemon. serverA is said to be "dual-homed," because it is connected to
to two different networks: the LAN and the WAN.