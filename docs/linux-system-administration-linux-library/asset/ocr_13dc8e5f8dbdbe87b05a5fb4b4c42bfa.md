Your firewall can be as restrictive or open as you wish. Perhaps you simply want to prevent people outside your firewall from being able to Telnet into your system. You may do this by having the firewall reject incoming packets that are required to set up such connections. In an alternate scenario, you might want to filter packets from your local area network to prevent anyone from reaching a given IP address. How restrictive your firewall depends on the rules you set in IP Chains.

The functionality for a packet filtering firewall is built into the Linux kernel, although you must recompile with certain kernel options turned on. This is outlined in the Firewall-HOWTO, maintained by Mark Grennan. Basically, in selecting options you need to include routing, defragmentation, IP masquerading, and multicast routing (if you intend to do multicasting). Older kernels in the 1.x era use a package called ipfwadm, which is no longer supported. Kernels 2.2.13 use IP Chains instead; we'll talk about that in the IP Chains section below, and you can supplement your knowledge by going to http://www.rustcorp.com/linux/ipchains/. The 2.4 kernels use a new firewall utility, known as iptables.

Read the Firewall and Proxy Server HOWTO IF you are building a firewall! It will be helpful to read the Linux Networking HOWTO and the Linux IPCHAINS as well. Most HOWTOs can be found on Red Hat's site:

```
http://www.redhat.com/mirrors/LDP/HOWTO/
```

A filtering firewall does not require a high-end power computer. If you have an old 486DX66 or better with at least 16MB of memory, 300–500MB of hard drive space, and network connections, you will do fine. The work of filtering packets doesn't heavily tax a system.

# IP Chains

The IP Chains package making the kernel inherent firewall capabilities much easier. An IP chain is a set of rules to be considered when a data packet is attempting to pass through the firewall. The default IP Chains configuration includes three permanent chains: input, output, and forward. The input chain governs incoming packets, the forward chain manages packets destined for another host, and outgoing packets are subjected to the rules of the output chain. You may add and edit other chains as needed. The IP chains process is fairly simple and is illustrated in Figure 7.3.