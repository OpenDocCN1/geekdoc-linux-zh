
# ksruhe.de#0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0)
EOL

15:37:56.261172 rstud1.rz.uni-ksruhe.de > isdn216-10.rz.uni-ksruhe.de:
icmp: echo reply (ttl 253, id 28562, optlen=40 RR|isdn216-10.rz.uni-ksruhe.de=rzasc01.rz.uni-ksruhe.de 129.137.96 rzstud1.rz.uni-ksruhe.de# r-ascend-netz.rz.uni-ksruhe.de rzasc01.rz.uni-ksruhe.de#
0.0.0.0 0.0.0.0 0.0.0.0 (EOL)

**Programming Access** We will show you how IP packet options can be accessed during programming. This example uses Version 1.38. When ping starts, the first thing is to check the parameters passed. If they include -R, then the Echo Request packet has to include the Record Route IP option. For this purpose, ping uses the setsockopt() function to inform an existing socket packet options.

The following example shows how this function is invoked from within the source code of ping:

```
if (setsockopt(s, IPPRTO_IP, IP_OPTIONS, rspace, sizeof(rspace)) < 0)
{
    perror("ping: record route");
    exit(1);
}
```

The specified options will be set in each packet sent over this socket in the future. The IPPRTO_IP parameter means that the packet option to be set is an IP option. This does not necessarily mean that it is an IP option in the true sense. It could be present in another position within the IP header (e.g., IP_TTL also belongs to the IPPRTO_IP group). From the programming perspective, we always have to assume that the current kernel implementation does not support the desired IP option. In this case, setsockopt() returns the value 1 and outputs an error message. Subsequently, an arbitrary number of packets with the packet option set sent over this socket.

Incoming ICMP packets sent by ping are checked for their options as follows: An option pointer points to the First Field in the protocol header is computed. The option pointer is incremented so that it points to the next for. The Record Route option pointer has to point to a byte that includes the number "7". ping doesn't actually have to take care of this value; like all other option-specific constants, it is defined in <linux/ip.h>:

```
#define IPOPT_END (0 |IPOPT_CONTROL)
#define IPOPT_NOOP (1 |IPOPT_CONTROL)
#define IPOPT_SEC (2 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_LSRR (3 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_TIMESTAMP (4 |IPOPT_CONTROL|MEASUREMENT)
#define IPOPT_RR (7 |IPOPT_CONTROL)
#define IPOPT_SID (8 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_SWRR (9 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_RA (20|IPOPT_CONTROL|IPOPT_COPY)
```

If one of these packet options is found, then it is output.

## 14.3.3 The ip_options Class in the Linux Kernel

This section describes all functions of the ip_options class implemented in the Linux kernel. If options are passed to or from functions, then this is normally done by use of the ip_options data type. This type is defined in <linux/ip.h and includes the variables, pointers, and constants required for all packet options.

```
ip_options_build()
```

This function takes the information about IP options from the socket object and creates the options part in the IP header.
The parameters passed here include a socket buffer, the packet options, the packet destination address, the routing table, and the is_frag variable. The socket buffer includes a datagram with a protocol header that is not yet complete. The passed packet options are copied to the end of the protocol header. If the Strict Source Routing exists, then the destination address of the packet is written to the address list of the packet option. If the packet is not a fragment, and if the Internet Timestamp or Record Route exists, then the required data is inserted into the corresponding lists. If the packet is a fragment and one of the two options exists, then these options are replaced by No Operation.

```
ip_options_echo()
```

ip_options_echo() routine takes the options from an IP packet received and uses them to create an echo packet (i.e., reply to the incoming message). This function is normally used to send a reply when packets with IP options have been received—for example, to insert a Strict Routing option. The parameters passed here are a socket buffer and the destination options.

```
ip_options_fragment()
```

This function takes the fragment that was passed as socket buffer and overwrites all packet options with the No Operation option, with the Copy flag not set. As described in Section 14.3.1, this flag is set for the Internet Timestamp and Record Route options. The replacement by No Operation has the advantage that the length of the protocol header does not change.

```
ip_options_compile()
```

This function compiles the Option field at the end of the IP header. ip_options_build() uses data structures readily prepared for packet options, ip_options_compile() has to compile all options. The parameters passed here include the packet options and the socket buffer. This function works by option until it reaches an End-of-Option List or the end of the protocol header. Any No Operation in the list is skipped. If an error occurs in this procedure, then an ICMP message is returned to the sender.

```
ip_options_undo()
```

It can be necessary to delete the last entries in the packet options Source Routing, Record Route, and Internet Timestamp. The function ip_options_undo() is responsible for this task. This function can follow once the ip_options_echo() is invoked. For example, an Echo Request with the Record Route option is set to the local computer, the function ip_options_echo() duplicates the set in the incoming packet. These packet options are then used to return.

```
ip_options_get()
```

This function checks whether the IP options can be accessed by setsockopt(). If so, it returns 0; otherwise, it returns a negative error code (defined in <asm/errno.h>).

```
ip_options_forward()
```

This function adds all necessary information about the IP options to the packet if the packet has to be forwarded. The only parameter passed here is the socket buffer.

```
ip_options_rcv_srr()
```

This function checks the packet options for Loose Routing or Strict Source Routing. If it is specified, it means that the function ip_options_rcv_srr() has to be invoked.

## 14.3 Options in the Layer

Incoming Packets There are several ways an IP packet can move across the IP layer. It can enter either from the lower or from the higher layers (i.e., from the IP module). Figure 14–10 shows this relation and the position within the packet-handling process.

If an IP packet enters the IP layer from a lower layer, then iprcv() is the first invoked. The packet is passed as socket buffer, and it first has to pass the netfilters. Netfilters have the functionality of a firewall and can address translations. To translate addresses, NK_HOOK() with the iprcv_finish() is invoked. Chapter 19 describes how netfilters are handled. After this process, iprcv_finish() is the function executed. The only parameter passed to this function is the socket buffer.

Local Packet Delivery The function ip_local_deliver() is invoked if an IP packet has to be delivered to the local computer. This packet could be a fragment of a larger IP datagram, which means many things have to be checked—for example all fragments have arrived, which is checked by the function ipdefrag(). Once all fragments have arrived, all options have to be removed from the first fragment to reassemble the fragments into the original datagram. The first fragment always includes all options that were copied when the datagram was fragmented. Next, the packet traverses the netfilters once more. The function ip_local_deliver_finish() completes a local packet delivery in the IP layer.
