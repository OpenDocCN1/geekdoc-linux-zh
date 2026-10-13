```
```text
44(0) win 8192 <mss 1460> (DF)
23:39:41.703732 cstl×001.bwc.org.8083 > shjws159.bwc.org.1879: S 2162833501:2162
833501(0) ack 43808645 win 30600 <mss 1460> (DF)
23:39:41.704168 shjws159.bwc.org.1879 > cstl×001.bwc.org.8083: . ack 1 win 8760
(DF)
23:39:41.705443 cstl×001.bwc.org.8083 > shjws159.bwc.org.1879 > saturn.bwc.org.657: udp 80
23:39:41.706955 shjws159.bwc.org.1879 > cstl×001.bwc.org.8083: P 1:451(450) ack
1 win 8760 (DF)
23:39:41.707061 cstl×001.bwc.org.8083 > shjws159.bwc.org.1879: . ack 451 win 306
6 (DF)
23:39:41.709400 cstl×001.bwc.org.8083 > shjws159.bwc.org.1879: . 1:1461(1460) ac
k 451 win 32120 (DF)
23:39:41.714870 saturn.bwc.org.657 > cstl×001.bwc.org.888: udp 60
23:39:41.826279 shjws159.bwc.org.1879 > cstl×001.bwc.org.8083: . ack 1461 win 87
60 (DF)
23:39:41.826379 cstl×001.bwc.org.8083 > shjws159.bwc.org.1879: FP 1461:1653(192)
ack 451 win 32120 (DF)
23:39:41.826924 shjws159.bwc.org.1879 > cstl×001.bwc.org.8083: . ack 1654 win 85
68 (DF)
23:39:41.849289 shjws159.bwc.org.1879 > cstl×001.bwc.org.8083: . 451:451(0) ack
1654 win 8568 (DF)
23:39:41.849381 cstl×001.bwc.org.8083 > shjws159.bwc.org.1879: . ack 452 win 321
19 (DF)
23:39:41.853015 192.115.144.85.1037 > cstl×001.bwc.org.telnet: . ack 3722964229
win 8495 (DF)
23:39:41.853092 cstl×001.bwc.org.telnet > 192.115.144.85.1037: P 1:29(28) ack 0
win 32696 (DF)
23:39:41.853936 cstl×001.bwc.org.889 > saturn.bwc.org.657: udp 84
23:39:41.864642 saturn.bwc.org.657 > cstl×001.bwc.org.889: udp 32
23:39:41.865619 cstl×001.bwc.org.2178 > bwcd×001.domain: 9100+ (45)
23:39:41.867214 bwcd×001.domain > cstl×001.bwc.org.2178: 9100 NXDomain 0/1/0 (99)
)
23:39:41.868653 cstl×001.bwc.org.890 > saturn.bwc.org.657: udp 76
23:39:41.870835 saturn.bwc.org.657 > cstl×001.bwc.org.890: udp 52
23:39:42.159239 192.115.144.85.1037 > cstl×001.bwc.org.telnet: . ack 29 win 8467
(DF)
23:39:42.496991 cstl×001.bwc.org.890 > ospfvl2-hello 44: rtrid 22.98.192.
0 backbone [ ospf ] [tos 0xc0] [ttl 1]
23:39:42.496972 cstl×001.bwc.org.891 > saturn.bwc.org.657: udp 80
23:39:42.505288 saturn.bwc.org.657 > cstl×001.bwc.org.891: udp 64
23:39:42.505972 cstl×001.bwc.org.892 > saturn.bwc.org.657: udp 80
23:39:42.508210 saturn.bwc.org.657 > cstl×001.bwc.org.892: udp 72
23:39:42.508904 cstl×001.bwc.org.893 > saturn.bwc.org.657: udp 80
23:39:43.000856 saturn.bwc.org.657 > cstl×001.bwc.org.893: udp 32
23:39:43.001115 cstl×001.bwc.org.2178 > bwcd×001.domain: 9101+ (42)
23:39:43.001727 bwcd×001.domain > cstl×001.bwc.org.2178: 9101 NXDomain 0/1/0 (116)
```
```

As you can see above, each packet is time stamped. The fields in each entry vary depending on the protocol type (such as UDP or TCP).

For UDP packets, entries are of the following general format:

`<time stamp> <source host>.<port> > <destination host>.<port>: \\  <other optional <fields> packet length`

For port numbers that have names associated with them, the names are printed instead. The following two lines show a domain name query and response: