remote system where a GUI would be slow, inefficient, and not very stealthy.

To start tcpdump, enter; 177 \| Page

```
```
root@kali-2019:~# tcpdump
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
16:07:04.062010 IP 192.168.0.235.57656 > 239.255.255.250.1900: UDP, length 174
16:07:04.064714 ARP, Request who-has (gateway) tell kali-2019.1299 (length 28
16:07:04.06517 ARP, Reply gateway is-at b0:be:76:08:b5:3c (oui Unknown), length 46
16:07:04.066326 IP kali-2019.35533 > gateway.domain: 15131+ PTR? 250.255.255.239.in-addr.arpa. (46)
16:07:04.080311 IP gateway.domain > kali-2019.35533: 15132 NXdomain 0/1/0 (103)
16:07:04.080872 IP kali-2019.59304 > gateway.domain: 50202+ PTR? 233.0.168.192.in-addr.arpa. (44)
16:07:04.095554 IP gateway.domain > kali-2019.59304: 50202 NXdomain 0/0/0 (44)
16:07:04.096001 IP kali-2019.43942 > gateway.domain: 28517+ PTR? 1.0.168.192.in-addr.arpa. (42)
16:07:04.111351 IP gateway.domain > kali-2019.43942: 28517 NXdomain 0/0/0 (42)
16:07:04.111687 IP kali-2019.42176 > gateway.domain: 23623+ PTR? 173.0.168.192.in-addr.arpa. (44)
16:07:04.126380 IP gateway.domain > kali-2019.42176: 23623 NXdomain 0/0/0 (44)
16:07:05.006342 IP 192.168.0.235.57656 > 239.255.255.250.1900: UDP, length 174
16:07:07.507418 IP kali-2019.59304 > 224.0.0.251.5390: PTR? (QM) 192.168.0.152.in-addr.arpa. (44)
16:07:07.585756 IP kali-2019.44754 > gateway.domain: 30429+ PTR? 251.0.0.224.in-addr.arpa. (42)
16:07:07.587774 IP gateway.domain > kali-2019.44754: 30433 PTR? 224.0.0.251.192.168.0.152.in-addr.arpa. (81)
16:07:07.601171 IP gateway.domain > kali-2019.44754: 30429 NXdomain 0/1/0 (99)
```
```

![](bbox=[0.13, 0.425, 0.87, 0.585])

kali >tcpdump

As you can see, as soon as you enter the command tcpdump, packets begin to flow across your screen.

These packets are largely communication between your Kali system and the LAN gateway.

Let's try creating some traffic to analyze. For instance, let's try sending a ping (ICMP echo request) to your Windows 7 system from one terminal and run tcpdump from the other.

kali > ping 192.168.0.114