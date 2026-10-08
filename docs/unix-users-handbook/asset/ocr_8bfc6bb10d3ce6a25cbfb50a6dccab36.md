| | | |
|---|---|---|
| data | 46-1500 bytes | 38-1492 bytes for 802.3; the difference in these two data sizes (MTU) can be seen with the *ifconfig* command |
| crc | 4 bytes | checksum to detect errors |


Figure 9-2 Ethernet Encapsulation

![](bbox=[0.02, 0.3, 0.1, 0.37])

One interesting item to note is the difference in the maximum data size between IEEE 802.3 and Ethernet of 1492 and 1500 bytes, respectively. This is the Maximum Transfer Unit (MTU). The **ifconfig** command covered shortly displays the MTU for your interface. The data in Ethernet is called a *frame* (the re-encapsulation of data at the next layer up is called a *datagram* in IP, and encapsulation at two levels up is called a *packet* for TCP).

Keep in mind that Ethernet and IEEE 802.3 will run on the same physical connection, but there are indeed differences between the two encapsulation methods. With your UNIX systems, you don't have to spend much, if any, time setting up your network interface for encapsulation.

# *Network Layer*

![](bbox=[0.02, 0.72, 0.1, 0.79])

Next we work up to the third layer, which is the network layer. This layer on UNIX systems is synonymous with Internet Protocol (IP). Data at this layer is called *datagrams*. This is the layer that handles the routing of data around the network. Data that gets routed with IP sometimes encounters an error of some type, which is reported back to the source system with an Internet Control Message Protocol (ICMP) message. We will see some ICMP messages shortly. **ifconfig** and **netstat** are two UNIX commands that are used to configure this routing, which I'll cover shortly.

Unfortunately, the information that IP uses does not conveniently fit inside an Ethernet frame, so you end up with fragmented data. This is really re-encapsulation of the data, so you end up with a lot of inefficiency as you work your way up the layers.