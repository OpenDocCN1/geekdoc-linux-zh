The third and fourth sections will vary depending upon the type of packet. If there is a TCP packet, the third section is TCP and the fourth section is protocol specific. The TCP section will contain the source and destination ports plus a few lines of the protocol-specific packet headers. For UDP packets, the third section in the verbose output is UDP, which normally contains the source and destination port information. It may also contain information about the length and checksum of the UDP packet. For ICMP packets, the third section is ICMP, which contains information about the type of ICMP request and the checksum for the packet.

Each output line is labeled with the name of a layer, as in **<LAYER>: <data>**. The following example demonstrates an output line for TCP:

TCP: Source port = 22

It is easy to tell where each section of a layer starts. Figure 9.14 shows the header lines for the IP section.

![](bbox=[0.07, 0.44, 0.92, 0.74])

You can filter the verbose mode with the grep command. If you are trying to debug a problem, you need to look at each layer in order to isolate the layer in which the problem occurs. Some of the most common problems include Ethernet frames being directed to the wrong MAC address and incorrect IP addresses. To display this type of information, you can use a command such as this:

% snoop - | grep <LAYER>

Replace the word **LAYER** with the name of the layer you want, such as the IP layer or TCP layer.