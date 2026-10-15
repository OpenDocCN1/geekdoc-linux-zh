
## Chapter 7, “Kernel Support Tools”

Not all networks and individual machines are connected to one another through Ethernet cabling. Some are WANs and other solutions require dial-up networking, and this more often than not requires making use of our old friend PPP. In this chapter, you learn the ins and outs of this protocol and what it's capable of, as well as how to utilize the pppd daemon for Linux PPP connections. After that, you learn about rip2d, the daemon that lets you add some basic RIP routing functionality to your PPP connection.

## Chapter 8, “Kernel 2.2.x Routing Daemons”

There are far too many tools to cover in just this one book. In this chapter, we take a look at additional tools such as zebra and iproute2, and also take a look at the differences between the kernel 2.2.x series and 2.4.x series from the point of view of routing.

## Chapter 9, “Inside the Commands”

Linux has a suite of commands that most of us have already used to handle our networking needs. However, most of these tools are actually far more complex than many people realize. This chapter covers the detailed innards of arp, ifconfig, netstat, ping, route, tcpdump, and traceroute. These tools will all serve you well in your networking and routing needs.

## Chapter 10, “Planning Basic Router Layout and Function”

Here's where we really get into the how of routing. Before you get into the actual implementation, you need to have put some serious thought into how you intend to keep your own routing tables manageable and how you plan to help contribute to the overall Internet's tables. By the time you finish this chapter you should be just about ready to start setting up your router.

## Chapter 11, “Linux Routing Basics”

If you picked up this book, you probably don't have a simple network setup. You've got some complicated LAN, a WAN, or even a VPN that you're trying to get working as a single routing unit. This chapter tackles the ins and outs of getting the various popular network types to route seamlessly, which helps with your security because people don't realize that the machines aren't all in the same building.

## Chapter 12, “Network Hardware Components, Technology, and Solutions”

Networks—especially ones that connect to the Internet—don't work without telecommunications hardware. Not only does this chapter cover the various methods of making connections, such as over cable modems and DSL, it also discusses the various kinds of setups you might use to allow remote administration of networks. In addition, there is discussion of the types of router interfaces that exist for digital data transfer.

## Chapter 13, “Building a Routing Kernel”

Whenever you intend to use a machine for a single purpose, or even just a few specific tasks, it’s important to remove as much extraneous functionality as possible. This concern applies not just to programs, but to the kernel as well. Once you’ve pulled out everything you know you don’t need, there’s more to do—namely, enabling any number of esoteric features that you otherwise wouldn’t need. This chapter covers building a custom kernel for your Linux router.

## Chapter 14, “Security and NAT Issues”

Routing just by itself doesn’t have anything to do with helping to secure your network. A router just ensures that your data gets where it needs to go. This chapter covers many of the tools you have available to turn your routing machine into your network’s first line of defense, including packet filtering and mangling, IP masquerading, and NAT.

## Chapter 15, “Monitoring, Analyzing, and Controlling Network Traffic”

In this chapter, we take a step back from the actual routing of data and look at the tools available for Linux that allow us to gather information on how efficient our network is and make corrections to any problems we find. Tools such as SNMP, MRTG, and IPTraf are included, as well as information on how to set quality of service (QoS) rules.

## Appendix A, “Linux Routing Resources”

This appendix is dedicated to helping you quickly locate the many programs mentioned in this book, as well as others we didn’t get to. There are also pointers to the central documents used to define how various Internet and networking protocols work and mentions of various additional resources that might be of use to you in your networking pursuits.

Because things change so rapidly in the networking world, consider these items a jumping-off point to start from.

## Appendix B, “Linux Hardware Routing Solutions”

This appendix is dedicated to routing appliances with Linux under the hood and network cards that you can utilize with Linux to build a router. As the Linux market matures, we expect that this list will grow significantly.
