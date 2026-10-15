
```text
root@kali-2019:~# tcpdump
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
16:07:04.062010 IP 192.168.0.235.57656 > 239.255.255.250.1900: UDP, length 174
16:07:04.064714 ARP, Request who-has (gateway) tell kali-2019.1299 (length 28)
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

`kali > tcpdump`

如图所示，只要你输入命令 `tcpdump`，数据包就会开始在你的屏幕上流动。

这些数据包主要是你的 Kali 系统与局域网网关之间的通信。

让我们尝试创建一些流量进行分析。例如，让我们尝试从一个终端向你的 Windows 7 系统发送一个 `ping`（ICMP 回显请求），同时从另一个终端运行 `tcpdump`。

`kali > ping 192.168.0.114`

`kali > tcpdump`

让我们放大 `tcpdump` 屏幕，以便能看清那里的细节。

```text
root@kali-2019:~# tcpdump
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
16:12:05.770020 IP kali-2019 > 192.168.0.114: ICMP echo request, id 25881, seq 3, length 64
16:12:05.770314 IP 192.168.0.114 > kali-2019: ICMP echo reply, id 25881, seq 3, length 64
16:12:05.770836 IP kali-2019.44328 > _gateway.domain: 39663+ PTR? 114.0.168.192.in-addr.arpa. (44)
16:12:05.780317 IP _gateway.domain > kali-2019.44328: 39663 NXDOMAIN 0/0/0 (44)
16:12:05.798799 IP kali-2019.37659 > _gateway.domain: 53089+ PTR? 173.0.168.192.in-addr.arpa. (44)
16:12:05.804341 IP _gateway.domain > kali-2019.37659: 53089 NXDOMAIN 0/0/0 (44)
16:12:05.804701 IP kali-2019.39714 > _gateway.domain: 47919+ PTR? 1.0.168.192.in-addr.arpa. (44)
```
