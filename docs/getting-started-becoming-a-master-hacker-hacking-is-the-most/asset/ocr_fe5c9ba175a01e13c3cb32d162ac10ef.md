```
```
root@kali-2019:~ # hping3 -S 192.168.0.114 -p ++1
HPING 192.168.0.114 (eth0 192.168.0.114): S set, 40 headers + 0 data bytes
len=46 ip=192.168.0.114 ttl=128 DF id=1883 sport=1  flags=RA seq=0 win=0 rtt=4.4 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1884 sport=2  flags=RA seq=1 win=0 rtt=4.8 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1885 sport=3  flags=RA seq=2 win=0 rtt=4.0 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1886 sport=4  flags=RA seq=5 win=0 rtt=4.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1887 sport=5  flags=RA seq=4 win=0 rtt=3.0 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1888 sport=6  flags=RA seq=5 win=0 rtt=2.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1889 sport=7  flags=RA seq=7 win=0 rtt=1.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1890 sport=8  flags=RA seq=7 win=0 rtt=9.4 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1891 sport=9  flags=RA seq=8 win=0 rtt=7.6 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1892 sport=10 flags=RA seq=9 win=0 rtt=6.7 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1893 sport=11 flags=RA seq=10 win=0 rtt=6.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1894 sport=12 flags=RA seq=11 win=0 rtt=6.1 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1895 sport=13 flags=RA seq=12 win=0 rtt=5.9 ms
len=46 ip=192.168.0.114 ttl=128 DF id=1896 sport=14 flags=RA seq=13 win=0 rtt=5.9 ms
```
```

```
```
root@kali:~$ hping3 -S -f 192.168.1.116 -p 445
HPING 192.168.1.116 (eth0 192.168.1.116): S set, 40 headers + 0 data bytes
len=46 ip=192.168.1.116 ttl=128 DF id=18306 sport=445 flags=SA seq=0 win=8192 rt
 t=1.8 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18307 sport=445 flags=SA seq=1 win=8192 rt
 t=1.5 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18308 sport=445 flags=SA seq=2 win=8192 rt
 t=1.3 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18309 sport=445 flags=SA seq=3 win=8192 rt
 t=1.1 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18310 sport=445 flags=SA seq=4 win=8192 rt
 t=1.4 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18311 sport=445 flags=SA seq=5 win=8192 rt
 t=1.8 ms
len=46 ip=192.168.1.116 ttl=128 DF id=18312 sport=445 flags=SA seq=6 win=8192 rt
 t=6.5 ms
```
```

![](bbox=[0.13, 0.59, 0.88, 0.82])

This scan starts at port 1 and increments by 1 (++1) to test each port for a response.