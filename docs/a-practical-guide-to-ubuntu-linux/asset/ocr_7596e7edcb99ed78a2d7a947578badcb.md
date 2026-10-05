# NETWORK SECURITY

LPD. Normally a data switch on a LAN automatically protects machines from people snooping on the network for data. In high-load situations, switches have been known to behave unpredictably, directing packets to the wrong ports. Certain programs can overload the switch tables that hold information about which machine is on which port. When these are overloaded, the switch becomes a repeater and broadcasts all packets to all ports. The attacker on the same switch as you can potentially see the traffic your system sends and receives.

# NETWORK SECURITY SOLUTIONS

One solution to shared-network problems is to encrypt messages between machines. IPSec (Internet Protocol Security Protocol) provides appropriate technology. IPsec is commonly used to establish a secure point-to-point network (VPN, port 1180) that allows two hosts to communicate securely over an insecure channel, such as the Internet. This protocol protects integrity, confidentiality, authenticity, and flexibility of implementation that supports multiple vendors.

IPSec is an amalgamation of protocols (IPSec = AH + ESP + IPComp + IKE):

+   * **Authentication Header (AH)**—A cryptographically irreversible checksum (page 1140) for an entire packet. AH guarantees that the packet is authentic.

+   * **Encapsulating Security Payload (ESP)**—Encrypts a packet to make the data unreadable.

+   * **IP Payload Compression (IPComp)**—Compresses a packet. Encryption can increase the size of a packet, and IPComp counters this increase in size.

+   * **Internet Key Exchange (IKE)**—Provides a way for the endpoints to negotiate a common key security. For AH to work, both ends of the exchange must use the same key to prevent “man-in-the-middle” (see footnote 3 on page 1114) from spoofing the connection.

While IPSec is an optional part of IPv4, IPv6 (page 387) mandates its use. It may be some time before IPv6 is widely implemented, however.

# NETWORK SECURITY GUIDELINES

Some general guidelines for establishing and maintaining a secure system follow. This list is not complete but rather is meant as a guide.

+   * Fiberoptic cable is more secure than copper cable. Copper is subject to both active and passive eavesdropping. With access to copper cable, all a data thief needs to monitor your network traffic is a passive device for measuring magnetic fields. In contrast, it is much more difficult to tap