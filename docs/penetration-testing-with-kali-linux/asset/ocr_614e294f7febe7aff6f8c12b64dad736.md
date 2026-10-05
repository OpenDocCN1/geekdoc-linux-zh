# OffSec

Penetration Testing with Kali Linux

| PORT | STATE | SERVICE |
|---|---|---|
| 123/udp | open | ntp |
| 389/udp | open | ldap |

Nmap done: 1 IP address (1 host) scanned in 22.49 seconds

Listing 60 - Using nmap to perform a UDP scan

The UDP scan (-SU) can also be used in conjunction with a TCP SYN scan (-SS) to build a complete picture of our target.

```
kali@kali:~ sudo nmap -SU -sS 192.168.50.149
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-09 08:16 EST
Nmap scan report for 192.168.50.149
Host is up (0.12s latency).
Not shown: 989 closed ports (reset), 977 closed udp ports (port-unreachable)
```

| PORT | STATE | SERVICE |
|---|---|---|
| 53/tcp | open | domain |
| 88/tcp | open | kerberos-sec |
| 135/tcp | open | msprc |
| 139/tcp | open | netbios-ssn |
| 389/tcp | open | ldap |
| 445/tcp | open | microsoft-ds |
| 464/tcp | open | kpasswd5 |
| 593/tcp | open | http-rpc-epmam |
| 636/tcp | open | ldapssl |
| 3268/tcp | open | globalcatLDAP |
| 3269/tcp | open | globalcatLDAPS |
| 53/udp | open | domain |
| 123/udp | open | ntp |
| 389/udp | open | ldap |

Listing 61 - Using nmap to perform a combined UDP and SYN scan

Our TCP and UDP scan revealed additional open udp ports, disclosing which services are running on the target host.

We can extend what we have learned from a single host and apply it to a full network range through Network Switching.

To deal with large volumes of hosts, or otherwise to conserve network traffic, we can attempt to probe targets using Network Switching techniques in which we begin with broad ranges, then use more specific scans against hosts of interest.

When performing a network scan with Nmap using the -sn option, the host discovery process consists of more than just sending an ICMP echo request. Nmap also sends a TCP SYN packet to port 443, a TCP ACK packet to port 80, and an ICMP timestamp request to verify whether a host is available.

```
kali@kali:~ nmap -sn 192.168.50.1-253
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-10 03:19 EST
Nmap scan report for 192.168.50.8
Host is up (0.12s latency).
Nmap scan report for 192.168.50.8
```

Nmap done: 254 IP addresses (13 hosts) scanned in 3.74 seconds

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

146