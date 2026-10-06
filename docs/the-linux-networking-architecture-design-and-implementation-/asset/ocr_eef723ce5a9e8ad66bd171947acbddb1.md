# Chapter 19 Packet Filters and Firewalls

Independent of the application protocol, we cannot use stateful filters when the control connections are encrypted. In this case, the only feasible method is to employ specially adapted client and server software that uses an appropriate protocol, such asOCKS [LGLK96], to let the firewall dynamically and selectively permit traffic on specific ports.

# 19.1.3 Quality Criteria for Packet-Filter Implementations

To be able to evaluate the quality of a packet-filter architecture, [ChBe94] formulates the following criteria:

+   - Filtering is done both for incoming and outgoing packets.
- There is an option to distinguish connection-establishment requests from other packets within one single connection.
- Filter options for protocols other than IP,TCP, and UDP either are available or can be added easily.
- There are filter options for arbitrary bit patterns within packets.
- There are filter options for routing information at both the input and the output.
- There is an option to reject data packets, if the destination address of these packets was changed by source routing.
- The set of rules is clearly presented, and there is an option to control the sequence in which rules are applied to a packet.
- Dropped data packets can be logged.

We will see in our discussion in the following sections that the new netfilter architecture of Linux Version 2.4 meets all those criteria.

# 19.1.4 Limits of the Firewall Principle

Though a properly configured firewall is an important component for protecting a network, we have to understand that a firewall can never be a panacea. All packet filters operate on the basis of information contained in the protocol headers of incoming data packets. This information can be tampered with easily. For example, an adapted TCP/IP implementation makes it very easy for an intruder to send IP packets whose source address in the IP header is not the address of the actual sender (called IP spoofing).

To achieve tamper-proof identification of a packet's origin as a prerequisite for effective filtering of incoming data traffic, it is recommended that one use cryptographic mechanisms (e.g., the IP security architecture of IPSec). In Linux, we can use FreeS/WAN, which is an IPsec implementation.

# 19.2 THE IPCHAINS ARCHITECTURE OF LINUX 2.2

ipchains is a packet-filtering architecture consisting of an infrastructure in the Linux kernel and a user-space program to manage rules lists, like all packet-filtering architectures currently implemented in Linux. In Linux 2.2, this product is called ipchains.