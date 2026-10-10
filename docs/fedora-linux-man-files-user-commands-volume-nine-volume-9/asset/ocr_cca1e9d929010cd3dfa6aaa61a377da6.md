```
[,dstport=dstport],txsession=txsession [,rxsession=rxsession][,ipv6],udp][,cookie64]
[,counter] [,pincounter],txcookie=txcookie[,rxcookie=rxcookie] [,offset=offset]
```

Connect VLAN n to L2TPv3 pseudowire. L2TPv3 (RFC3931) is a popular protocol to transport Ethernet (and other Layer 2) data frass between two systems. It is present in routers, firewalls and the Linux kernel (from version 3.3 onwards).

This transport allows a VM to ccommunicate to another VM, router or firewall directly.

src=srcaddr source address (mandatory) dst=dstaddr destination address (mandatory) udp select udp encapsulation (default is ip). srcport=srcport source udp port. dstport=dstport destination udp port. ipv6 force v6, otherwise defaults to v4. rxcookie=rxcookie txcookie=txcookie Cookies are a weak form of security in the l2tpv3 specification. Their function is mostly to prevent misconfiguration. By default they are 32 bit. cookie64 Set cookie size to 64 bit instead of the default 32 counter=off Force a 'cut-down' L2TPv3 with no counter in draft-mkonstan-l2tpext-keyed-ipv6-tunnel-00 pincounter=on Work around broken counter handling in peer. This may also help on networks which have packet reorder. offset=offset Add an extra offset between header and data

For example, to attach a VM running on host 4.3.2.1 via L2TPv3 to the bridge br-lan on the remote Linux host 1.2.3.4:

```
# Setup tunnel on linux host using raw ip as encapsulation # on 1.2.3.4 ip l2tp add tunnel remote 4.3.2.1 local 1.2.3.4 tunnel_id 1 peer_tunnel_id 1 \
encap udp ~~ dst_port 16384 udp_sport 16384 ip l2tp add session tunnel_id 1 na vmtunnel0 session_id 0xFFFFFFF peer_session_id 0xFFFFFFF ifconfig vmtunnel0 mtu 1500 ifconfig vmtunnel0 up brctl addif br-lan vmtunnel0 # on 4.3.2.1 # launch QEMU instance - if your network has reorder or is very lossy add -pincounter qe-system-i386 linux.img -net nic -net l2tpv3,src=4.2.3.1,dst=1.2.3.4,udp,srcport=16384,dstport=16384,rxsession=0xffffff,txsession=0xffffff,counter
```

```
-netdev vde,id=id[,sock=socketpath][,port=n][,group=groupna][,mode=octalmode] -net vde[,vlan=n],na=na[,sock=socketpath] [,port=n][,group=groupna][,mode=octalmode]
```

Connect VLAN n to PORT n of a vde switch running on host and listening for incoming connections on socketpath. Use GROUP groupna and MODE octalmode to change default ownership and permissions for communication port. This option is only available if QEMU has been compiled with vde support enabled.

Example:

```
# launch vde switch vde_switch -F -sock /tmp/mySwitch # launch QEMU instance qe-system-i386 linux.img -net nic -net vde,sock=/tmp/mySwitch
```

-netdev hubport,id=id,hubid=hubid Create a hub port on QEMU “vlan” hubid. The hubport netdev lets you connect a NIC to a QEMU “vlan” instead of a single netdev. -net and -device with parater vlan create the required hub automatically.

-netdev vhost-user,chardev=id[,vhostforce=on|off] Establish a vhost-user netdev, backed by a chardev id. The chardev should be a unix domain socket backed one. The vhost-user uses a specifically defined protocol to pass vhost ioctli replacec ssages to an application on the other end of the socket. On non-MSIX guests, the feature can be forced