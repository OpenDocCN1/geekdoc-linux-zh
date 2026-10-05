# OffSec

Penetration Testing with Kali Linux

| 1.3.6.1.2.25.1.6.0 | System Processes |
| 1.3.6.1.2.25.42.1.2 | Running Programs |
| 1.3.6.1.2.25.42.1.4 | Processes Path |
| 1.3.6.1.2.25.2.3.1.4 | Storage Units |
| 1.3.6.1.2.25.6.3.1.2 | Software Name |
| 1.3.6.1.4.1.77.2.25 | User Accounts |
| 1.3.6.1.2.25.6.13.13.3 | TCP Local Ports |

Table 2 - Windows MIB values

Scan for open SNMP points, we can run nmap, using the -U option to perform UDP scanning and the -n option to limit the hosts and display only points.

```
kali@kali:~$ sudo nmap -sU --open -p 161 192.168.50.254 -o open-snmp.txt
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-14 06:02 EDT
Nmap scan report for 192.168.50.151
Host is up (0.10s latency).
```

```
PORT STATE SERVICE
161/udp snmp

map done: 1 IP address (1 host) scanned in 0.49 seconds
```

Listing 84 - Using nmap to perform a SNMP scan

Alternatively, we can use a tool like onesixty² which will attempt a brute force attack against a list of IP addresses. First, we must build text files containing community strings and the IP addresses we wish to scan.

```
kali@kali:~$ echo public > community
kali@kali:~$ echo private > community
kali@kali:~$ echo manager > community
```

```
kali@kali:~$ for ip in $(seq 1 254); do echo 192.168.50.$ip; done > ips

kali@kali:~$ onesixty -c community -i ips
Scanning 254 hosts, 3 communities
192.168.50.151 [public] Hardware: Intel Core i6 Model 6 Stepping 1 AT/AT
COMPATIBLE - Software: Windows Version 6.3 (Build 17763) Multiprocessor Free)
...
```

Listing 85 - Using onesixty to brute force community strings

Once we find SNMP services, we can start querying them for specific MIB data that might be interesting.

We can probe and query SNMP values using a tool such as snmpwalk, provided we know the SNMP read-only community string, which in most cases is "public".

Using some of the MIB values provided in Table 2, we can attempt to enumerate the corresponding values. Let's try the following example against a known machine in the labs, which has a SNMP port exposed with the community string "public". This command enumerates the entire MIB tree using the -c option to specify the community string, and -v to

³⁷⁵ (Alexander Sotirov, 2008), http://www.freedom.org/software/onesixty/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

159