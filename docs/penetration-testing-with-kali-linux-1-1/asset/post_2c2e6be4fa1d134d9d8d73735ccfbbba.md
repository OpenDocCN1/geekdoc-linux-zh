
| No. | Time | Source | Destination | Protocol | Length Info |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 3 | 8.125497384 | 19.11.0.126 | 19.11.1.145 | TCP | 31 80BPS TCP-1 |
| 4 | 8.187829833 | 19.11.1.115 | 19.11.6.126 | ICMP | 71 Destination unreachable (Port un... |
| 5 | 1.802881589 | 19.11.0.126 | 19.11.1.115 | UDP | 43 51082 - 161 Len=5 |
| 6 | 2.003950947 | 19.11.0.125 | 19.11.1.115 | UDP | 43 51082 - 161 Len=5 |
| 7 | 2.403284646 | 19.11.0.126 | 19.11.1.115 | UDP | 43 43218 - 160 Len=1 |
| 8 | 2.231871853 | 19.11.1.115 | 19.11.8.126 | ICMP | 71 Destination unreachable (Port un... |

![](img/ec25e59d75726b7041242a56d3376832_182_0.png)

As seen in Figure 43, an empty UDP packet is sent to a specific port (packets 3, 5, 6, and 7). If the destination UDP port is open, the packet will be passed to the application layer and the response received will depend on how the application is programmed to respond to empty packets. In this example, the application sends no response. However, if the destination UDP port is closed, the target should respond with an ICMP port unreachable (as seen in packets 4 and 8), that is sent by the UDP/IP stack of the target machine.

Most UDP scanners tend to use the standard “ICMP port unreachable” message to infer the status of a target port. However, this method can be completely unreliable when the target port is filtered by a firewall. In fact, in these cases the scanner will report the target port as open because of the absence of the ICMP message.

### 7.2.1.3 Common Port Scanning Pitfalls

UDP scanning can be problematic for several reasons. First, UDP scanning is often unreliable, as firewalls and routers may drop ICMP packets. This can lead to false positives and ports showing as open when they are, in fact, closed. Second, many port scanners do not scan all available ports, and usually have a pre-set list of “interesting ports” that are scanned. This means open UDP ports can go unnoticed. Using a protocol-specific UDP port scanner may help in obtaining more accurate results. Finally, penetration testers often forget to scan for open UDP ports, instead focusing on the “more exciting” TCP ports. Although UDP scanning can be unreliable, there are plenty of attack vectors lurking behind open UDP ports.

## 7.2.2 Port Scanning with Nmap

Nmap[^196] (written by Gordon Lyon, aka Fyodor) is one of the most popular, versatile, and robust port scanners available. It has been actively developed for over a decade and has numerous features beyond port scanning.

> *Some of the Nmap example scans we cover in this module are run using sudo*  
> *This is due to the fact that quite a few Nmap scanning options require access to raw sockets,* [^197]*which in turn require root privileges. Raw sockets allow for surgical manipulation of TCP and UDP packets. Without access to raw sockets,*

[^196]: (Nmap, 2019), http://nmap.org/  
[^197]: (Man7, 2017), http://man7.org/linux/man-pages/man7/raw.7.html

![](img/ec25e59d75726b7041242a56d3376832_183_0.png)

> *Nmap is limited as it falls back to crafting packets by using the standard Berkeley socket API.* [^198]

[^198]: Not explicitly cited in text but implied as footnote 198.

Let's explore some port scanning examples to get a better feel for Nmap and its options.

### 7.2.2.1 Accountability for Our Traffic

A default Nmap TCP scan will scan the 1000 most popular ports on a given machine. Before we start running scans blindly, let’s examine the amount of traffic sent by this type of scan. We'll scan one of the lab machines while monitoring the amount of traffic sent to the target host using **iptables**.[^199]

[^199]: Not explicitly cited in text but implied as footnote 199.

We will use several **iptables** options. First, we will use the `-I` option to insert a new rule into a given chain, which in this case includes both the **INPUT** (Inbound) and **OUTPUT** (Outbound) chains followed by the rule number. We will use `-s` to specify a source IP address, `-d` to specify a destination IP address, and `-j` to **ACCEPT** the traffic. Lastly, we will use the `-Z` option to zero the packet and byte counters in all chains.

Let's run those commands now:

```
kali@kali:~$ sudo iptables -I INPUT 1 -s 10.11.1.220 -j ACCEPT
kali@kali:~$ sudo iptables -I OUTPUT 1 -d 10.11.1.220 -j ACCEPT
kali@kali:~$ sudo iptables -Z
```
Listing 229 - Configuring our iptables rules for the scan

Now let's generate some traffic using **nmap**.

```
kali@kali:~$ nmap 10.11.1.220
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:20 EST
Nmap scan report for 10.11.1.220
Host is up (0.29s latency).
Not shown: 989 closed ports
PORT STATE SERVICE
21/tcp open ftp
53/tcp open domain
88/tcp open kerberos-sec
135/tcp open msrpc
139/tcp open netbios-ssn
389/tcp open ldap
445/tcp open microsoft-ds
464/tcp open kpasswd5
593/tcp open http-rpc-epmap
636/tcp open ldapssl
3268/tcp open globalcatLDAP
3269/tcp open globalcatLDAPSsl
3389/tcp open ms-wbt-server
Nmap done: 1 IP address (1 host up) scanned in 46.29 seconds
```
Listing 230 - Scanning an IP for the 1000 most popular TCP ports

The scan completed and revealed a few open ports.

Now let’s look at some **iptables** statistics to get an idea of how much traffic our scan generated. We will use the **-v** option to add some verbosity to our output, **-n** to enable numeric output, and **-L** to list the rules present in all chains:

```
kali@kali:~$ sudo iptables -vn -L
Chain INPUT (policy ACCEPT 1528 packets, 226K bytes)
 pkts bytes target prot opt in out source destination
1263 51264 ACCEPT all -- * * 10.11.1.220 0.0.0.0/0

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target prot opt in out source destination

Chain OUTPUT (policy ACCEPT 1323 packets, 191K bytes)
 pkts bytes target prot opt in out source destination
1314 78300 ACCEPT all -- * * 0.0.0.0/0 10.11.1.220
```
Listing 231 - Using iptables to monitor nmap traffic for a top 1000 port scan

According to this output, this default 1000-port scan has generated around 78 KB of traffic.

Let’s use **iptables -Z** to zero the packet and byte counters in all chains again and run another **nmap** scan using **-p** to specify ALL TCP ports:

```
kali@kali:~$ sudo iptables -Z
kali@kali:~$ nmap -p 1-65535 10.11.1.220
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:27 EST
Nmap scan report for 10.11.1.220
Host is up (0.00067s latency).
Not shown: 65507 closed ports
PORT STATE SERVICE
21/tcp open ftp
53/tcp open domain
88/tcp open kerberos-sec
135/tcp open msrpc
139/tcp open netbios-ssn
389/tcp open ldap
445/tcp open microsoft-ds
464/tcp open kpasswd5
593/tcp open http-rpc-epmap
636/tcp open ldapsssl
1291/tcp filtered seagullms
3268/tcp open globalcatLDAP
3269/tcp open globalcatLDAPssl
3389/tcp open ms-wbt-server
5722/tcp open msdfs
9389/tcp open adws
12777/tcp filtered unknown
46056/tcp filtered unknown
47001/tcp  open    winrm
...
Nmap done: 1 IP address (1 host up) scanned in 80.42 seconds
```

```
kali@kali:~$ sudo iptables -vn -L
Chain INPUT (policy ACCEPT 219K packets, 252M bytes)
 pkt  bytes  target     prot opt  in      out     source        destination
66243  2659K  ACCEPT    all  --  *      *      10.11.1.220   0.0.0.0/0

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkt  bytes  target     prot opt  in      out     source        destination

Chain OUTPUT (policy ACCEPT 85792 packets, 11M bytes)
 pkt  bytes  target     prot opt  in      out     source        destination
66768  4006K  ACCEPT    all  --  *      *      0.0.0.0/0    10.11.1.220
```
*Listing 232 - Using iptables to monitor nmap traffic for a port scan on ALL TCP ports*

A similar local port scan explicitly probing all 65535 ports generated about 4 MB of traffic, a significantly higher amount. However, this full port scan has discovered new ports that were not found by the default TCP scan.

The results above imply that a full Nmap scan of a class C network (254 hosts) would result in sending over 1000 MB of traffic to the network. In an ideal situation, a full TCP and UDP port scan of every single target machine would provide the most accurate information about exposed network services. However, the example above reveals the need to balance any traffic restrictions (such as a slow uplink), with the need to discover additional open ports and services, by using a more exhaustive scan. This is especially true for larger networks, such as a class A or B network assessment.

In the next section, we’ll explore some of Nmap’s various scanning techniques.

### 7.2.2.2 Stealth / SYN Scanning

Nmap’s preferred scanning technique is a SYN, or “stealth” scan.[^200] There are many benefits to using a SYN scan and as such, it is the default scan technique used when no scan technique is specified in an **nmap** command and the user has the required raw sockets privileges.

[^200]: (Nmap, 2019). https://nmap.org/book/synscan.html

SYN scanning is a TCP port scanning method that involves sending SYN packets to various ports on a target machine without completing a TCP handshake. If a TCP port is open, a SYN-ACK should be sent back from the target machine, informing us that the port is open. At this point, the port scanner does not bother to send the final ACK to complete the three-way handshake.

```
kali@kali:~$ sudo nmap -sS 10.11.1.220
Starting Nmap 7.70 ( https://nmap.org ) at 2019-03-04 11:27 EST
Nmap scan report for 10.11.1.220
Host is up (1.3s latency).
Not shown: 980 closed ports
PORT     STATE  SERVICE
21/tcp   open     ftp
53/tcp   open     domain
```
