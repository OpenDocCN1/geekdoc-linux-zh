-x set the more fragments flag in the IP header

-y set the don't fragment flag in the IP header Please also note that the default mode of hping3 is TCP packets. Unlike nmap that defaults to sending an ICMP ping, which can often be blocked by firewalls and gateways.

The screenshot above shows us even more options. I’d like to draw your attention to the following:

-p destination port,

-Q get the TCP sequence number,

-tcp-timestamp gets the TCP timestamp and converts it into days, hours and minutes.

Also note that we can set any of the TCP flags (S,A,F,P, R, U) as well as the XMAS (-X) scan (flags P,U,F set).

88 | P a g e

```
root@kali-2019:~# hping3 -S 192.168.0.114 -p 80
Hping 192.168.0.114 (eth0 192.168.0.114): S set, 40 headers + 0 data bytes
len=46 ip=192.168.0.114 ttl=128 DF id=1857 sport=80 flags=RA seq=0 win=0 rtt=6.8 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1858 sport=80 flags=RA seq=1 win=0 rtt=5.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1859 sport=80 flags=RA seq=2 win=0 rtt=4.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1860 sport=80 flags=RA seq=3 win=0 rtt=3.2 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1861 sport=80 flags=RA seq=4 win=0 rtt=3.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1862 sport=80 flags=RA seq=5 win=0 rtt=2.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1863 sport=80 flags=RA seq=6 win=0 rtt=2.2 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1864 sport=80 flags=RA seq=7 win=0 rtt=2.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1865 sport=80 flags=RA seq=8 win=0 rtt=1.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1866 sport=80 flags=RA seq=9 win=0 rtt=9.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1867 sport=80 flags=RA seq=10 win=0 rtt=7.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1868 sport=80 flags=RA seq=11 win=0 rtt=7.7 ms
```

```
root@kali-2019:~# hping3 -S 192.168.0.114 -p 445
Hping 192.168.0.114 (eth0 192.168.0.114): S set, 40 headers + 0 data bytes
len=46 ip=192.168.0.114 ttl=128 DF id=1874 sport=445 flags=SA seq=0 win=8192 rtt=8.7 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1874 sport=445 flags=SA seq=1 win=8192 rtt=7.8 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1875 sport=445 flags=SA seq=2 win=8192 rtt=6.7 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1876 sport=445 flags=SA seq=3 win=8192 rtt=6.0 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1877 sport=445 flags=SA seq=4 win=8192 rtt=5.2 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1878 sport=445 flags=SA seq=5 win=8192 rtt=4.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1879 sport=445 flags=SA seq=6 win=8192 rtt=4.8 ms
```