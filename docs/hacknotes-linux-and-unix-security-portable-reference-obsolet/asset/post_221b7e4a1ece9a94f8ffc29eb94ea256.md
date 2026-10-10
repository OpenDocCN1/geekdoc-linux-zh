
# Reverse Ident

Ident (Identification Protocol) servers listen for connections on port 113. If a TCP connection is established to a port listening on the host running the ident server, the ident server may be queried for the privilege level of the process associated with the connection.

# Reverse Ident Scans

Using the `-I` flag in `nmap` will perform a TCP reverse ident scan:

```bash
$ nmap -I -sT -p 80 192.168.1.100
```

Starting `nmap` V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (192.168.1.100):

| Port | State | Service | Owner |
| :--- | :--- | :--- | :--- |
| 80/tcp | open | http | nobody |

Nmap run completed -- 1 IP address (1 host up) scanned in 1 second

# XMAS

This method of scanning involves sending out a TCP packet with the FIN, URG, and PUSH flags set. If the target host is listening on the particular port, it sends a RST packet back. If the target host is not listening on that port, it does not respond.

> FIN packets are normally used to tear down an established TCP connection. URG packets signify that information needing immediate attention is present within the IP packet, such as a ^C sent during a telnet session. A PUSH packet signifies that the sender requests the receiver to immediately pass all buffered data to the applications.

# XMAS Scanning

Using the `-sX` flag in `nmap` will perform an XMAS scan:

```bash
$ nmap -sX 192.168.1.1
```

Starting `nmap` V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (192.168.1.1):
(The 1597 ports scanned but not shown below are in state: closed)

| Port | State | Service |
| :--- | :--- | :--- |
| 22/tcp | open | ssh |
| 80/tcp | open | http |
| 113/tcp | open | auth |
| 6000/tcp | open | X11 |

Nmap run completed -- 1 IP address (1 host up) scanned in 6 seconds

## NULL

This type of scan involves sending a TCP packet to the destination host with all the flags turned off in the TCP header. If the target host is listening on the particular port, it will not respond. Otherwise, it will send a RST packet.

## NULL Scanning

Using the `-sN` flag in `nmap` will perform a TCP NULL scan:

```bash
$ nmap -sN 192.168.1.100
```

Starting `nmap` V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (192.168.1.100):
(The 1594 ports scanned but not shown below are in state: closed)

| Port | State | Service |
| :--- | :--- | :--- |
| 21/tcp | open | ftp |
| 22/tcp | open | ssh |
| 25/tcp | open | smtp |
| 53/tcp | open | domain |
| 80/tcp | open | http |
| 110/tcp | open | pop-3 |
| 113/tcp | open | auth |

Nmap run completed -- 1 IP address (1 host up) scanned in 41 seconds

## RPC

This type of scan is used to send NULL commands to open ports in order to determine if they are RPC (remote procedure call) ports. Once an open port is determined to be an RPC port, information about the application that is bound to the port is queried for and obtained.

## RPC Scanning

Using the `-sR` option in `nmap` will perform an RPC scan:

```bash
$ nmap -sR 10.0.0.10
```

Starting `nmap` V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (10.0.0.10):
(The 1584 ports scanned but not shown below are in state: closed)

| Port | State | Service (RPC) |
| :--- | :--- | :--- |
| 7/tcp | open | echo |
| 21/tcp | open | ftp |
| 22/tcp | open | ssh |
| 37/tcp | open | time |
| 53/tcp | open | domain |
| 111/tcp | open | sunrpc (rpcbind V2-4) |
| 113/tcp | open | auth |
| 512/tcp | open | exec |
| 513/tcp | open | login |
| 514/tcp | open | shell |
| 515/tcp | open | printer |
| 587/tcp | open | submission |
| 2049/tcp | open | nfs (nfs V2-3) |
| 4045/tcp | open | lockd (nfs V2-3) |
| 7100/tcp | open | font-service |
| 32771/tcp | open | sometimes-rpc5 (ypserv V1-2) |
| 32772/tcp | open | sometimes-rpc7 |

Nmap run completed -- 1 IP address (1 host up) scanned in 40 seconds

## IP Protocol

The aim of this type of scan is to determine which IP protocols are supported on the target host. It sends raw IP packets destined for particular protocols, and if an ICMP protocol unreachable message is received, then the particular protocol is most likely unsupported on the target host.

### IP Protocol Scanning

Using the `-sO` flag in `nmap` will perform an IP protocol scan:

```bash
$ nmap -sO 192.168.1.1
```

Starting `nmap` V. 3.00 ( www.insecure.org/nmap/ )
Interesting protocols on (192.168.1.1):
(The 251 protocols scanned but not shown below are in state: closed)

| Protocol | State | Name |
| :--- | :--- | :--- |
| 1 | open | icmp |
| 2 | open | igmp |
| 6 | open | tcp |
| 17 | open | udp |

## ACK

This type of scan is mainly used to determine firewall rule sets. ACK packets are sent to the target host. If the target host does not respond or sends back an ICMP unreachable packet, then the port is probably being filtered by a firewall. If the target sends back a RST packet, then the port is not being filtered by a firewall.

### ACK Scanning

ACK scans can be performed by using `nmap` with the `-sA` flag:

```bash
nmap -sA target_address
```

## Window

This type of scan, while similar to the ACK scan, sometimes helps detect open, filtered, and unfiltered ports on some systems due to an anomaly in the way TCP window sizes are reported.

### Window Scanning

Window scans can be performed by potential intruders using `nmap` with the `-sW` flag:

```bash
nmap -sW target_address
```

## UDP

In order to determine if a host is listening on a particular UDP port, a UDP packet is sent to the port. If the target host is not listening on the particular port, an ICMP port unreachable packet is received. However, if the target host is listening on the particular port, no such packet is received. Since UDP is not a connection-oriented protocol, UDP scanning is unreliable.

### UDP Port Scanning

Using the `-sU` option in `nmap` will perform UDP scanning:

```bash
$ nmap -sU 192.168.1.100

Starting Nmap 7.54BETA31 ( https://nmap.org/ )
Interesting ports on (192.168.1.100):
(The 1454 ports scanned but not shown below are in state: closed)
PORT      STATE         SERVICE
53/udp    open          domain
```

### Defend Against Port Scans

You can use these methods to counter scans directed at your networks:

- Configure your firewall to drop packets destined for closed ports. This will slow down scans directed toward your network, since this will cause the port scanning applications to resend SYN packets after the timeout value is exceeded. Only after repeated timeouts, the port scan application will assume the port to be filtered, and will move on to the next set of ports.
- Most firewalls and IDSS have the ability to detect port scans. Make use of this feature, and routinely watch your logs.
- Configure your firewall to not trust source port values. Stateful firewalls have the ability to allow source port 20 packets only from FTP servers to whom connections are known to have been established. In any case, the use of a clear-text protocol such as FTP is not recommended. Better alternatives (such as SSH) exist and should be used instead. In addition, do not allow incoming TCP packets with the source port set to 53 unless they are destined for your DNS servers that need to perform zone transfers. Restrict DNS traffic by IP addresses of the DNS servers authorized to serve your hosts.
- Most FTP servers do not allow clients to issue a PORT command with the IP address of a host other than that of the client. This will prevent FTP bounce scans. Check your FTP server documentation and configurations for details.
- Configure your firewalls to drop or reset connection attempts to the ident port (113).
- Use a stateful firewall. This will prevent most of the scans mentioned in the preceding text.

## FINGERPRINTING

Though many operating system designers do their best to follow relevant RFCs, the operating system kernel authors sometimes interpret details differently. Tools such as Xprobe2 and Nmap probe for such differences in order to fingerprint the target operating systems.

### Fingerprinting Operating Systems Using Xprobe2

Xprobe2 uses ICMP packets to perform fingerprinting. Results are sorted by scores assigned to best guesses of the target operating systems. This tool, which has the ability to distinguish between filtering devices along the path to the destination, is available at http://www.sys-security.com/html/tools/tools.html.

Here is an example of how to use Xprobe2:

```bash
# xprobe2 -v target.somecompanyasanexample.com

Xprobe2 v.0.1 Copyright (c) 2002 Fygrave@tigerteam.net,
ofir@sys-security.com

[+] Target is target.somecompanyasanexample.com
[+] Loading modules.
[+] Following modules are loaded:
    [x]ICMP echo (ping)
    [x]TTL distance
    [x]ICMP echo
```
