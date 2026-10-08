# Capturing from ha

File    Edit    View    Go    Capture    Analyze    Statistics    Telephony    Wireless    Tools    Help

Apply a display filter ... `<Ctrl-/>`    Expression...

No.    Time    Source    Destination    Protocol    Length    Info
86    10.042153002    192.168.1.1    239.255.255.250    SSDP    316    NOTIFY * HTTP/1.1
87    10.045421866    192.168.1.1    239.255.255.250    SSDP    379    NOTIFY * HTTP/1.1
88    10.049329584    192.168.1.1    239.255.255.250    SSDP    379    NOTIFY * HTTP/1.1
89    10.052280616    192.168.1.1    239.255.255.250    SSDP    316    NOTIFY * HTTP/1.1
90    10.055588933    192.168.1.1    239.255.255.250    SSDP    307    NOTIFY * HTTP/1.1

```
Frame 1: 381 bytes on wire (3048 bits), 381 bytes captured (3048 bits) on interface 0
Ethernet II, Src: Cisco-Li_97:4f:48 (00:25:9c:97:4f:48), Dst: IPv4cast_7f:ff:fa (01:00:5e:7f:ff:fa
Internet Protocol Version 4, Src: 192.168.1.1, Dst: 239.255.255.250
User Datagram Protocol, Src Port: 1900, Dst Port: 1900
Simple Service Discovery Protocol
```

```
0000    01 00 5e 7f ff fa 00 25 9c 97 4f 48 08 00 45 00  .,^. .%_OH..E.
0016    01 6f 99 d6 00 00 04 11 6a 04 c0 a8 01 01 cf ff  .o. .............
0029    ff fa 07 6c 07 6c 01 5b 2a c0 4e 4f 54 49 46 59  .l.l.[*.NOTIFY
0038    20 2a 20 48 44 54 50 2f 31 2e 31 0d 0a 48 6f 73   * HTTP/1.1..Hos
0044    74 3a 32 33 39 2e 32 35 35 2e 32 35 35 0d 0a 73  t:239.25.255.25
0056    30 3a 31 39 30 30 0d 0a 4e 54 75 72 6e 3a 73      0:1900.. NTurn:s
0064    63 6d 65 6c 6c 61 3a 69 66 69 61 6c 6c 69 61      chemas-w ifiallia
0078    66 63 65 2d 6f 72 67 3a 73 65 72 76 69 63 65 3a   nce-org: service:
```

ha: live capture in progress>    Packets: 90 - Displayed: 90 (100.0%)    Profile: Default