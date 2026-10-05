
# Network Interface Cards and Drivers

# Applications and Services

| RPC | DCOM | Named Pipes | Mail Services |
|---|---|---|---|---|
| Winsock API | Telephony API | Redirectors | Servers | NetBios OS |
| TCPIP | IPX/SPX | NetBEUI | AppleTalk | ICA | ULC |
| Native ATM | IP over ATM | ATM Lane | NDIS Network Device Interface Specification |

Connection-Oriented NDIS
Connection-Oriented Miniports

Connectionless NDIS
Connectionless Miniports

![](img/1c1e7552b53cca888836b6c6895bdb48_56_0.png)

## 3.1.4 Configuring Your Network Interface Card

### 3.1.4.1 Windows 2000

When you install Windows 2000, your network adapter is automatically detected. If you are doing an interactive install, you will have to supply network information like the IP address, subnet mask, and gateway. If you use Dynamic Host Configuration Protocol (DHCP), most of this information will be configured in the LAN automatically. As, the process will select the appropriate driver and then bind the adapter to TCP/IP if you later install another protocol, such as NWLink (IPX/SPX), it will then bind the adapter to both TCP/IP and NWLink. Some drivers will also load card-specific information when they install. If you want to change these settings, start the Device Manager, expand the Network adapters entries, right-click the icon representing your adapter, and choose Properties.

If you change NICs or add additional hardware, Windows 2000 will automatically detect the new cards from the installation media or from a source you specify. Again, you may be asked to provide some additional configuration information.

Most systems transmit Ethernet frames in LLC format, while Windows 2000 does by default. To set the default transmitting format to 802.3/II, edit the Registry and set the value to 1:

```
HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces
```

### 3.1.4.2 HP-UX

HP-UX 11 supports multiple logical interfaces per NIC. IP addresses associated with the logical interfaces can be on the same or different subnets. If you require both Ethernet and IEEE 802.3 (SNAP) encapsulations on the same NIC, you must configure two logical interfaces with separate IP addresses in different subnets. The interface name for Ethernet is lan; for IEEE 802.3 it is snap. The loopback interface is always l0.

If you had your NIC in place when you installed your HP-UX system, the operating system installation process installed its driver into the kernel, created device files for it, and installed the appropriate networking software. For Ethernet, this software is called LAN/9000. Because of its popularity, we will assume you are installing an Ethernet card. (Other HP working software includes Token Ring/9000, FDDI/9000, and 100VG-AnyLan Link.) If you use Switch cards or add additional ones, follow the procedure below.

It is much easier to configure your NIC using Hewlett-Packard's System Administrator (SAM) than to do everything with commands and startup files. The same is true about other forms of UNIX. Make sure the LAN card and driver are installed in the system before you use SAM to configure the software. (These steps come from Hewlett-Packard's *Installing and Administering LAN/9000 Software*, pp. 32–34.) Log in as *root* and do the following:

1. At the HP-UX prompt, **type sam**.
2. Select the **Networking and Communications** item of the SAM main window.
3. Select the **Network Interface Cards** item from the **Networking and Communications** window.
4. Highlight the LAN card that you want to configure from the object list.
5. Verify that the hardware path is correct for your LAN card.
6. If you are configuring the first logical interface for a card type (also called the *initial interface*), choose **Configure** from the *Actions* menu to open the **Configure LAN Card**

If you are adding logical interfaces to a card type, choose **Add IP Logical Interface** from the *Actions* menu to open the **Configure LAN Card** window.

a. Enter the information about the LAN card. To do so, press the Tab key to move through the data entry fields.

NOTE: Enter the information about the LAN card. To do so, press the Tab key

b. Enter the information about the LAN card. To do so, press the Tab key to move through the data entry fields.

NOTE: Enter the information about the LAN card. To do so, press the Tab key

c. Enter the information about the LAN card. To do so, press the Tab key to move through the data entry fields.

NOTE: Enter the information about the LAN card. To do so, press the Tab key

d. Enter the information about the LAN card. To do so, press the Tab key to move through the data entry fields.

NOTE: Enter the information about the LAN card. To do so, press the Tab key

e. Enter the information about the LAN card. To do so, press the Tab key to move through the data entry fields.

NOTE: Enter the information about the LAN card. To do so, press the Tab key

f. Enter the information about the LAN card. To do so, press the Tab key to move through the data entry fields.

NOTE: Enter the information about the LAN card. To do so, press the Tab key

g. Enter the information about the LAN card. To do so, press the Tab key to move through the data entry fields.

NOTE: Enter the information about the LAN card. To do so, press the Tab key

h. Enter the information about the LAN card. To do so, press the Tab key to move through the data entry fields.

NOTE: Enter the information about the LAN card. To do so, press the Tab key

i. Enter the information about the LAN card. To do so, press the Tab key to move through the data entry fields.

NOTE: Enter the information about the LAN card. To do so, press the Tab key

## 3.2 Conclusion

## The Internet Layer

We now proceed to the next level of the four-layer TCP/IP model, the internet layer, sometimes called the network layer. (If the word internet is not capitalized, it refers to the inter-networking of networks in a generic sense. The word Internet (with a capital I) refers to the now public internetwork.) The Internet layer enables pieces of data, usually called datagrams, to find their correct destination, even if the destination is several networks away. Within the TCP/IP protocol suite, IP, the Internet Protocol, is responsible for the routing of these datagrams. Because of the recent Internet phenomenon, TCP/IP is omnipresent these days, making it a key to system interoperability. TCP/IP runs on a wide variety of platforms: mainframes, Macs, VAXs, and of course UNIX and Windows 2000. Therefore, your desktop computer may run Windows 2000, you can connect to a Web server running HP-UX or Linux, since the Web relies on Hypertext Transfer Protocol (HTTP), a TCP/IP application. So let's look at TCP/IP concentrating in this chapter on IP, the network layer.

TCP/IP began as a part of the Defense Department's Advanced Research Projects Agency in 1969. It was incorporated into BSD UNIX in the early 1980s and is part of every current implementation of UNIX. Microsoft released a completely rewritten TCP/IP suite with the release of Windows NT 3.5 in 1994. Whatever the source, any vendor claiming to prove TCP/IP must ensure that it adheres to the Internet Standards set forth in the Request for Comments (RFC) document series. According to RFC 2026, The Internet Standards Process – Revision 3, p. 3, “The Internet standards process is an activity of the Internet community by the Internet Architecture Board (IAB) and the Internet Engineering Steering Group (IESG)” are the official means of these bodies to regulate Internet standards. You can find the RFCs in a number of locations on the Internet, one of which is the Internet Engineering Task Force's Web site at www.ietf.org.

A first step in internetworking is to standardize on TCP/IP. Older network applications often used NetBEUI (NetBIOS Extended User Interface) to communicate with each
