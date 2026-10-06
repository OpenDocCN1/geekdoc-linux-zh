# 14.3.3 The ip_options Class in the Linux Kernel

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