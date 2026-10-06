# Chapter 11 • PERFORMANCE TUNING AND CAPACITY PLANNING 32

You can see the duplex mode of an interface on Solaris by querying the link_mode of an interface using ndd; 0 means half-duplex, and 1 means full-duplex, as follows:

```
# ndd /dev/hme link_mode
1
```

On Free/Open/BSD, the duplex is listed in ifconfig output.

```
bash$ ifconfig xl0
xl0: flags=8843-UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
media: Ethernet 100baseTX full-duplex
  status: active
inet 192.168.1.4 mask 0xffffff broadcast 192.168.1.255
```

On Red Hat Linux, duplex status is driver-specific, and there is no standard interface for querying duplex status. The best way to figure out the duplex of an interface in this case is to run dmesg | grep -i duplex, which displays buffered kernel messages containing the word "duplex." For example:

```
$ dmesg | grep -i duplex
eth: Setting full-duplex based on MII#1 link partner capability of 45e1.
```

# Tuning Network Performance

Even the most experienced network professionals struggle to master all of the techniques of network performance tuning. Even so, just performing a basic duplex tuning tasks can greatly increase the performance and reliability of your network communications. The following sections discuss some of the most basic network performance tuning tasks.

# Hard-coding Duplex Modes

As learned in the previous section, full-duplex communications can cause latency on a network connection. However, full-duplex can be used only in switched environments where there is only one peer on the same segment. Mesh segments connected to hubs are relegated to half-duplex mode.

You should not let autonegotiation decide the duplex for you in a production environment; it is just too unreliable. Duplex mismatches caused by botched autonegotiation are not uncommon in multiple architecture environments, and they can cause network errors and high latency—problems you want to avoid at all costs. The solution is to hardcode the proper duplex mode into your switches and servers to disable autonegotiation altogether.

On a Cisco switch running IOS 12.0, you can hardcode the duplex as follows:

```
switch#conf t
Enter configuration commands, one per line. End with CNTL/Z.
switch(config)#int Fa0/16
switch(config-if)#duplex full
switch(config-if)#
```