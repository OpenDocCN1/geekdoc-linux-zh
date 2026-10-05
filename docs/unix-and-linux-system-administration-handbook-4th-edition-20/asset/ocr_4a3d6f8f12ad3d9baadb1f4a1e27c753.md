# Chapter 14 TCP/IP Networking

```
quit = Terminate the Admin, return to shell
reset = Reset LAN Interface, execute selfftest
specific = Go to Driver specific menu
```

Enter command: **display**

| LAN INTERFACE STATUS DISPLAY |
| Jun 2, 2009 00:04:24 |
| PPA Number = 0 |
| Description = lan0 Intel PCI Pro 10/100Tx Server Adapter |
| Type (value) = ethernet-csmacd(6) |
| MTU Size = 1500 |
| Speed = 100000000 |
| Station Address = 0x00306eea9237 |
| Administration Status (value) = up(1) |
| Operation Status (value) = up(1) |

+   - Inbound Unicast Packets = 45691
- Inbound Non-Unicast Packets = 2630

+   - Deferred Transmissions = 0
- Late Collisions = 0
- Excessive Collisions = 0

# HP-UX DHCP configuration

As with other network configuration parameters, you turn on the use of DHCP at boot time by setting variables in the **/etc/rc.config.netconf** file. In this case, the variable names start with DHCP_ENABLE. The index [0] refers to the first interface, [1] to the second interface, and so on. For example,

```
DHCP_ENABLE[0]=1
```

sets the first network interface to DHCP mode. It will get its IP address, netmask, and other parameters from the DHCP server on the local network. Setting the variable to 0 would disable DHCP, you'd have to assign a static address in the **netconf** file. No DHCP_ENABLE clause is present, the variable defaults to 1.

The **/bin/auto_parms** script does the real work of contacting the DHCP server. The program **dhcpdb2conf** enters the DHCP parameters secured by **auto_parms** into the **netconf** file, which boot-time configuration information is taken.

# HP-UX dynamic reconfiguration and tuning

In Solaris, you can use **ndd** to tune many different networking parameters. When used instantaneously, ndd values change permanently, entering them in **/etc/rc.config.netconf**, **nddconf**, which is read at boot time.

On an HP-UX system, **ndd's -h** (help) option is quite useful. Without arguments, it lists all the parameters you can tune. If you specify a variable name, **ndd -h**

See page 498 for more details about **ndd**.