# Basic Communication

Now you can put it all together. When you communicate with another computer, you call the hostname or fully qualified domain name of the other computer, such as linux1 or linux1.mommabears.com. TCP/IP uses either the /etc/hosts file or a DNS server to translate this name to an IP address. With a network mask, your computer can figure out whether the destination computer is on your LAN. If the computer is on your LAN, your message searches computer by computer, if necessary, to find the destination.

Once contact is made, each computer identifies its hardware address. Finally, real communication begins. Messages are sent between computers using host and destination addresses that correspond to the appropriate hardware addresses.

# IP Addressing

Every computer on a TCP/IP network needs an IP address before it can communicate with others. You or your ISP can assign a permanent address, or IP addresses can be "leased" from what is known as a Dynamic Host Configuration Protocol (DHCP) server.

To set up IP addresses for your network, you need a network address and a network mask. IP addresses that share the same network address and network mask are on the same LAN.

Network addresses fall into one of five different address classes. Network masks define a range of IP addresses that you can assign with a specific network address.

Every network with a connection to other networks needs a gateway IP address for that connection. In Linux, you can limit access to and from your network with the /etc/hosts.allow and /etc/hosts.deny files.

![](bbox=[0.1, 0.68, 0.22, 0.82])

> IP addresses consist of four numbers between 0 and 255. One example of a valid IP address is 254.1.158.33. Each of these numbers is also known as an octet. This format of numbers and periods is sometimes known as dotted-decimal notation or dotted-quad format.

The Sair Linux/GNU exams assume the use of IP version 4 (IPv4), which has been in use since the 1970s. Although the Internet is currently in transition to IP version 6 (IPv6), your IPv4 addresses will still work after the transition is complete.