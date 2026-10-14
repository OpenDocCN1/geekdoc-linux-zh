
## Wireshark: Analyse traffic

We explain all the necessary essentials that you need to know to start using the GUI-enhanced Wireshark, and analyse three kinds of network traffic.

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_101_0.png)

Wireshark is a very popular and extremely capable network protocol analyser that was developed by Gerald Combs. Wireshark was born in June 2006 when Combs renamed the network tool Ethereal, which he also created, as he was changing jobs and couldn’t use the old name anymore. Nowadays, most people use Wireshark and Ethereal has been consigned to history. Your Linux distribution will have a ready to install package for analyser too, so go ahead and install it. You may ask what makes Wireshark different to other network analysers – apart from the fact that it’s free – and why we’re not simply advocating using tcpdump for packet capturing? The main advantage of Wireshark is that it’s a graphical application. Capturing and inspecting network traffic using a graphical user interface is a very helpful thing because it cuts through the complexity of network data. To help the beginner understand Wireshark they will need to understand network traffic. The aim of this article then is to supply a comprehensive introduction to TCP/IP to enable you to come to useful conclusions about the network traffic data you’re analysing. If you run Wireshark as a normal user, you won’t be able to use any network interfaces for capturing, because of the default Unix file permission that network interfaces have. It’s more convenient to run Wireshark as root (sudo wireshark) when capturing data and as a normal user when analysing network data. Alternatively, you can capture network data using the tcpdump command line utility as root and analyse it using Wireshark afterwards. Please keep in mind that on a truly busy network, capturing using Wireshark might slow down a machine or, even worse, might not enable you to capture everything because Wireshark needs more system resources than a command line program. In such cases using tcpdump for capturing network traffic is the wisest solution.

## Capturing network data

The easiest way to start capturing network packets is by selecting your preferred interface after starting Wireshark and then pressing Start. Wireshark will show network data on your screen depending on the traffic of your network. Note that you can select more than one interface. If you know nothing about TCP/IP or the other TCP/IP protocols, you may find the output complicated and difficult to read or understand. In order to stop the capturing process you just select Capture > Stop from the menu. Alternatively, you can press the fourth icon from the left, the one with a red square (which is shorthand for ‘Stop the running live capture’) on the Main toolbar (Note: Its exact location depends on your Wireshark version). This button can only be pressed while you are capturing network data. When using the described method for capturing, you can’t change any of the default Wireshark Capture Options. You can

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_101_1.png)

The TCP packet and the IP packet format.

see and change the Capture Options by selecting Capture > Options from the menu. There you can select the network Interface(s), see your IP address, apply capture filters, put your network card in promiscuous mode, and save your capture data in one or multiple files. You can even choose to stop packet capturing after a given number of network packets or a given amount of time or indeed a given size of data (in bytes).

Wireshark doesn’t save the captured data by default but you can always save your data afterwards. It’s considered good practice to first save and then examine the network packets unless there’s a specific reason for not doing so.

Wireshark enables you to read and analyse already captured network data from a large amount of file formats including tcpdump, libpcap, Sun’s snoop, HP’s nettl, K12 text file etc. This means that you can read almost any format of captured network data with Wireshark. Similarly, Wireshark enables you to save your captured network data in a variety of formats. You can even use Wireshark to convert a file from a given format to another.

You can also export an existing file as a plain text file from the File menu. This option is mainly for manually processing network data or using it as input to another program.

There is an option that allows you to reprint your packets. I have never used this option in real life but it may be useful to print packets and their full contents for educational purposes.

## Display filters

While capture filters are applied during network data capture and make Wireshark discard network traffic that doesn’t match the filter, display filters are applied after capture and ‘hide’ network traffic without deleting it. You can always disable a Display filter and get your hidden data back.

Generally, display filters are considered more useful and versatile than capture filters because it’s unlikely you’ll know in advance what you’ll capture or want to examine. Nevertheless, applying filters at capture time can save you time and disk space and that’s the main reason you might want to use them.

Wireshark will highlight when a display filter is syntactically correct with a light green background. When the syntax is erroneous, the background becomes pink.

Display filters support comparison and logical operators. The **http.response.code == 404 && ip.addr == 192.168.1.1** display filter shows the traffic that either comes from the 192.168.1.1 IP address or goes to the 192.168.1.1 IP address that also has the 404 (Not Found) HTTP response code in it. The **!bootp && !ip && !arp** filter excludes BOOTP, IP and

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_102_0.png)

ARP traffic from the output. The **eth.addr == 01:23:45:67:89:ab && tcp.port == 25** filter displays the traffic from or to network device with the 01:23:45:67:89:ab MAC address that uses TCP port number 25 in its incoming or outgoing connections.

Keep in mind that display filters don’t magically solve problems. They are extremely useful tools when used correctly but you still have to interpret the results, find the problem and think about the possible solutions yourself.

When defining rules please remember that the **(ip.addr != 192.168.1.5)** expression doesn’t mean that none of the ip.addr fields can contain the 192.168.1.5 IP address. It actually means that one of the ip.addr fields should not contain the 192.168.1.5 IP address. Therefore, the other ip.addr field value can be equal to 192.168.1.5. You can think of it as ‘there exists one ip.addr field that is not 192.168.1.5’. The correct way of expressing it is by typing **!(ip.addr == 192.168.1.5)**. This is a common misconception.

You also remember that MAC addresses are truly useful when you want to track a given machine on your LAN because the IP of a machine can change if it uses DHCP but its MAC address is more difficult to change.

It is advisable that you visit the display filters reference site for TCP related traffic at http://bit.ly/WireSharkTCP. For the list of all the available field names related to UDP traffic, it’s advisable to look at http://bit.ly/WireSharkUDP.

## About TCP/IP, TCP and IP

TCP/IP is the most widely used protocol for interconnecting computers and it is closely related to the internet that it’s extremely difficult to discuss TCP/IP without talking about the Internet and vice versa. Every device that uses it has:

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_102_1.png)

### The TCP protocol

TCP stands for Transmission Control Protocol. The main characteristic of TCP is that it’s reliable and makes sure that a packet was delivered. If there’s no proof of packet delivery, it resends the packet. TCP software transmits data between machines using segments (also called a TCP packet). TCP assigns a sequence number to each byte transmitted, and expects a positive acknowledgment (or ACK) from the receiving

TCP stack. If the ACK is not received within a timeout interval, the data is retransmitted as the original packet is considered undelivered. The receiving TCP stack uses the sequence numbers to rearrange the segments when they arrive out of order, and to eliminate duplicate segments. The TCP header includes both the Source Port and Destination Port fields. These two fields, plus the source and destination IP addresses are

combined to uniquely identify each TCP connection. Ports help TCP/IP stacks in network connected devices (PCs and routers etc) to distribute traffic among multiple programs executing on a single device. If a service wants to be seen as reliable it’s usually based on TCP, otherwise it’s based on IP. But as you can imagine, reliability comes at a cost and therefore isn’t always desirable.

**Subscribe to Linux Format** See www.myfavouritemagazines.co.uk/lin
