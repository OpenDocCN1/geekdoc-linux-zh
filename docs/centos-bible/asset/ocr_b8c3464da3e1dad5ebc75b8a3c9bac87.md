# # Part IV Networking

continued

You can filter for certain special activities on the network, using the gateway, broadcast, or multicast primitives. Entering *gateway host* lets you find packets sent to a gateway host that is neither a Source nor a Destination for the packet (which is determined because the Ethernet address doesn't match either of those IP addresses). Enter **ether broadcast** to monitor broadcast packets on your Ethernet network, such as announcements from name servers *announcing* availability. Likewise, you could filter for multicast packets on ether or IP protocols (*ether multicast*).

The following tips will help you interpret what the data means:

+   - The Source and Destination columns show where each packet came from and where it went. If the "Enable name resolution" option is on (which is recommended), the hostname associated with IP packets is displayed. This makes it much easier to see which computer is communicating with you.

+   - To see all activity associated with a particular location, click on the Source or Destination column. Packets will be sorted alphabetically, making it easier for you to scroll through the activity list for the location that interests you.

+   - If you are trying to debug a particular feature, click on the Protocol column to gather activities based on protocol. For example, if you were trying to get Samba to work (for Windows file or printer sharing), sorting by protocol would enable you to see all NetBIOS and NBNs (NetBIOS name server) requests that came to your computer.

+   - To mark a packet of interest to you, click the middle mouse button. This will highlight the packet, making it easier to find later. (If you have only a two-button mouse and you indicated during installation that it should emulate a three-button mouse, you can click both mouse buttons together to emulate the middle mouse button.)

The Info column gives you details about the intention of the packet. For example, you can see the type of service that was requested (such as HTTP for Web Service or FTP for file transfer). You can see what information is being broadcast and determine when attempts to find particular host computers are failing. If you believe that someone is using your network improperly, you can see which sites they are visiting and the services they are requesting.

Another handy option is one that lets you follow the stream of TCP information. Click Tools > Follow TCP Stream. The Contents of TCP stream window that appears lets you see the total output of the HTTP, SMTP, or other protocol being used. Of course, viewing data being transmitted by protocols is useful only if it is in plaintext. Although the fact that more and more data and service requests are being encrypted makes it more difficult to debug using Wireshark, it also makes it harder for bad guys on your network to steal your data.