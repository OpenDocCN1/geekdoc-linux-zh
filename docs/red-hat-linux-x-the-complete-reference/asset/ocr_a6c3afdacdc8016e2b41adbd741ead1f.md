# IPv4 and IPv6

Traditionally, a TCP/IP address is organized into four segments, consisting of numbers separated by periods. This is called the IP address. The IP address actually represents a 32-bit integer whose binary values identify the network and host. This form of IP addressing adheres to Internet Protocol, version 4, also known as IPv4. IPv4, the kind of IP addressing described here, is still in wide use.

Currently, a new version of the IP protocol called Internet Protocol, version 6 (IPv6) is gradually replacing the older IPv4 version. IPv6 expands the number of possible IP addresses by using 128 bits. It is fully compatible with systems still using IPv4. IPv6 addresses are represented differently, using a set of eight 16-bit segments, each separated from the next by a colon. Each segment is represented by a hexadecimal number. A sample address would be:

```
FEC0:0:0:0:800:BA98:7654:3210
```

Advantages for IPv6 include the following:

+   - Features simplified headers that allow for faster processing.
+   - Provides support for encryption and authentication along with Virtual Private Networks (VPN) using the integrated IPSEC protocol.
+   - Extends the address space to cover 2 to the power of 128 possible hosts (billions of billions). This extends far beyond the 4.2 billion supported by IPv4.
+   - Supports stateless autoconfiguration of addresses for hosts, bypassing the need for DHCP to configure such addresses. Addresses can be generated directly using the MAC (Meda Access Control) hardware address of an interface.
+   - Supports Quality of Service (QoS) operations, providing sufficient response times for services like multimedia and telecom tasks.
+   - Multicast capabilities built into the protocol, providing direct support for multimedia tasks.
+   - Multicast addressing also provides the same function as IPv4 broadcast addressing.
+   - More robust transmissions can be insured with anycast addressessing, where packets can be directed to an anycast group of systems, only one of which needs to receive them. Multiple DNS servers supporting a given network could be designated as an anycast group, of which only one DNS server needs to receive the transmission, providing greater likelihood that the transmissions will go through.
+   - Better access for mobile nodes, like PDAs, notebooks, and phones.