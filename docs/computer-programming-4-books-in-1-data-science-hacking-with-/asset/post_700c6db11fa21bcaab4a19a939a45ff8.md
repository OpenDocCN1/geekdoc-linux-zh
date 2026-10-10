
## IP Sub-netting

Routed IP environments require that your pool of IP addresses be sub-netted. This allows each sub-net to see itself as a separate segment of the larger internetwork. The router then ties together the various sub-nets into one network. The router knows how to route traffic to the correct segment because it builds a routing table. The routing table is basically the network's roadmap.

IP sub-netting is fairly complex, and so to make this discussion informative but still digestible at an introductory level, we will limit our exploration of sub-netting to one class of IP addresses; we will look at an example of sub-netting a Class B range of IP addresses. The mathematical tricks that we use to sub-net the Class B network can also be used to sub-net a Class A or Class C network (although sub-netting Class C networks greatly limits the number of usable IP addresses that you end up with).

Sub-netting is a two-part process.

First, you must determine the sub-net mask for the network (it will be different than the default sub-net masks; for example, the default for Class B is 255.255.0.0). After figuring out the new sub-net mask for the network, you must then compute the range of IP addresses that will be in each sub-net.

## IPv4 vs. IPv6

Currently, IP version 4 (IPv4) addresses are the Internet IP addresses of choice. As mentioned, these addresses are composed of four sets of eight bits. In the future, we will likely adopt the IP version 6 (IPv6) address scheme. IPv6 differs in form and substance from IPv4 in two ways:

- IPv6 addresses have eight 16-bit numbers (128 bits total), usually expressed in four-digit hexadecimal form. The range of a single 16-bit number is greater than that of an eight-bit number, spanning from zero to 65,535.
- The 16-bit numbers in an IPv6 address are separated by colons rather than periods.

Why make the switch? Because under IPv4, there are not enough numbers available to assign one to every computer or device on the Internet that needs one. IPv6 solves this problem, offering 2 raised to the 128th power addresses; in contrast, IPv4 offers only 2 raised to the 32nd power—although masking and private-address strategies have been used to extend the number of available IPv4 addresses on the Internet.

![](img/e34dde0654d255bebea353c553e965ac_236_0.png)

## What is CCNA?

CCNA stands for Cisco Certified Network Associate. It is a widely held certification among computer network enthusiasts. This certification is valid for any computer network engineer that starts with the low-level network engineers, network support engineers and network administrators through to network specialists.

The certification program was founded in 1998. An estimated 1 million certificates have been awarded to qualified persons ever since.

CCNA program spans numerous crucial networking concepts. It is an essential foundational course for interested candidates in the preparation for current and emerging networking technologies.

## CCNA Scope

The following are the major topics that feature greatly in CCNA certification program:

- Networking essentials—which includes definition of network; description of network components; and the basic network setup and configuration requirements.
- IP addressing
- The OSI Reference Model
- IP Routing
- Routers—routing protocols (OSPF, EIGRP and RIP)
- WLAN and VLAN
- Network device security
- Network security and management
- Network troubleshooting

## Why CCNA?

- The CCNA certificate is a trusted validation of a networking professional's ability to manage and administer a routed and medium-level network. It is the validation of an individual's understanding of a network, and their ability to operate and configure it. It also certifies a person's ability to troubleshoot the network.
- The course offers lessons on how to meet network users' requirements by proper determination of a network topology.
- Candidates learn how to make point-to-point networks.
- Protocol routing for connecting networks is also realized through CCNA certification.
- Network address construction is adequately explained in the CCNA certification course.
- The course offers a comprehensive explanation on the establishment of a connection with a remote network.
- CCNA certification is offered using easy-to-understand study material.
- The course is a prerequisite for other important CISCO certification programs such as CCNA Wireless, CCNA Security and CCNA Voice, among others.
- CCNA certification program equips learners with the necessary knowledge and skills for the installation, configuration and management of a small LAN and WAN service networks.

## Different Forms of CCNA Certifications

There are two main approaches to fulfilling a CCNA certification course:

1. Combined CCNA Exam
2. ICND1 Exam and ICND2

Note that every CCNA certificate is only valid for a period of 3 years. Every holder of a CCNA certificate is expected to take a fresh examination after every 3 years.

## Chapter 8: Fundamentals of Network Security

Network security is one of the most important aspects in overall computer [security]. Now, more than ever, having an adequate security protocol which can combine both functionality and protection is essential for all types of users.

Amid the large amount of threats out there, users must have a system which they can rely on when going about their usual day-to-day business. In that regard, the need to integrate these aspects motivates users to find the ideal solution to their individual needs.

In this chapter, we are going to be taking a look at the fundamentals of network security, guidelines and best practices, as well as, the most common threats found lurking today. In addition, we are going to be discussing the ways in which the average user can take better care to avoid becoming the victim of unscrupulous folks out there.

### The only thing to fear, is fear itself

It’s natural for the average user to fear hackers. This may lead the average user to spend a pretty penny on security measures which may or may not offer the combination of security and functionality that such users need. In fact, the most common side effect of top-notch security measures is a slow system. For example, a solid online security system will essentially scan every single bit of information that goes through their system. However, this can lead to an overall slowing of internet connection speeds.

As a result, users may feel that they have been short-changed by the performance of their security system. Other systems may sacrifice certain safety features in exchange for faster performance and internet speeds. Yet, these tradeoffs may leave critical information and transactions vulnerable to unwanted folks.

That is why the first thing to keep in mind is that breaking the bank out of fear of being vulnerable may lead you to overspend on a system that, while keeping your system safe, may end up costing you more in the end. That is why finding the right balance is essential; striking a balance between features and performance is the ultimate goal of all users. Therefore, we will be taking an objective look at what threats are out there, which ones you will most likely be vulnerable to, and what you can do to protect yourself.

Please keep one thing in mind: of all the horror stories out there, some may not necessarily apply to [you] so long as you don’t engage in the types of practices that attract hackers and fraudsters such as [handling] a large volume of financial transactions on a daily basis. Consequently, taking the proper steps to secure the transactions that you do make, will go a long way toward keeping your information, and your money, safe.

### What to be on the Lookout for

Threats are out there, and they are real. However, the most important thing to keep in mind is that hackers and fraudsters love feeding on low-hanging fruit.

What does that mean?

It means that cheaters are looking for vulnerable people who don’t know any better. Hence, they
