# Chapter 21: Network Configuration and Security

FIGURE 21-11
Information about eth0 in the Network Tools application

![](bbox=[0.035, 0.165, 0.455, 0.575])

The easiest and fastest way to identify the current configuration of one of your Ethernet interfaces will probably always be to run the ifconfig -name interface-command in an xterm or GNOME Terminal window, which will display out like the following:

```
$ ifconfig eth0
Link encap:Ethernet HWaddr00:16:EC:CA:AE:20
      inet addr:192.168.6.6 Bcast:192.168.6.255 Mask:255.255.255.0
      inet6 addr:fe80::26:ff:eca20/64 Scope:Link
      UP BROADCAST RUNNING MTU:1500 Metric:1
      RX packets:32034 errors:0 dropped:0 overruns:0 frame:0
      TX packets:28776 errors:0 dropped:0 overruns:0 carrier:0
      collisions:0 txqueuelen:0
      RX bytes:12108607 (11.5 MiB) TX bytes:4603767 (4.3 MiB)
```

As you can see, the text display of Ethernet interface information provided by the ifconfig command requires a certain amount of interpretation when compared to the friendlier display of information shown in Figure 21-11.