
## route

Purpose: Display and configure TCP/IP routes.

Usage syntax: `route [OPTIONS]`

```
$ route -n
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.101.0 0.0.0.0 255.255.255.0 U 0 0 0 wlan0
10.10.1.0 0.0.0.0 255.255.255.0 U 0 0 0 eth0
0.0.0.0 10.10.1.1 0.0.0.0 UG 0 0 0 eth0
0.0.0.0 192.168.101.1 0.0.0.0 UG 0 0 0 wlan0
```

Displaying routing tables

The `route` command displays and configures network routes. In the above example, executing `route -n` displays the local system’s routing table.

The `add` and `del` options can be used to add or delete static routes as shown in the next example.

```
# route add -net 10.10.2.0/24 gw 10.10.1.1 eth0
# route del -net 10.10.2.0/24
```

Adding and removing static TCP/IP routes

Common usage examples:

| Command | Description |
| :--- | :--- |
| `route -n` | Display routing tables |
| `route add [ROUTE]` | Add the specified static route |
| `route del [ROUTE]` | Delete the specified static route |

## ifstat

**Purpose**: Display network interface statistics.

**Usage syntax**: `ifstat [DELAY] [COUNT]`

```
$ ifstat 2 10
eth1
KB/s in KB/s out
0.02 0.04
0.02 0.04
10.68 0.86
44.49 2.93
3.45 7.95
2.33 48.46
0.40 0.86
0.04 0.11
3.26 0.58
0.02 0.04
```

Displaying network interface statistics using ifstat

`ifstat` displays network interface statistics. It can be used to monitor network interface activity over a period of time. In the above example, executing `ifstat 2 10` displays interface statistics every two seconds for ten iterations.

**Note** If no arguments are specified, `ifstat` will continuously display network utilization until interrupted (by pressing CTRL + C).

- `ifstat`: Continuously display network utilization
- `ifstat [DELAY]`: Update results at the specified interval
- `ifstat [DELAY] [COUNT]`: End after reaching the specified count

## tcpdump

**Purpose:** Displays raw traffic on a network interface.

**Usage syntax:** `tcpdump [OPTIONS]`

```
# tcpdump
listening on eth0, link-type EN10MB (Ethernet), capture size 96 bytes
05:59:05.027107 arp who-has 10.10.1.242 tell 1t-cad12-01.dontfearthecommandline.com
05:59:05.028261 IP dt-office-27.dontfearthecommandline.com.50999 > exchange-01.dontfearthecommandline.com.domain: 9454+ PTR?
242.1.10.10.in-addr.arpa. (42)
05:59:05.028459 arp who-has dt-office-27.dontfearthecommandline.com tell exchange-01.dontfearthecommandline.com
05:59:05.028475 arp reply dt-office-27.dontfearthecommandline.com is-at 00:21:70:ac:ff7e (oui Unknown)
...
18 packets captured
303 packets received by filter
0 packets dropped by kernel
```

Using the tcpdump command to capture network traffic

**tcpdump** displays network packets sent and received to and from the local system. It can be helpful in monitoring network conditions or troubleshooting connectivity problems.

In the above example, **tcpdump** captures network traffic on the `eth0` interface. Information on each packet is then displayed on the screen. The capture will continue until interrupted (by pressing `CTRL + C`).

> **Tip**
> Output from **tcpdump** *can be difficult to interpret*. *A free utility called Wireshark is available that can be used to import* **tcpdump** *packet captures for easy viewing.* *Wireshark is available for* Linux, *Mac OS* X*, and Windows systems. Visit* www.wireshark.com *for more information.*

**Common usage examples:**

| Command | Description |
| :--- | :--- |
| `tcpdump` | Display network traffic on the screen |
| `tcpdump > [FILE]` | Save the packet capture to a file |
| `tcpdump -i [INTERFACE]` | Capture traffic on the specified interface |
| `tcpdump -vv` | Display verbose packet information |
| `tcpdump -c [COUNT]` | Stop after receiving the specified number of packets |

## dhclient

Purpose: DHCP client for Linux and BSD systems.

**Usage syntax:** `dhclient [OPTIONS] [INTERFACE]`

```bash
# dhclient eth0
Listening on LPF/eth0/00:21:70:ac:f7:e7
Sending on   LPF/eth0/00:21:70:ac:f7:e7
Sending on   Socket/fallback
DHCPREQUEST of 10.10.1.100 on eth0 to 255.255.255.255 port 67
DHCPOFFER  of 10.10.1.100 from 10.10.1.45
bound to 10.10.1.100 -- renewal in 37193 seconds.
```

_Using dhclient to request a DHCP address_

`dhclient` is a client for requesting an IP address from a DHCP server. The above example demonstrates using the `dhclient` command to request an IP address for the `eth0` interface.

> > **Tip**
> _To release a DHCP address, execute `dhclient -r` on the command line._

**Common usage examples:**

| Command | Description |
| :--- | :--- |
| `dhclient [INTERFACE]` | Request an IP address from the DHCP server |
| `dhclient -r [INTERFACE]` | Release an assigned IP address |

## nmap

**Purpose:** Scan TCP/IP ports on network systems.

**Usage syntax:** `nmap [OPTIONS] [HOST]`

```
# nmap -O 10.10.1.70

Starting Nmap 5.00 ( http://nmap.org ) at 2010-05-06 16:55 CDT
Interesting ports on 10.10.1.70:
Not shown: 995 closed ports
PORT	STATE	SERVICE
135/tcp	open	msrpc
139/tcp	open	netbios-ssn
445/tcp	open	microsoft-ds
5800/tcp	open	vnc-http
5900/tcp	open	vnc
MAC Address: 00:1A:A0:05:6B:19 (Dell)
Device type: general purpose
Running: Microsoft Windows XP
OS details: Microsoft Windows XP SP2 or SP3, or Windows Server 2003
Network Distance: 1 hop

OS detection performed. Please report any incorrect results at
http://nmap.org/submit/.
Nmap done: 1 IP address (1 host up) scanned in 2.94 seconds
```

Using the nmap command to scan a network host

**nmap** is a network scanning utility. It can be used to evaluate security and troubleshoot network connectivity issues. In the above example, the **nmap** command is used to identify the operating system and open ports on the specified target host.

> **Tip**
> For the best results, use **nmap** as the root user or via the *sudo* command. This allows **nmap** to have access to have unrestricted access to system resources when performing network scans.

**Common usage examples:**

| Command | Description |
| :--- | :--- |
| `nmap [HOST]` | Display open ports on the specified host |
| `nmap -PN [HOST]` | Do not ping the target before scanning |
| `nmap -O [HOST]` | Display the operating system of the target system |
| `nmap -A [HOST]` | Perform an aggressive scan |

## telnet

Purpose: Client for connecting to remote servers via the telnet protocol.

Usage syntax: `telnet [OPTIONS] [HOST]`

```
$ telnet myserver
login: nick
password: ******
$
```

Connecting to a remote system using the telnet command

The **telnet** command is used to connect to remote systems via the telnet protocol. The above example demonstrates connecting to a remote system using **telnet**. Once connected to the remote system you can execute commands as if you were logged into the system locally.

> **Note**
> **Telnet is an insecure legacy protocol and has largely been replaced by SSH for security reasons. Usernames, passwords, and other sensitive information transmitted via telnet are sent in plain text making it very easy for hackers to capture. Avoid using telnet whenever possible, especially when communicating over untrusted networks such as the internet.**

Common usage examples:

| Command | Description |
| :--- | :--- |
| `telnet [HOST]` | Start a telnet session to a remote system |

## ssh

Purpose: Client for connecting to remote servers via the SSH protocol.

Usage syntax: `ssh [OPTIONS] [HOST]`

```bash
$ ssh myserver
nick@myserver's password: ******
$
```

Using the ssh command to connect to a remote system

The `ssh` command is used to connect to remote systems via the SSH protocol. SSH creates an encrypted connection between two systems and provides a secure channel for communication. This helps prevent “man in the middle” hackers from being able to capture sensitive information (such as usernames and passwords) when connecting to remote systems.

| Tip | PuTTY, a free SSH and telnet client for Windows, can be downloaded at www.chiark.greenend.org.uk/~sgtatham/putty/. This allows you to connect to remote Unix, Linux, and BSD servers directly from Windows systems. |

Common usage examples:

```
ssh [HOST]              # Start an SSH session to a remote system
ssh -1 [USER] [HOST]    # Login as the specified user on the target system
ssh -C [HOST]           # Enable compression (for slow connections)
```
