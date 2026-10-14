**Table 14.1 — netstat Column Heading Definitions**

| Heading | Definition |
|---|---|
| Iface | Interface |
| MTU | Maximum Transmission Unit<br>Number is in bytes and default for Ethernet is 1500 |
| Met | Metric<br>Default is zero<br>Utilized by routing information protocol |
| RX-OK/TX-OK | Packets received/transmitted error-free |
| RX-ERR/TX-ERR | Packets received/transmitted with errors |
| RX-DRP/TX-DRP | Packets received/transmitted/dropped |
| RX-OVR/TX-OVR | Packets received/transmitted/lost due to overrun |
| Flg | Flags set for interface |

```
```text
[insert] /sbin/ifconfig
eth0      Link encap:Ethernet  HWaddr 00:60:97:C1:04:F4
          inet addr:130.207.226.122  Bcast:130.207.226.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:0
          RX packets:36267 errors:0 dropped:0 overruns:0 frame:0
          TX packets:27937 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:100
          Interrupt:5 Base address:0x300

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:3924  Metric:0
          RX packets:197870 errors:0 dropped:0 overruns:0 frame:0
          TX packets:197870 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0

[insert]
```
```

*Figure 14.6*  ifconfig on Red Hat Linux 6.0.