# OffSec Penetration Testing with Kali Linux

21/tcp open
22/tcp open ssh OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol
2.0)

```
ssh-hostkey:
3072 56:57:11:d3:b5:dc:f1:d3:50:88:b8:ab:93:e2:29 (RSA)
256 64:f1:d2:f5:cb:b0:43:e0:76:b4:c3:96:19:a2:ba:f0:44 (ECDSA)
256 67:46:b3:27:96:a9:e3:48:e20:b3:98:7a:32 (ED25519)
```

```
23/tcp closed telnet
25/tcp closed smtp
53/tcp closed domain
80/tcp open Apache http 2.4.1 ((Ubuntu))
http-server-header: Apache/2.4.1 (Ubuntu)
|http_title: Under Construction
110/tcp closed pop3
111/tcp closed rpcbind
```

> Listing 65 - Using nmap to perform a twenty port scan, saving the output in greppable format

The 20 nmap results generated using the /usr/share/nmap/map-services file, which uses a simple format of three whitespace-separated columns. The first is the name of the service, the second contains the number and protocol, and the third is the "frequency". Everything after the third column is ignored, which is typically used for comments as shown by the use of pound sign (#). The frequency is based on how often the port was found during periodic scans of the internet.²⁶³

```
kali@kali:~# cat /usr/share/nmap/map-services
finger 79/udp 0.008956 # www -http | World | Wide Web HTTP
http 80/tcp 0.068090 # World Wide Web HTTP
http 80/tcp 0.484143
http 80/udp 0.035767 # World Wide Web HTTP
hosts2- 81/tcp 0.012086 # HOSTS2 Name Server
hosts2-ns 81/udp 0.001085 # HOSTS2 Name Server
```

> Listing 66 - The nmaps file showing the open frequency of TCP port 80

At this point, we could conduct a more exhaustive scan against machines that are service-rich or otherwise interesting.

There are many ways we can be creative with our scanning to conserve bandwidth and lower our profile, as as interesting discovery techniques²⁶⁴ that are worth further research.

We have now scanned hosts that revealed a few services, so we can now guess the nature of the target's operating system. Luckily for us, Nmap is already shipped with an OS Fingerprinting option.

OS fingerprinting²⁶⁵ can be enabled with the -O option. This feature attempts to guess the target's operating system by inspecting returned packets. This works because operating systems use different implementations of the TCP/IP stack (such as varying default TTL values

²⁶³ (Nmap, 2022), https://nmap.org/book/nmap-services.html
²⁶⁴ (Nmap, 2022), https://nmap.org/book/man-host-discovery.html
²⁶⁵ (Nmap, 2022), https://nmap.org/book/osdetect.html

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

148