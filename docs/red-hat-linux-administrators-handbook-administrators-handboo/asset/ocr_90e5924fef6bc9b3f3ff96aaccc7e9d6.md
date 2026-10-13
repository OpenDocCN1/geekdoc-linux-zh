3. To start the alias device, run ifconfig eth0:0 up, and you should see output similar to the following:

```
lo Link encap:Local Loopback
 inet addr:127.0.0.1 Bcast:127.255.255.255
 Mask:255.0.0.0
 UP BROADCAST LOOPBACK RUNNING MTU:3584 Metric:1
 RX packets:501 errors:0 dropped:0 overruns:0
 frame:0
 TX packets:501 errors:0 dropped:0 overruns:0
 carrier:0
 collisions:0

eth0 Link encap:Ethernet HWaddr 00:C0:F6:98:37:37
 inet addr:206.171.50.50 Bcast:206.171.50.63
 Mask:255.255.255.240
 UP BROADCAST RUNNING MULTICAST MTU:1500
 Metric:1
 RX packets:2 errors:0 dropped:0 overruns:0
 frame:0
 TX packets:2 errors:0 dropped:0 overruns:0
 carrier:0 collisions:4
 Interrupt:5 Base address:0x340

eth0:0 Link encap:Ethernet HWaddr 00:C0:F6:98:37:37
 inet addr:206.171.50.58 Bcast:206.171.50.63
 Mask:255.255.255.240
 UP BROADCAST RUNNING MTU:1500 Metric:1
 RX packets:9 errors:0 dropped:0 overruns:0
 frame:0
 TX packets:9 errors:0 dropped:0 overruns:0
 carrier:0 collisions:0
```

As you can see, the eth0:0 device is up and running. You can create an alias of any other Ethernet device in the same way.