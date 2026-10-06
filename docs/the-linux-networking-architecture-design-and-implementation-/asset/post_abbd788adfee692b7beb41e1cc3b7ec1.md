
## 9.4 Implementation in the Linux Kernel

PPPoE implementation were moved to the file pppox.c, and other PPP implementations over other networks should be available in the future.

### Functions and Data Structures of the PPPoE Driver

In the first step, the PPPoE driver registers the PPPoE protocol with the kernel. This can be seen in the following piece of source text:

```
pppoe_init() drivers/net/pppoox.c
{
  Use a function from drivers/net/pppoox.c to register the PPPoE protocol:
  int err = register_pppoe_proto(PX_PROTOCOL_POE, &pppoe_proto);
  if (err==0) {
    dev_add_pack(&pppoes_type);
    /*Add a packet handler
    for incoming packets of type ETH_P_PPP_SES
    (PPPoE session packets), which points to pppoe_rcv */
    dev_add_pack(&pppoed_type);
    /*Add a packet handler for incoming packets of type
    ETH_P_PPP_DISC (PPPoE connection setup packets), which
    points to pppoe_disc_rcv */
    register_netdevice_notifier(&pppoe_notifier);
    /*Add to netdevice notification chain */
    proc_net_create("pppoe", 0, pppoe_proc_info);
    /*Generate an entry in the proc directory */
  }
  return (err);
}
```

Subsequently, the PPPoE protocol functionality provides functions that can be used by pppd to access the PPPoE socket. The structure proto_ops proto_pppoe_ops in driver/net/pppoe.c is used to bind the functionality of the PPPoE socket to general socket functions (e.g., connect(), sendmsg(), recvmsg(), and bind()). Chapter 26 includes a more detailed description of how sockets are implemented in the Linux kernel.

```
pppoe_create() drivers/net/pppoe.c
```

This function is invoked whenever a new PPPoE socket is opened. The function is exported and announced the structure pppoe_proto and the function register_pppoe_proto().

```
pppoe_connect() drivers/net/pppoe.c
```

This function calls connect() at the PPPoE socket interface. If the call is successful, then PPPoE packets that have previously been sent or received over the specified Ethernet card can be accessed over the PPPoE socket in the application layer.

### pppoe_sendmsg()

The function pppoe_sendmsg() is used to pack data sent by pppd into the PPPoE packets and send them over the Ethernet.

### pppoe_rcvmsg()

This function serves to receive PPPoE packets over the PPPoE socket. However, only packets belonging to the discovery stage of the PPPoE protocol are processed; all other packets are instead forwarded to the generic PPPoE driver. Information about whether the PPPoE protocol is in the discovery stage or in the session stage is saved in sk->state.

Finally, once the PPPoE discovery stage is completed, incoming packets are forwarded to the generic PPPoE driver (The case of PPPoE relay is not discussed here.) Various functions can be used to receive packets:

### pppoe_rcv()

This function is executed within the NET_RX tasklet. It handles error cases and passes packets to the function pppoe_rcv_core() for further processing.

### pppoe_rcv_core()

This function determines the dependency on the phase of the PPPoE protocol stored in sk->state, which means that an incoming packet is either forwarded to the generic PPP driver (by the function大量_input()) or appended to the queue of the PPPoE socket by the function sock_queue_rcv_skb(), where it will be processed by the aforementioned function pppoe_rcvmsg().

### pppoe_disc_rcv()

This function is invoked whenever a packet of the PPPoE discovery stage was received (ethertype 0x8863 or ETH PPP DISC, as defined in linux/if_ether.h). However, the function pppoe_disc_rcv() only serves to receive PADT packets; all other packets are rejected. If an incoming packet is a PADT packet, then the PPPoE connection is disconnected and the socket is released.

### pppoe_xmit()

This function is invoked by the generic PPP driver. It serves as wrapper for the function __pppoe_xmit().

### _pppoe_xmit()

This function is used to pack transmit data of the generic PPP driver into a PPPoE frame and send it over the specified Ethernet network card.

### 9.4.2 Tasks of the ppp daemon

A data connection is established in several phases. The phase of the PPPoE discovery is fully handled by the ppp daemon, avoiding thethepppo driver. Special packet sockets are included in kernel Version 2.4 (see Chapter 26) and can be used to send or receive packets specified in RFC 2516 directly to or from the network card. If the discovery is successful, then the ppp daemon sets up a ppp interface in the kernel. The ppp daemon achieves this by opening a PPPoE socket and binding this socket to the PPPoE driver. Finally, the ppp daemon uses an ioctl() to set the field sk->state with the parameter PPPOCCGAN (implemented in driver/net/ppp.c) to PPPOX_BOUND.

As described in the previous section, this causes the PPPoE driver to forward all incoming packets to the ppp daemon, except the PPPoE relay case, which is not considered here, and for PADT packets, which are handled by the function pppoe_disc_recv() (as already described). The ppp daemon can use different ioctl() calls over the PPPoE socket to change other parameters. However, the data path always leads over the generic PPP driver, from which the PPPoE driver now accepts PPP packets (data and control packets); it packs them and eventually, passes them to the network card.

### 9.4.3 Configuration

To be able to use PPPoE in Linux from kernel Version 2.4 and higher, the option PPPOverEthernet and the option Socket have to be activated in the kernel configuration upon compilation (via activation of the support for experimental drivers). If the PPPoE support is compiled as a module, then we additionally have to add the line “alias net-pf-24 pppoe” to the file /etc/modules.conf. This line is used to allocate the protocol with identifier 24 to the pppoe module. A package that integrates PPPoE extensions is available for pppd. All we have to do is to complete the file /etc/ppp/options by adding the line plugin pppoe pppd can be started with pppd eth0. [Ostr01] includes more installation instructions.

## CHAPTER 10 Asynchronous Transfer Mode—ATM

### 10.1 INTRODUCTION

Initially, the Asynchronous Transfer Mode (ATM) was introduced to provide a uniform protocol for the transmission of voice and data, offering guarantees for the required QoS (Quality of Service) parameters [McSp95].

In contrast to initial expectations and forecasts, the ATM network technology has not established in end systems, but it is widely used in core networks: of all ATM offers a uniform concept to support QoS (Quality of Service) in networks; QoS was attempted much later in IP-based networks.

The network technology is connection-oriented, which means that a connection has to be established before data can be transmitted: In a Permanent Virtual Connection (PVC), the connection throughout the network is established by the network management: a network management station extends the forwarding tables within the forwarding nodes between two endpoints of an ATM connection so that the ATM cells created by the endpoints are forwarded to the other endpoint. The second type of ATM connection is a Signaled Virtual Connection (SVC); in this connection, the connection is established by the communicating systems, which send connection requests and respond to such requests.

In ATM, packets are called cells. In contrast to IP protocol data units, an ATM cell has a fixed size, 53 bytes: 5 bytes for the packet header, 48 bytes for the payload. The 5-byte packet header includes forwarding information, as for IP frames, ATM network technology uses a hierarchical connection concept, distinguishes between paths and channels. Each cell is allocated to exactly one virtual path, and to exactly one virtual channel within that path, as shown in Figure 10–1. This allocation to a path and a channel is specified in two bits in the cell header: an 8-bit field for the Virtual Path Identifier (VPI), and a 16-bit field for the Virtual Channel Identifier (VCI).
