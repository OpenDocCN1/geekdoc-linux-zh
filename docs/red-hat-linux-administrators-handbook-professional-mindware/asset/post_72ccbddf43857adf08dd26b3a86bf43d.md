
If you use IDE drives on a PCI system, keep the defaults for the following options:

- **Generic PCI IDE chipset support** (`CONFIG_BLK_DEV_IDEPCI`) [Y/n/?]
- **Generic PCI bus-master DMA support** (`CONFIG_BLK_DEV_IDEDMA`) [Y/n/?]
- **Boot off-board chipsets first support** (`CONFIG_BLK_DEV_OFFBOARD`) [N/y/?]

If your system is capable of using Direct Memory Access (DMA) for IDE drives, choose the default for the following question:

- **Use DMA by default when available** (`CONFIG_IDEDMA_AUTO`) [Y/n/?]

If you want to enable enhanced support for various IDE chipsets, choose yes for the following question:

- **Other IDE chipset support** (`CONFIG_IDE_CHIPSETS`) [N/y/?]

## Additional block devices

For most cases, all options in this section are useless, so you can safely accept the default answers here:

- **Loopback device support** (`CONFIG_BLK_DEV_LOOP`) [N/y/m/?] y
- **Network block device support** (`CONFIG_BLK_DEV_NBD`) [N/y/m/?]
- **Multiple devices driver support** (`CONFIG_BLK_DEV_MD`) [N/y/?]
- **RAM disk support** (`CONFIG_BLK_DEV_RAM`) [N/y/m/?]
- **XT hard disk support** (`CONFIG_BLK_DEV_XD`) [N/y/m/?]
- **Parallel port IDE device support** (`CONFIG_PARIDE`) [N/y/m/?]

## Networking options

Networking is one of the most important sections. Here, you decide on various networking issues.

- **Packet socket** (`CONFIG_PACKET`) [Y/m/n/?]  
  Applications such as tcpdump use the Packet protocol; therefore, you should accept the default answer.

- **Kernel/User netlink socket** (`CONFIG_NETLINK`) [N/y/?]

### Network firewalls (`CONFIG_FIREWALL`) [N/y/?]

If you want to use your system as a firewall or want to use the arpd daemon to maintain an internal ARP cache, say yes here.  
If you would like to use your system as a packet-filtering firewall, set this to yes.

### Network aliasing (`CONFIG_NET_ALIAS`) [N/y/?]

If you have multiple network interfaces for your system, set this to yes.

### Socket Filtering (`CONFIG_FILTER`) [N/y/?]

This feature allows programs to attach filters to sockets and to control how data go through the socket. Unless you use such programs, the default answer is fine.

### Unix domain sockets (`CONFIG_UNIX`) [y/N/m/n/?]

Sockets are standard Unix mechanisms for establishing and accessing network connections. Therefore, the default answer is fine.

### TCP/IP networking (`CONFIG_INET`) [Y/n/?]

This is a no-brainer.

### IP: multicasting (`CONFIG_IP_MULTICAST`) [N/y/?]

Typically, you use IP multicasting for transferring large amounts of data such as real-time, broadcast-quality video that uses large bandwidth connections. Unless you have such needs, the default is fine.

### IP: advanced router (`CONFIG_IP_ADVANCED_ROUTER`) [N/y/?]

If you intend to run your Linux box mostly as a router (as a computer that forwards and redistributes network packets), press y.

### IP: kernel level autoconfiguration (`CONFIG_IP_PNP`) [N/y/?]

This enables automatic configuration of the IP addresses of devices, and of the routing table during kernel boot, based on information supplied either at the kernel command line or by BOOTP or RARP protocols.

### IP: optimize as router not host (`CONFIG_IP_ROUTER`) [N/y/?]

Some Linux network drivers use a technique called copy and checksum to optimize host performance. However, for a machine that acts as a router most of the time and is forwarding most packets to another host, such optimization is not needed—select the default.

### IP: tunneling (`CONFIG_NET_IPIP`) [N/y/m/?]

Tunneling means encapsulating data of one protocol within another protocol and sending it over a channel that understands the encapsulating protocol. This particular tunneling driver implements encapsulation of IP within IP, which sounds kind of pointless but can be useful if you want to make your (or some other) machine appear on a different network from the one it is physically connected to or to use mobile-IP facilities (allowing laptops to seamlessly move between networks without having to change their IP addresses).

### IP: GRE tunnels over IP (`CONFIG_NET_IPGRE`) [N/y/m/?]

GRE (Generic Routing Encapsulation) allows encapsulating of IPv4 or IPv6 over the existing IPv4 infrastructure.

### IP: aliasing support (`CONFIG_IP_ALIAS`) [N/y/?]

If you want to attach multiple IP addresses to a single network interface, say yes here.

### IP: TCP syncookie support (not enabled per default) (`CONFIG_TCP_SYNCOOKIES`) [N/y/?]

Normal TCP/IP networking is open to an attack known as “SYN flooding.” This denial-of-service attack prevents legitimate remote users from connecting to your computer during an ongoing attack and requires very little work from the attacker, who can operate from anywhere on the Internet. SYN cookies provide protection against this type of attack. If you choose y here, the TCP/IP stack uses a cryptographic challenge protocol known as “SYN cookies” to enable legitimate users to continue to connect even when your machine is under attack. There is no need for legitimate users to change their TCP/IP software, but SYN cookies may prevent correct error reporting on clients when the server is overloaded. If this happens frequently, you had better turn them off. If you choose y here, note that choosing the default does not enable SYN cookies; you can enable them by choosing Y to the /proc filesystem support (below) and Sysctl support (above) options and executing the command `echo 1 >/proc/sys/net/ipv4/tcp_syncookies` at boot time after the /proc file system mounts.

### IP: Reverse ARP (`CONFIG_INET_RARP`) [N/y/m/?]

If you want your server to provide Reverse Address Resolution Protocol (RARP) service for other computers on your network, you can select yes or set this feature to be a module.

### IP: Drop source routed frames (`CONFIG_IP_NOSR`) [Y/n/?]

Source routing is an IP protocol feature that allows the originating IP packet to contain full routing information for the destination IP address. Source routing is typically the cause of many network security problems, and you should avoid it. The default option is recommended.

### IP: Allow large windows (not recommended if <16Mb of memory) (`CONFIG_SKB_LARGE`) [y/n/?]

The above option is useful only if you are dealing with 2MB/sec or above bandwidth and long-distance networks.

### The IPX protocol (`CONFIG_IPX`) [N/y/m/?]

Unless you need support for Novell IPX networking, the default answer is fine.

### AppleTalk DDP (`CONFIG_ATALK`) [N/y/m/?]

Unless you need AppleTalk networking support, the default answer is fine.

## SCSI Support

If you have SCSI disks, a CD-ROM, tape drives, or other SCSI devices, this section allows you to configure support for such devices. Answer the following questions based on available SCSI hardware:

- **SCSI support** (`CONFIG_SCSI`) [Y/n/m/?]
- **SCSI disk support** (`CONFIG_BLK_DEV_SD`) [Y/n/?]
- **SCSI tape support** (`CONFIG_CHR_DEV_ST`) [Y/n/m/?]
- **SCSI CD-ROM support** (`CONFIG_BLK_DEV_SR`) [N/y/m/?]
- **SCSI generic support** (`CONFIG_CHR_DEV_SG`) [N/y/m/?]

- **Probe all LUNs on each SCSI device** (`CONFIG_SCSI_MULTI_LUN`) [Y/n/?]  
  Unless you have a SCSI device with multiple Logical Unit Numbers (LUN), choose no here.

- **Verbose SCSI error reporting (kernel size +12K)** (`CONFIG_SCSI_CONSTANTS`) [Y/n/?]  
  The error messages regarding your SCSI hardware are easier to understand if you choose yes here.

- **SCSI logging facility** (`CONFIG_SCSI_LOGGING`) [N/y/?]  
  This turns on a logging facility you can use to debug a number of SCSI-related problems. If you choose yes, you must enable logging by using the following command in /etc/rc.d/rc.local:

  ```
  echo "scsi log token [level]" > /proc/scsi/scsi
  ```

  Here, token can be error, scan, mlqueue, mlcomplete, llqueue, llcomplete, hlqueue, or hlcomplete. The level controls the verbosity of the log and can be any positive number or 0.

The rest of the questions in the SCSI section are specific to SCSI host adapters. You should choose support for only the adapter(s) you have installed.

## Network device support

In this section, you configure various network device features.

- **Network device support** (`CONFIG_NETDEVICES`) [Y/n/?]  
  Because you are configuring the kernel for your server, you must say yes to the preceding question.

- **ARCNET support** (`CONFIG_ARCNET`) [N/y/m/?]  
  Unless you have ARCNET network interface cards, the default is fine.

- **Dummy net driver support** (`CONFIG_DUMMY`) [N/y/?]
