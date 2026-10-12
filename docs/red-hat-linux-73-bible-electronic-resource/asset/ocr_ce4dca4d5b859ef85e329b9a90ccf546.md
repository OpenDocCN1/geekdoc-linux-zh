```
lo      Link encap:Local Loopback
       inet addr:127.0.0.1 Mask:255.0.0.0
       UP LOOPBACK RUNNING MTU:3924 Metric:1
       RX packets:56 errors:0 dropped:0 overruns:0 frame:0
       TX packets:56 errors:0 dropped:0 overruns:0 carrier:0
       collisions:0
       RX bytes:3148 (3.0 Kb)  TX bytes:3148 (3.0Kb)
```

In this example, there are currently two network interfaces up on the current computer. The first section shows your Ethernet interface (eth0) and its hardware address, Ethernet hardware address, IP address (inet addr), broadcast address, and network mask. The next lines provide information on packets that have been sent, along with the number of errors and collisions that have occurred.

> **NOTE:** The lo entry is for loopback. This enables you to run TCP/IP commands on your local system without having a physical network up and running. I describe this and other network interfaces in more detail in Chapter 16.

If your eth0 interface does not appear, it may still be configured properly, but not running at the moment. Try to start the eth0 interface by typing the following:

```
# ifconfig eth0 up
```

After this, type `ifconfig` again to see if eth0 is now running. If it is, it may be that eth0 is simply not configured to start automatically at boot time. You can change it so Ethernet starts at boot-time (which I recommend), using the Network Configuration window (described earlier in this chapter).

> **TIP:** If your network interfaces are not running at all, you can try to start them from the network initialization script. This interface reads parameters and basically runs `ifconfig` for all network interfaces on your computer. Type the following to restart your network:
> 
> # /etc/init.d/network restart

Another way to see statistics for your Ethernet driver is to list the contents of the process pseudo file system for network devices. To do that, type the following:

```
# cat /proc/net/dev
```

The output should look similar to the following:

| Inter- face | Receive bytes | packets | errs | drop | fifo | frame | compressed | multicast | Transmit bytes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| lo: | 5362 | 64 | 0 | 0 | 0 | 0 | 0 | 5362 | 64 0 0 0 0 |
| eth0: | 3083 | 35 | 0 | 0 | 0 | 0 | 0 | 3876 | 31 0 0 0 0 |

The output is a bit hard to read (our book isn’t wide enough to show it without wrapping around, so the output was truncated at the right). With this output, you can see Receive and