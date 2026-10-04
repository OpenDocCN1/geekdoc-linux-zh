# Chapter 2 • Inventory and Exposure of Corporate Assets

Since this book is not intended for newbies, I assume that you have an understanding of the Transmission Control Protocol/Internet Protocol (TCP/IP) and have used these tools before. If you aren't familiar with the options shown in an example, refer to the context, man page, or help text for that tool.

# Host Discovery and Service Discovery

Basic asset inventory really has only two steps, host discovery and service discovery, but each of them have multiple techniques that can be used to gather results for different situations and requirements.

> NOTE\This is a basic list and is not intended to be a comprehensive listing of all possible scan types. If you want that list, check out the home of Fyodor’s nmap at www.insecure.org.

+   * Host discovery Internet Control Protocol (ICMP) requests such as Echo, Netmask, and Timestamp are the first step in host discovery. The second step of host discovery is creating a list of devices that respond to TCP pings.
* ICMP sweeps Since most internal networks allow ICMP, ICMP sweeps are very useful when you need to quickly determine the sheer size of your network or one of its segments. If you need to identify hosts in a very quick and dirty manner, you should perform a ping sweep. Be sure to save the live IP addresses in a file for later use.

```
SCANLINE: sl -in 10.0.3.150-190 | find "10.0.3.*" > ICMPping.txt
MAP: nmap -sn -sPI -PM -PP 10.0.3.150-190 -oM ICMP.txt
```

+   * TCP ping sweeps This can be performed using any reliable TCP port scanner to sweep a list of several common TCP ports with SYN or ACK packets and wait for a response. Be sure that you configure the port scanner to “not perform a ping” before the TCP scan. Your responding hosts should be added to a file for later use. The following example shows the syntax for TCP Ping with nmap and

![](bbox=[0.068, 0.939, 0.294, 0.971])