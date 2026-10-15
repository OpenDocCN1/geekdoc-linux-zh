
10. The link layer of www.midwinter.com notices that there’s a packet addressed to it coming over its Ethernet wire (or whatever type of networking that system uses). It grabs the packet and begins to decode it; it strips away the Ethernet-specific material, leaving a packet that the Internet layer can handle.

11. When the Internet layer receives the packet, it strips and examines its own layer of material. If it notices that the packet was broken into parts by its counterpart on your system, it will hold onto the first part it receives for a specified period of time, and if more parts arrive, combine them. When this job is done, it passes the packet up to the transport layer, and more specifically, to the TCP handler.

12. TCP, like the Internet layer, checks to see if the packet had been broken up into pieces before transmission, and waits for all pieces to arrive. When they’re all present, TCP combines them, checks the destination program (or, more precisely, the destination port), and passes the combined data packet on to that program.

13. The recipient program in the application layer is a Web server such as Apache. Apache notes that it has just received a request to send the file /lurk/eplist.html to your computer, and it prepares to do so.

14. The process now repeats itself, this time taking the file /lurk/eplist.html from www.midwinter.com to your computer, and specifically to Netscape.

15. Netscape processes the file. Most Web pages these days contain graphics. These don’t come with the original Web page itself. Instead, the Web page includes a reference to another file on the server. Thus, for each graphic image, the entire round-trip sequence repeats. Similar requests go out for embedded sounds, JavaScript, and so on. The need for multiple requests for a single page is why a Web page will sometimes load some graphics but not others; if some sort of blockage occurs on the Internet after your system has received some images but not others, you’ll have an incomplete Web page on display.

As you can see, even a fairly simple Internet transfer can take quite a few steps to complete. Similar processes occur for other types of Internet accesses, including printing a file to a remote printer, running an X program on a remote computer, and so on. Some of these processes can involve temporally extended connections (as in running a program remotely). For these, TCP maintains a connection, which basically just means that the client and server programs keep listening for packets from each other, and maintain information in memory such as their respective IP addresses, so they don’t need to continue looking up this information.

## Alternatives to TCP/IP

Although TCP/IP is a very common set of networking protocols, and the most important one for the Internet as a whole, it’s not the only networking stack. Particularly in an office setting, other protocols can be extremely important. Described broadly, these other protocols work much like TCP/IP, though the details do differ.

Linux supports many of these protocols, or provides ways to support them in conjunction with TCP/IP. Because TCP/IP is designed to transmit any type of data, it's possible to encapsulate one protocol within another. For instance, you can pass NetBEUI packets within TCP/IP packets. When you do this, you effectively place one network stack on top of another one; the link layer of the first stack serves as the application layer of the second. The resulting data packet is depicted in Figure 2.3. Of course, for this to work you do need support for such encapsulation on both systems.

| Ethernet Header | IP Header | TCP Header | ftp Header | NetBIOS, AppleTalk, or NetWare Headers | NetBIOS, AppleTalk, or NetWare Data | Ethernet Footer |
|---|---|---|---|---|---|---|
| TCP/IP Data |

### FIGURE 2.3

When TCP/IP is used to transport a secondary networking protocol's packets, the TCP/IP data area carries not only the ordinary data, but also the headers associated with the secondary protocol.

### UUCP

UNIX-to-UNIX Copy (UUCP) is a networking protocol that's designed specifically for modem connections. It was in wide use as a means to transfer email and files in the days before the Internet became ubiquitous, but it's not as widely used today. Unlike many other protocols, UUCP can't be used over Ethernet cabling.

As I've already mentioned, TCP/IP can also be used over a modem, via the PPP and SLIP link-layer protocols. Why UUCP, then? For one thing, there's history—UUCP was developed in the 1970s, well before SLIP or PPP. For another thing, UUCP has built-in support for scheduled transfers. For instance, suppose you write several emails on your Linux computer over the course of a day. If you were using PPP, you might connect to your ISP every time you finish an email. With UUCP, the typical procedure would be for your system to keep the emails in a queue and transfer them all at once, without supervision. This can help reduce telephone use and costs if the connections are long distance, particularly because the transfers can be done whenever long-distance rates are lowest.
