
# 30 Part I: Hacking Techniques and Defenses

```
113/tcp open auth
512/tcp open exec
513/tcp open login
514/tcp open shell
515/tcp open printer
587/tcp open submission
2049/tcp open nfs (nfs V2-3)
4045/tcp open locked (nfs V2-3)
7100/tcp open font-service
32771/tcp open sometimes-rpc5 (ypserv V1-2)
32772/tcp open sometimes-rpc7
```

Nmap run completed -- 1 IP address (1 host up) scanned in 40 seconds

# IP Protocol

The aim of this type of scan is to determine which IP protocols are supported on the target host. It sends raw IP packets for particular protocols, and if an ICMP protocol unreachable message is received, then the particular protocol is most likely unsupported on the target host.

# IP Protocol Scanning -sO flag in nmap will perform an IP protocol scan.

```bash
[bash]# nmap -sO 192.168.1.1
```

Starting nmap V.3.00 ( www.insecure.org/nmap/ )
Interesting protocols on (192.168.1.1):
The 251 protocols scanned but not shown below are in state: (closed)

| Protocol | State Name |
|---|---|---|
| 1 | open icmp |
| 2 | open igmp |
| 6 | open tcp |
| 17 | open udp |

# ACK

This type of scan is mainly used to determine firewall rule sets. ACK packets are sent to the target host. If the target host does not respond or sends back an ICMP unreachable packet, then the port is likely being filtered by a firewall. If the target sends back a RST packet, then the port is not being filtered by a firewall.

# ACK Scanning

ACK scans can be performed by using nmap with the -sA flag.

```
nmap -sA target_address
```

# Chapter 2: Scanning and Identification 31

# # Window

This type of scan, while similar to the ACK scan, sometimes helps detect open, filtered, and unfiltered ports on some systems due to an anomaly in the way TCP window sizes are reported.

# ## Window Scans

Window scans can be performed by potential intruders using nmap with the -sW flag:

```
nmap -sW target_address
```

# ## UDP

In order to determine if a host is listening on a particular UDP port, a UDP packet is sent to the port. If the target host is not listening on the particular port, an ICMP port unreachable packet is received. However, if the target host is listening on the particular port, no such packet is received. Since UDP is not a connection-oriented protocol, UDP scanning is unreliable.

# ## UDP Port Scanning

Using the -sU option in nmap will perform UDP scanning:

```bash
[bash]# nmap -sU 192.168.1.100
```

Starting nmap V. 2.54BETA31 ( with insecure.org/nmap/ )
Interrupting ports on (192.168.1.100):
The 1454 ports scanned but not shown below are in state: (closed)

| Port | State | domain |
|---|---|---|
| 53/udp | open | |

# ## Defend Against Port Scanning

You can use these methods to counter scans directed at your networks:

- - Configure your firewall to drop packets destined for closed ports. This will slow down scans directed toward your network, since this will cause the port scan applications to respond SYN packets after the timeout value is exceeded. Only after repeated timeouts, the port scan application will assume the port to be filtered, and will move on to the next set of ports.
- Most firewalls and IDSs have the ability to detect port scans, and routinely watch your logs.
- - Configure your firewall to not trust source port values. Stateful firewalls have the ability to allow source port 20 packets only from FTP servers to whom are known to have established. In any case, the use of a clear-text protocol such as FTP is not recommended. Better alternatives (such as SSH) exist and should be used instead. In addition, do not allow incoming TCP packets with the source port set to 53 unless they are destined for your DNS servers that need to perform transfers. Restrict DNS traffic by IP addresses of the DNS servers authorized to serve your hosts.
- - Most FTP servers do not allow clients to use an IP address of a host other than that of the client. This will prevent bounce scans. Check your FTP server documentation and configurations for details.
- - Configure your firewalls to drop or reset connection attempts to the ident port (113).
- - Use a stateful firewall. This will prevent most of the scans mentioned in the preceding text.

# # FINGERPRINTING

Though many system designers do their best to follow relevant RFCs, the operating system kernel sometimes interpret details differently. Tools such as Xprobe and Nmap probe for such differences in order to fingerprint the target operating systems.

# ## Fingerprinting Operating Systems Using Xprobe

Xprobe uses ICMP packets to perform fingerprinting. Results are sorted by scores assigned to best guesses of the operating systems. This tool, has the ability to distinguish between filtering devices along the path to the destination, is available at http://www.sys-security.com/html/tools/tools.html. Here is an example of how to use Xprobe:

```bash
[bash] xprobe -v target.someexample.com
```

Xprobe v0.1 Copyright (c) 2002 ygrave@tiger.net, ofir@sys-security.com
+] Target is target.someexample.com
+] Loading modules:
+] ICMP echo (ping)
+] ICMP distance
+] ICMP echo
+] ICMP Timestamp
+] ICMP Address
+] ICMP Request
+] Initial engine
+] Running scan
+] Host: 192.168.1.1 is up (Guess probability: 100%)
+] Target: 192.168.1.1 is alive
+] Primary guesses:
+] Host: 192.168.1.1 OS: "Linux Kernel 2.4.5" (Guess probability: 60%)
+] Other guesses:
+] Host: 192.168.1.1 OS: "Linux Kernel 2.4.0 - 2.4.4" (Guess probability: 60%)
+] Host: 192.168.1.1 OS: "Linux Kernel 2.2" (Guess probability: 60%)
+] Host: 192.168.1.1 OS: "Microsoft Windows NT 4 Service Pack 4 and Above" (Guess probability: 60%)
+] Host: 192.168.1.1 OS: "BSD 1.2" (Guess probability: 50%)
+] Host: 192.168.1.1 OS: "Microsoft Windows NT 4 Service Pack 3 and Below" (Guess probability: 50%)
+] Host: 192.168.1.1 OS: "Microsoft Windows ME" (Guess probability: 50%)
+] Host: 192.168.1.1 OS: "Microsoft Windows 2000/2000SP1/2000SP2" (Guess probability: 50%)
+] Host: 192.168.1.1 OS: "Microsoft Windows XP" (Guess probability: 50%)
+] Host: 192.168.1.1 OS: "FreeBSD 4.5" (Guess probability: 45%)
+] Host: 192.168.1.1 OS: "OS X 10.1.5" (Guess probability: 40%)
+] Host: 192.168.1.1 OS: "Microsoft Windows 98/98SE" (Guess probability: 40%)
+] Host: 192.168.1.1 OS: "Digital UNIX 5.6" (Guess probability: 35%)
+] Host: 192.168.1.1 OS: "Sun Solaris 5 (SunOS 2.5)" (Guess probability: 35%)
+] Host: 192.168.1.1 OS: "Sun Solaris 6 (SunOS 2.6)" (Guess probability: 35%)
+] Host: 192.168.1.1 OS: "Sun Solaris 7 (SunOS 2.7)" (Guess probability: 35%)
+] Host: 192.168.1.1 OS: "Sun Solaris 8 (SunOS 2.8)" (Guess probability: 35%)
+] Host: 192.168.1.1 OS: "FreeBSD 3.4"
+] Cleaning up scan engine
+] Modules deinitialized
+] Execution completed.
```

# Using nmap to Perform Operating System Fingerprinting

The nmap program can also be used by an intruder to perform an OS fingerprinting, using the -O flag:

```bash
[bash]# nmap -O 192.168.1.1
```

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (192.168.1.1):
(The 1597 ports scanned but not shown below are in state: closed)

| Port | State | Service |
|---|---|---|
| 22/tcp | open | ssh |
| 80/tcp | open | http |
| 113/tcp | open | auth |
| 6000/tcp | open | X11 |

Remote operating system guess: Linux Kernel 2.4.0 - 2.5.20
Uptime 6.584 days (since Sun Oct 27 10:23:37 2002)

Nmap run completed -- 1 IP address (1 host up) scanned in 8 seconds

# SUMMARY

Hosts be pinged in order to quickly determine if they are alive. In addition, various scanning techniques can be used to determine what ports are open on the alive hosts. Operating System fingerprinting tools can then be used to recognize the Operating System versions on the target hosts. Once an intruder has followed such a methodology, he or she can then move on to the process of username and service enumeration as described next, in Chapter 3.
