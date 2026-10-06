
# Data Packets

After you have established a connection with the network (whether it is physical or wireless), you need to send data. The first part is to identify where you want to send it. We will start off discussing IP version 4 addresses; we will look at IPv6 a bit later in this chapter. All computers (as well as routers) have an IP address that is a series of four numbers between 0 and 255 separated by periods, such as 192.0.0.5 (note that this is an IPv4 address). The second part is to format the data for transmission. All data is ultimately in binary form (1s and 0s). This binary data is put into packets, all less than 65,000 bytes. The first few bytes are the header. Header tells where the packet is going, where it came from, and how many more packets are coming as part of this transmission. There is actually more than one header, but for now, we will just discuss the header as a single entity. Some attacks that we will study (IP spoofing, for example) try to change the header of packets to give false information. Other methods of attack try to intercept packets and read the content (thus compromising the data).

A packet can have multiple headers. In fact, most packets will have at least three headers. The IP header has information such as IP addresses for source and destination, as well as what protocol the packet is. The TCP header has information such as port number. The Ethernet header has information such as the MAC address for source and destination. If a packet is encrypted with Transport Layer Security (TLS), it will also have a TLS header.

# IP Addresses

The first major issue to understand is how to get packets to their proper destination. Even a small network has many computers that could potentially be the final destination of any packet sent. The Internet has millions of computers spread across the globe. How do you ensure that a packet gets to its proper destination? The problem is not unlike addressing a letter and ensuring it gets to the correct destination. Let's begin by looking at IP version 4 addressing because it is the most common in use today, but this section also discusses IP version 6.

An IP version 4 address is a series of four three-digit numbers separated by periods. (An example is 10.22.98.198.) Each of the three-digit numbers must be between 0 and 255. You can see that an address of 107.22.98.466 would not be a valid one. The reason for this rule is that these addresses are actually four binary numbers: The computer displays them to you in decimal format. Recall that 1 byte is 8 bits (1s and 0s), and an 8-bit binary number converted to decimal format will be between 0 and 255. The total of 32 bits means approximately 4.2 billion possible IP version 4 addresses exist.

The IP address of a computer tells you a lot about that computer. The first byte (or the first decimal number) in an address tells you what class of network that machine belongs to. Table 1-1 summarizes the five network classes.

# TABLE 1-1 Network Classes

| Class | IP Range for the First Byte | Use |
|---|---|---|
| A | 0–126 | Extremely large networks. No Class A IP addresses are left. All have been used. |
| B | 128–191 | Large corporate and government networks. All Class B IP addresses have been used. |
| C | 192–223 | The most common group of IP addresses. Your ISP has Class C address. |
| D | 224–239 | These are reserved for multicasting (transmitting different data on the same channel). |
| E | 240–255 | Reserved for experimental use. |

These five classes of networks will become more important later in this book (or should you decide to study networking a deeper level). Observe Table 1-1 carefully, and you will probably discover that the IP range of 127 was not listed. This omission is because it is reserved for testing. The IP address 127.0.0.1 designates the machine you are on; this address is often referred to as the *loopback address*.

These particular classes are important as they tell you what part of the address represents the network and what part represents the node. For example, in Class A address, the first octet represents the network, and the remaining three octets represent the node. In Class B address, the first two octets represent the network, and the remaining two represent the node. Finally, in Class C address, the first three octets represent the network, and the last represents the node.

There are also very specific IP addresses and ranges you should be aware of. Private IP addresses are another issue. Certain ranges of IP addresses have been designated for use within networks; these cannot be used as public IP addresses but can be used for internal workstations and servers. Those addresses are:

- 10.0.0.0 to 10.255.255.255
- 172.16.0.0 to 172.31.255.255
- 192.168.0.0 to 192.168.255.255

A good analogy is a subnet. Within a single subnet, each number must be unique. There are other subnets, many of which have their own subnet. You can think of private IP addresses as numbers that must be unique within their network, but public IP addresses are more like mailing addresses. Those must be unique worldwide. When communicating from office to office, you use public IP addresses. You can communicate within your network using private IP addresses, but to communicate with any computer outside your network, you have to use public IP addresses.

One of the roles of a gateway is to perform what is called network address translation (NAT). Using NAT, a router takes the private IP address on outgoing packets and replaces it with the public IP address of the gateway so that the packet can be routed through the Internet.

# CHAPTER 1 Introduction to Network Security

Sometimes new people have trouble understanding public and private IP addresses. We have already discussed IPv4 addresses; now let's turn our attention to subnetting. If you are already familiar with this topic, feel free to skip this section. For some reason this topic gives students a deal of trouble. We will begin with a conceptual understanding. Subnetting is simply chopping up a network into smaller portions. For example, if you have a network using the IP address 192.168.1.X (X being whatever the address is for the specific computer), then you have allocated 256 possible IP addresses. What is subnetting?

More technically, the subnet mask is a 32-bit number that is assigned to each host to divide the 32-bit binary IP address into network and node portions. You also cannot put in any number you want. The first value of a subnet mask must be 255; the remaining values can be 255, 254, 252, 248, 240, or 128. Your computer will take your IP address and the subnet mask and use a binary AND operation to combine them.

It may surprise you to know that you have a subnet mask even if you have not subnetting. If you have a Class C IP address, your subnet mask is 255.255.255.0. If you have a Class B IP address, your subnet mask is 255.255.0.0. And finally, if it is Class A, your subnet mask is 255.0.0.0.

Now think about these relationship to binary numbers. The decimal value 255 converts to 11111111 in binary. So you are literally “masking” the portion of the network address that is used to define the network, and the remaining portion is used to define individual nodes. Now if you have fewer than 255 nodes in your subnet, you need something like 255.255.240 for your subnet. If you convert 240 to binary, it is 11110000. That means the first three octets and the first 4 bits of the last octet define the network. That means you could have as many as 1111 (in binary) or 15 (in decimal) nodes on this subnet. This is the basic essence of subnet.
