Mason is well worth obtaining and using, if for nothing other than the learning experience it will provide.

# The Network Mapper (nmap)

The Network Mapper (nmap) is a very sophisticated port scanner. It can generate a variety of different types of packets. It can generate all types of normal packets like TCP, UDP, ICMP, ftp, and many others. It can also generate fragments and oversized packets. It is a very good utility to use to test your firewall. The bad-guys will use it against you, so you should use it first. You can obtain it from

http://www.insecure.org/

# Additional Firewall Software

There are two publicly available proxy-based firewall packages that operate well in conjunction with ipchains. They are the Firewall Toolkit (FWTK) and SOCKSv5. Both of these packages offer full-featured proxy services (although they do so in different ways) and user authentication. You can find out more about FWTK at

http://www.tis.com/research/software/

Also, Internet Security: A Professional Reference, cited in General Firewall References on page 488, contains configuration details about FWTK. SOCKS can be obtained from

http://www.socks5.nec.com/

# Virtual Private Networks and Encrypted Tunnels

In Secure Shell Alternatives on page 310, we pointed out some of the available tools for the purpose of building encrypted tunnels and/or virtual private networks (VPN).

# THE NEXT GENERATION...

The good news is that ipchains is much more flexible and capable than ipfwadm. The other bit of good news is that the follow-on replacement to ipchains is in the works—it will provide significant functionality enhancements. There will also be a suit of tools to allow for ipchains (and possibly ipfwadm) syntax to be used. The next-generation replacement for ipchains is called netfilter;