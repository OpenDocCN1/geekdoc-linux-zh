commonly used to establish a secure point-to-point virtual network (VPN, page 1280) that allows two hosts to communicate securely over an insecure channel, such as the Internet. This protocol provides integrity, confidentiality, authenticity, and flexibility of implementation that supports multiple vendors.

IPSec is an amalgamation of protocols (IPSec = AH + ESP + IPComp + IKE):

+   - **AH (Authentication Header)**—A cryptographically secure, irreversible *checksum* (page 1242) for an entire packet. AH guarantees that the packet is authentic.

+   - **ESP (Encapsulating Security Payload)**—Encrypts a packet to make the data unreadable.

+   - **IPComp (IP Payload Compression)**—Compresses a packet. Encryption can increase the size of a packet, and IPComp counteracts this increase in size.

+   - **IKE (Internet Key Exchange)**—Provides a way for the endpoints to negotiate a common key securely. For AH to work, both ends of the exchange device must use the same key to prevent a “man in the middle” (see the tip on page 1160) from spoofing the connection.

While IPSec is an optional part of IPv4, IPv6 (page 293) mandates its use.

# NETWORK SECURITY GUIDELINES

The following list of general guidelines for establishing and maintaining a secure system is not a complete list, but rather is meant as a guide.

+   - Fiberoptic cable is more secure than copper cable. Copper is subject to both active and passive eavesdropping. With access to copper cable, all a data thief needs to monitor your network traffic is a passive device for measuring magnetic fields. In contrast, it is much more difficult to tap a fiberoptic cable without interrupting the signal. Sites requiring top security keep fiber- optic cable in pressurized conduits, where a change in pressure signals that the physical security of the cable has been breached.

+   - Avoid leaving unused ports available in public areas. If a malicious user can plug a laptop into the network without being detected, you are at risk of a serious security problem. Network drops that will remain unused for extended periods should be disabled at the switch, preventing them from accepting or passing network traffic.

+   - Use the latest in wireless encryption. At the time of this writing, WEP is totally broken and WPA with TKIP is seriously flawed. WPA2 with AES is generally believed to be relatively secure.

+   - Many network switches have provisions for binding a hardware address to a port for enhanced security. If someone unplugs one machine and plugs in another machine to capture traffic, chances are that the second machine will have a different hardware address. When it detects a device with a different