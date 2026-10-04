Attacking and Defending DNS • Chapter 8 443

```
t ./main
netstat -lp
```

Active Internet connections (only servers) Foreign Address

| State Proto Recv-Q Send-Q Local Address PID/Program name Address |
|---|---|---|---|---|---|---|---||
| tcp 0 0 10.0.32.163:domain | *: |
| LISTEN | 26096/dnscache | | |
| udp 0 0 10.0.32.163:domain | *: |
| 26096/dnscache | | |

+   5. You have a local DNS resolver server running. To grant additional hosts resolver access, add their IPs. For example, to add 1.2.3/24, you would add a blank classfull descriptive file (1.2.3) in the approved ip resolver directory (restart of dnscache is unnecessary thanks to daemon-tools):
    touch /etc/dnscache/root/ip/1.2.3

# TinyDNS Configuration

Configuration of TinyDNS can be done manually or through the configuration maker:

+   1. Run the configuration maker. Replace z.y.x.w with the appropriate IP address. Note that dnscache and TinyDNS cannot run on the same IP:
    tinydns-conf tinydns dnslog /etc/tinydns 1.2.3.5
2. Just like dnscache, make a symbolic link to the service directory so daemontools can initiate TinyDNS:
    ln -s /etc/tinydns /service
3. After starting TinyDNS, you need to add zone configurations:
    vim /etc/tinydns/root/data
4. This file will include all zones. Insert the domains that will be hosted on this server. The syntax is very different from that of BIND or others. The dot (.) symbol is a nameserver record:
    .example.com::ns1.example.com

![](bbox=[0.706, 0.943, 0.933, 0.968])