Another important transformation is part of large enterprises moving to a new network architecture called Spine Leaf, which increases the efficiency of the traffic and reduces the possible bottlenecks caused by the traditional architecture. Figure 7.3 shows the difference between the traditional architecture, which has three layers (access, aggregation, and core) with limitations of the parallel traffic, and the new architecture, with a mesh connection with high bandwidth and low- latency features:

![](bbox=[0.14, 0.24, 0.86, 0.48])

*Figure 7.3: Traditional and spine leaf architectures. Source: Aruba Networks*

Another important change in the last few years was the introduction of IPv6, the most recent version of the Internet Protocol. This new version uses 128-bit addresses instead of the 32-bit ones on IPv4. The use of IPv6 is still limited in local networks, but the adoption of ISP and large enterprises are a reality.

# ## Physical layer (Layer 1)

Chapter 6, Monitoring System Resources, described using the command `lshw` to list the available Ethernet devices on the system. The command `ethtool` was introduced in the same chapter to obtain information about the status, such as if the link was detected and the possible speeds available.

The command `ip` replaces the operations to the traditional, and the deprecated command `ifconfig` in Linux replaces the operations to list information about the interfaces. Specifying as an argument, the word `link` lists the network interface's physical information as illustrated in figure 7.4: