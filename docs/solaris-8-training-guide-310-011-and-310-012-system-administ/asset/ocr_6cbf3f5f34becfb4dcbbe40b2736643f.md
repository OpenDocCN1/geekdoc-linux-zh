# CLASS NETWORKS

There are five classes of IP addresses: A, B, C, D, and E. The following is a brief description of each class.

# Class A Networks

Class A networks are used for large networks with millions of hosts, such as the Internet. A class A network number uses the first 8 bits of the IP address as its network ID. The remaining 24 bits comprise the host part of the IP address. The values assigned to the first byte of class A network numbers fall within the range 0–127. For example, consider the IP address 75.4.10.4. The value 75 in the first byte indicates that the host is on a class A network. The remaining bytes, 4.10.4, establish the host address. The InterNIC assigns only the first byte of a class A number. Use of the remaining 3 bytes is left to the discretion of the owner of the network number. Only 127 class A networks can exist; each of these networks can accommodate up to 16,777,214 hosts.

# Class B Networks

Class B networks are medium-sized networks, such as universities and large businesses with many hosts. A class B network number uses 16 bits for the network number and 16 bits for host numbers. The first byte of a class B network number is in the range 128–191. In the number 129.144.50.56, the first two bytes, 129.144, are assigned by the InterNIC and comprise the network address. The last two bytes, 50.56, make up the host address and are assigned at the discretion of the network’s owner. A class B network can accommodate a maximum of 65,534 hosts.

# Class C Networks

Class C networks are used for small networks containing fewer than 254 hosts. Class C network numbers use 24 bits for the network number and 8 bits for host numbers. A class C network number occupies the first three bytes of an IP address; only the fourth byte is assigned at the discretion of the network’s owner. The first byte of a class C network number covers the range 192–223. The second and third bytes each cover the range 1–255. A typical class C address might be 192.5.2.5, with the first three bytes, 192.5.2, forming the network number. The final byte in this example, 5, is the host number. A class C network can accommodate a maximum of 254 hosts.

# Class D and E Networks

Class D addresses cover the range 224–239 and are used for IP multicasting as defined in RFC 988. Class E addresses cover the range 240–255 and are reserved for experimental use.

# SOLARIS PSEUDO FILE SYSTEMS AND SWAP SPACE

Sometimes referred to as ram-based or virtual file systems, the distinguishing feature is that a pseudo file system does not reside on hard physical media. Pseudo file systems reside only in physical memory while the operating system is running. The pseudo file systems supported in the Solaris 8 operating environment are listed in Summary Table 28.