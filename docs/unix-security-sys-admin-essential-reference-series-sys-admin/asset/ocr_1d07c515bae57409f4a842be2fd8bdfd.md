A dual-homed gateway is not vandal-proof. An attacker who successfully obtains access to the dual-homed gateway has what amounts to local network access on your private network. At this point, all of the standard security holes become available. Misconfigurations or improper permissions on NFS-mounted filesystems, .rhosts files, automatic software distribution systems like rdist, network backup programs, and other administrative shell scripts become tools to help the attacker gain a presence on your gateway. Once that presence is established, it will only be a matter of time before all of the systems in your network are compromised.

With a dual-homed gateway, if the firewall is destroyed, the attacker may be able to alter the routing and expose the entire network. Since most UNIX-based dual-homed gateways disable TCP/IP forwarding by modifying the kernel parameter IPFORWARDING, the attacker might want simply to defeat the gateway and change this parameter. If root privileges on the gateway can be obtained, then this is most certainly the first choice of attack. Once the new kernel is linked, the intruder can force a reboot during the night and gain access to your network without having to access the gateway first.

# The Screened Host Gateway

The screened host gateway is similar to the dual-homed gateway, but is considered very secure while remaining relatively easy to implement. While the dual-homed gateway consists of a single machine, the screened host gateway (Figure 11.7) is more

Figure 11.7 The screened host gateway is similar to the dual-homed gateway, but is more complicated to establish and requires additional equipment.

![](bbox=[0.15, 0.88, 0.88, 0.98])