# 298 Understanding TCP/IP

# Next-generation IP (IPv6)

When the 4-byte IP address was created, the number of available addresses seemed adequate. Now, however, the 4-byte addresses are running out. The Internet Engineering Task Force (IETF) recognized the potential for running out of IP addresses in 1991, and began work on the next-generation IP addressing scheme. They called it IPng (for Internet Protocol Generation) and intended that it would eventually replace the old 4-byte addressing scheme (called IPv4).

IPv6 is designed to be an evolutionary step from IPv4. The proposed standard provides direct interoperability between hosts using the older IPv4 addresses and new IPv6 hosts. The idea is that users can upgrade their systems to use IPv6 when they want and that network operators are free to upgrade their network hardware without affecting current users of IPv4. Sample implementations of IPv6 are being developed for many operating systems including Linux. For more information about IPv6 in Linux, consult the IPv6 FAQ/HOWTO at www.linuxhq.com/IPv6/.

Alternative addressing schemes for IPng were proposed and debated. The final contender, with a 128-bit (16-byte) address, was dubbed IPv6 (for IP Version 6). On September 18, 1995, the IETF declared the core set of IPv6 addressing to be an IETF proposed Standard.

The IPv6 128-bit addressing scheme allows for 340,292,366,920,938,463,374,631,768,216 unique hosts! This should last for us for a while!

![](bbox=[0.133, 0.535, 0.233, 0.613])

In decimal notation, a byte (which has 8 bits) can have a value between 0 and 255. A valid IP address can use only the numbers between 0 and 255 in the dotted-decimal notation.

# Internet services and port numbers

The TCP/IP suite has become the lingua franca of the Internet because many standard services are available on any system that supports TCP/IP. These services make the Internet tick by facilitating the transfer of mail, news, and Web pages. These services go by well-known names such as the:

+   - DHCP (Dynamic Host Configuration Protocol) is for dynamically configuring TCP/IP network parameters on a computer. DHCP is primarily used to assign IP addresses and other networking information (such as name server, default gateway, and domain names) to configure TCP/IP networks. The DHCP server listens on port 67.

+   - FTP (File Transfer Protocol) is used to transfer files between computers over the Internet. FTP uses two ports — while control information is exchanged on port 21.