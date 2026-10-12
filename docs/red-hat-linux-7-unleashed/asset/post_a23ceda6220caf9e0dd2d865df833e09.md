
## traceroute

As you can see, **traceroute** can be an invaluable tool. Much more information can be gleaned from **traceroute** output; it is best to read the **traceroute**(8) man page for a complete discussion.

## tcpdump

**tcpdump** is another invaluable tool for debugging some types of network problems. It basically works as a *packet sniffer*--it listens to the network, looks at any packets that come by (whether destined for the host on which it is running or not), and operates on it. It can store all or just some interesting parts of the traffic it sees, or perform a rudimentary analysis of the information it contains.

**tcpdump** works by setting the network card into what is known as *promiscuous mode*. Normally, a network card will only see packets that are meant for *it*. However, in promiscuous mode, it will see all packets that pass through the network and pass them to the operating system above. The OS then passes the packets to **tcpdump**, which can then filter and display or store them. Because it modifies the configuration of the network card, **tcpdump** must be run by *root*.

### Caution

> **tcpdump** is a potential security hole. It falls into the category of programs known as *sniffers*, which listen to the network and can listen to all packets in the network and store them. If users use programs such as *Telnet* that send passwords in the clear, a cracker might use a sniffer to sniff out their passwords. Because of this, **tcpdump** should never be installed *setuid* *root*.

To detect whether a network interface is in promiscuous mode (and thus might have a sniffer running on it), use the **ifconfig** command to display the interface's configuration. The **PROMISC** flag will appear if the interface is in promiscuous mode:

```
$ /sbin/ifconfig eth0
eth0      Link encap:Ethernet  Hwaddr 00:00:97:5E:F0:61
          inet addr:10.0.1.50  Bcast:10.0.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING PROMISC MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:5 errors:0 dropped:0 overruns:0 carrier:5
          Collisions:0
          Interrupt:3 Base address:0x310
```

If you run `tcpdump` without any arguments, you get a listing of all the packets that pass through the network:

```
# /usr/sbin/tcpdump

tcpdump: listening on eth0
22:46:12.730048 renato.1445832987 > visionlu.nfs: 100 readlink [nfs]
22:46:12.734424 tunoloia.1012 > visionlu.800: uo2 92
22:46:12.746763 tunoloia.22 > atman.1023: P 1442999991:1423000355 (44) ack 3798274339 win 32120 <OF> [tos 0x10]
22:46:12.765084 atman.1023 > tunoloia.22: . ack 44 win 32120 <OF> [tos 0x10]
22:46:12.778100 visionlu.800 > tunoloia.1015: uo2 56
22:46:12.780084 renaro.144837013 > visionlu.nfs: 124 lookuo [nfs]
22:46:12.780153 tunoloia.22 > atman.1023: P 44:596(552) ack 1 win 32120 <OF> [tos 0x10]
```

The dump will stop when you press Ctrl+C.

As you can see, `tcpdump` by default converts IP addresses to hostnames and port numbers to service names. It also attempts to interpret some packets (such as those where the line ends with `lookuo [nfs]`, which are NFS lookups). In some cases, the number of bytes that `tcpdump` looks at (68) might not be enough to fully decode the packet. In this case, you may use the `-s` option to increase the number (see the `-s` option in Table 20.5).

You don't often want to see all the packets, especially in medium to large networks. Sometimes you want to see all the packets going between two specific hosts, or even those that use a specific service. `tcpdump` takes as a parameter an optional filter expression that will select only certain packets.

`tcpdump`'s filter expressions consist of one or more primitives joined by the keywords `and`, `or`, and `not`. Each primitive consists of a qualifier followed by an ID. A qualifier consists of one or more keywords, the most common of which are shown in Table 20.4. The ID specifies the value the corresponding field must have to match the filter.

### TABLE 20.4 Most Common tcpdump Qualifiers

| Qualifier | Matches |
| :--- | :--- |
| src host | The IP address of the host from where the packet comes. |
| dst host | The IP address of the host to which the packet is going. |
| host | The IP address of the source or the destination host. |
| src port | The port the packet is coming from. |
| dst port | The port the packet is going to. |
| port | The source or the destination port. |
| tcp, udp, or icmp | The packet's protocol is the specified one. |

### Tip

One common mistake is to run `tcpdump` through a remote connection, such as when connected through `telnet` or `ssh`, with a filter that includes all the `telnet` or `ssh` packets. An example is including just `host thishost`, where `thishost` is the host on which `tcpdump` is running. In that case you end up with an incredible amount of output. This is because the first packet that comes through generates output, which is transmitted through the network and captured by `tcpdump`, which generates more output, which is also transmitted through the network, and so on.

To prevent that, be more specific in your filter expressions. For example, you might include the primitive `not port 22` to filter out `ssh` packets.

`tcpdump` also takes several switches, the most common of which are shown in Table 20.5.

### Table 20.5 Most Common tcpdump Switches

| Switch | Description |
| :--- | :--- |
| `-c count` | Exit after receiving `count` packets. |
| `-i interface` | Listen on `interface`. By default, `tcpdump` listens on the first interface found after the loopback interface. You can see the order in which the interfaces are searched using the `ifconfig -a` command. |
| `-n` | Don't convert numeric addresses and port numbers to host and service names (print numeric output). This eliminates the need for DNS lookups. |
| `-N` | Print out only the hostname, not its fully qualified domain name. For example, if you give this flag then `tcpdump` will print `redhat` instead of `redhat.com`. |
| `-r file` | Read packets from `file`, which must have been created with the `-w` option. |
| `-s snaplen` | Grab `snaplen` bytes from each packet. The default is 68, which is enough for IP, ICMP, TCP, and UDP packets. However, for certain protocols (such as DNS and NFS), a `snaplen` of 68 will truncate some protocol information. This is marked by `[protocol]`, where the `protocol` indicates the protocol part where truncation occurred. |
| `-v` | Verbose mode. Print some more information about each packet. |
| `-vv` | Even more verbose output. Print much more information about each packet. |
| `-w file` | Capture the packets in `file`. |
| `-x` | Print out each packet in hex. This will print out either the whole packet or `snaplen` bytes, whichever is less. |

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_720_0.png)

## Network Security Tools

There are several tools that help you secure your networks. First of all, you must have a firewall to separate your internal network from the Internet and to prevent hackers from getting in. Then there is the problem of getting into your network from the outside, and from your network to the outside world, without leaving a wide-open door for hackers.

You must remember that the most important factor in security is usually the human one. You might have the best firewall in the world, perfectly configured, and an employee might simply copy confidential information to a floppy disk and hand it to a competitor. Security starts with people and with a good security policy. This particular subject cannot be discussed in depth here, however. If you want to learn more (and you should!), an excellent reference is *Maximum Security, Second Edition: A Hacker’s Guide to Protecting Your Internet Site and Network*, (ISBN 0-672-31341-3, Sams Publishing).

### Firewalls

A *firewall* is a computer that stands between a trusted network (such as your internal network) and an untrusted network (such as the Internet), and controls what traffic passes between them. It is an essential piece of the information security puzzle.

There are two general types of firewalls (which may be combined): application-level firewalls (known as *proxies*), and packet-filtering firewalls. A *packet-filtering firewall* simply allows or disallows packets depending on their content. Most packet-filtering firewalls determine what packets to allow or disallow based on the source or destination addresses, source or destination port, and whether the packet is part of an ongoing conversation.

An application-level firewall or proxy acts as an intermediary between client and server programs. Instead of connecting directly to the server, a client application connects to the proxy and asks it for the information. The proxy opens a connection to the server, sends the request, and continues to pass information back and forth between server and client (see Figure 20.9).

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_721_0.png)
