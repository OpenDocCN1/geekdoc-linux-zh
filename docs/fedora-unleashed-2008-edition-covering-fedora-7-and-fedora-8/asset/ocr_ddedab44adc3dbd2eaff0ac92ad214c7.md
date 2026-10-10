+   ▸ **Class B**—Consists of networks defined by the first two octets, with the first ranging from 128 to 191. The “128.” network is also reserved for local network use. There are 16,382 Class B networks—each with 65,534 possible hosts.

+   ▸ **Class C**—Consists of a network defined by the first three octets, with the first ranging from 192 to 223. The “192.” network is another that is reserved for local network use. There are a possible 2,097,150 Class C networks of up to 254 hosts each.

No host portion of an IP address can be all 0s or 255s. These addresses are reserved for local network broadcasts. Broadcast messages are not typically seen by users. IP addresses with all 0s in the host portion are reserved for network-to-network broadcast addresses.

These classes are the standard, but a netmask also determines in what class your network is. The netmask determines what part of an IP address represents the network and what part represents the host. Common netmasks for the different classes are as follows:

+   ▸ **Class A**—255.0.0.0

+   ▸ **Class B**—255.255.0.0

+   ▸ **Class C**—255.255.255.0

Because of the allocation of IP addresses for Internet hosts, it is now impossible to get a Class A network. It is also nearly impossible to get a Class B network (all the addresses have been given out, but some companies are said to be willing to sell theirs), and Class C network availability is dropping rapidly with the current growth of Internet use worldwide. See the following sidebar.

# Limits of Current IP Addressing

The current IPv4 address scheme is based on 32-bit numbering and limits the number of available IP addresses to about 4.1 billion. Many companies and organizations (particularly in the United States) were assigned very large blocks of IP addresses in the early stages of the growth of the Internet, which has left a shortage of “open” addresses. Even with careful allocation of Internet-connected host IP addresses and the use of network address translation (NAT) to provide communication to and from machines behind an Internet-connected computer, the Internet might run out of available addresses.

To solve this problem, a newer scheme named IPv6 (IP version 6) is being implemented. It uses a much larger addressing solution based on 128-bit addresses, with enough room to include much more information about a specific host or device, such as global positioning server (GPS) or serial numbering. Although the specific details about the entire contents of an IPv6 address have yet to be finalized, all Internet-related organizations appear to agree that something must be done to provide more addresses. It’s difficult to gauge just how big the Internet actually is, but according to Internet World Stats, some 1.224 billion people use the Internet as of September 2007. Multiply that by the number of mail servers, newsgroup servers and other web servers that are attached to the web and you will quickly find that the range of addresses supplied by IPv4 is quickly running out.