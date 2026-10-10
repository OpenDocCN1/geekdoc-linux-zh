( www.freeswan.org ). Openswan is included in the Fedora software repository (to install it, type yum install openswan ).

+   Crypto IP Encapsulation (CIPE) — Using this method, IP packets are routed across selected IP interfaces as encrypted UDP packets. CIPE is easy to set up and carries less overhead than PPP over OpenSSH, so you should get better performance. One drawback is that, because it is not a standard VPN, CIPE is not available on all platforms and was dropped from Fedora.

Chapter 14 explained the basic idea behind using a VPN and described how to configure NetworkManager to communicate with a remote openvpn server. In this chapter, I provide an overview of the features and tools in IPsec and a detailed description of configuring an OpenVPN server in Fedora.

# Understanding IPsec

To provide more secure transmission of TCP/IP data in the new Internet Protocol version 6 (IPv6) standard, developers of that standard created the Internet Protocol Security (IPsec) architecture. With IPsec, encrypted communication is possible right at the IP level and methods for providing access control, data integrity, authentication, and traffic flow confidentiality are standardized as well.

In practical terms, organizations that have computers that need to communicate on public networks in ways that are secure and private can create VPNs with IPsec. Unlike other VPN implementations (such as CIPE), which require a manual exchange of keys to work, IPsec offers an automated way of creating security associations between communications endpoints and managing keys.

With slow adoption of IPv6 in the United States and other places, IPsec has been included (backported) into the IPv4 protocol, which is still the most common IP version used on the Internet. That backport was added into the IP protocol included with the Linux 2.6 kernel that comes with Fedora starting with version 2. The Internet standard RFC2401 document describes the IPsec architecture.

# Using IPsec protocols

IPsec consists of two primary protocols: Authentication Header (AH) and Encapsulating Security Payload (ESP). Look in the /etc/protocols file and you’ll see that AH is assigned to protocol number 51 and ESP is assigned to protocol number 50.

To authenticate peer computers and exchange symmetric keys, IPsec uses the Internet Key Exchange (IKE) protocol. At the beginning of communication between two host computers using IPsec, IKE does the following: