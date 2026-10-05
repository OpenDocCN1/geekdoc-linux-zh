# OffSec

session layer protocol and service that allows computers on a local network to communicate with other. While modern implementations of SMB work without NetBIOS, NetBIOS over TCP (NBT) is required for backward compatibility and these are enabled together. This also means the enumeration of these two services often hand-in-hand. These services can be scanned with tools like nmap, using syntax similar to the following:

```
kali@:$ nmap -v p 139,445 -oG smb.txt 192.168.50.1-254
```

```
kali@:$ cat smb.txt
# Nmap 7.92 initiated Thu Mar 17 06:03:12 2022 as: nmap -v -p 139,445 -oG smb.txt
192.168.50.1-254
# Ports scanned: 2(139,445) UDP(0); SCTP(0); PROTOCOLS()
Host: 192.168.50.1 () Status: Down

Host: 192.168.50.21 () Ports: 139/closed/tcp/netbios-ssn///,
445/closed/tcp/netbios-ssn///,

Host: 192.168.50.217 () Ports: 139/closed/tcp/netbios-ssn///,
445/closed/tcp/netbios-ssn///,
# Nmap done at Thu Mar 17 06:03:18 2022 - 254 IP addresses (1 hosts up) scanned in
6.17 seconds
```

> Listing 73 - Using nmap to scan for the NetBIOS service

We saved the output into a text file, which revealed hosts with ports 139 and 445.
There are other, more specialized tools for identifying NetBIOS information, such as nbtscan. We can use this query to fetch NetBIOS name for valid hosts, identifying the operating UDP port with the -f option.

```
kali@:$ nbtscan -r 192.168.50.0/24
Doing NBT name scan for addresses from 192.168.50.0/24
```

| IP address | NetBIOS Name | Server | User | MAC address |
|---|---|---|---|--|
| 192.168.50.124 | SAMBA | <server> | SAMBA | 00:00:00:00:00:00 |
| 192.168.50.134 | SAMBAWEB | <server> | SAMBAWEB | 00:00:00:00:00:00 |

> Listing 74 - Using nbtscan to collect additional NetBIOS information

The scan revealed two NetBIOS names belonging to two hosts. This kind of information can be used to improve the context of the scanned hosts, as NetBIOS names are often very descriptive about the host within the organization. This data can feed our information-gathering cycle by further discussions.
Nmap also offers many useful NSE scripts that we can use to discover and enumerate SMB services. We'll find them in the /usr/share/nmap/scripts/smb* directory.

```
kali@:$ ls -l /usr/share/nmap/scripts/smb*
/usr/share/nmap/scripts/smb2-capabilities.nse
/usr/share/nmap/scripts/smb2-security-mode.nse
```

371 (Wikipedia, 2022), https://en.wikipedia.org/wiki/NetBIOS_over_TCP/IP