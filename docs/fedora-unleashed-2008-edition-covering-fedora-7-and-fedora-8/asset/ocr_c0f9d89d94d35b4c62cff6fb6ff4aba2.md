This line defines the special `localhost` interface and assigns it an IP address of `127.0.0.1`. You might hear or read about terms such as `localhost`, `loopback`, and *dummy interface*; all these terms refer to the use of the IP address 127.0.0.1. The term `loopback interface` indicates that to Linux networking drivers, it looks as though the machine is talking to a network that consists of only one machine; the kernel sends network traffic to and from itself on the same computer. *Dummy interface* indicates that the interface doesn't really exist as far as the outside world is concerned; it exists only for the local machine.

Each networked Fedora machine on a LAN will use this same IP address for its `localhost`. If for some reason a Fedora computer does not have this interface, edit the `/etc/hosts` file to add the `localhost` entry, and then use the `ifconfig` and `route` commands as root to create the interface like this:

```
# ifconfig lo 127.0.0.1
# route add 127.0.0.1 lo
```

These commands create the `localhost` interface in memory (all interfaces, such as `eth0` or `ppp0`, are created in memory with Linux), and then add the IP address `127.0.0.1` to an internal (in-memory) table so that the Linux kernel's networking code can keep track of routes to different addresses.

Use the `ifconfig` command as shown previously to test the interface. You should now be able to use `ping` to check that the interface is responding properly like this (using either `localhost` or its IP address):

```
$ ping -c 3 localhost
PING localhost.localhost (127.0.0.1) from 127.0.0.1: 56(84) bytes of data.
64 bytes from localhost.localhost (127.0.0.1): icmp_seq=0 ttl=255 time=212 \usec
64 bytes from localhost.localhost (127.0.0.1): icmp_seq=1 ttl=255 time=80 usec
64 bytes from localhost.localhost (127.0.0.1): icmp_seq=2 ttl=255 time=50 usec

--- localhost.localhost ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max/mdev = 0.050/0.114/0.212/0.070 ms
```

The `-c` option is used to set the number of pings and the command, if successful (as it was previously), returns information regarding the round-trip speed of a test packet sent to the specified host.

# Networking with TCP/IP

The basic building block for any network based on UNIX hosts is the *Transport Control Protocol/Internet Protocol (TCP/IP)* suite of three protocols. The suite consists of the *Internet Protocol (IP)*, *Transport Control Protocol (TCP)*, and *Universal Datagram Protocol (UDP)*. IP is the base protocol. The TCP/IP suite is *packet-based*, which means that data is broken into