
send data destined to 192.168.x.x addresses to the Ethernet board and everything else over the PPP link.

Note that the sending and receiving computers don’t need to use the same type of network hardware. For instance, you can use a PPP dialup connection to communicate with a computer that’s linked using Ethernet. In such a situation, however, one or more of the intervening computers must have two interfaces, and the intervening machine must be configured to route the traffic from one interface to another. This router strips the link layer’s header, places a new header on the packet, and sends it on to the second interface.

One variant on the router model is implemented in IP masquerading. In this case, the intervening computer peels back more layers in the packaging and meddles with the return IP address, thus hiding the originating system’s address. The intervening computer then watches for replies to this packet and meddles again to send the packet to the originating system. Does this sound dishonest? In some sense it is, but it’s a very useful technique when you have a limited number of IP addresses at your disposal. You can use this technique to link a small home network to the Internet via a dialup PPP connection, for instance. You can then cruise the Web using a Mac with no modem, to name just one possible application.

> **Note**
> 
> The 32-bit IP address limits the theoretical maximum number of computers on the Internet as a whole to about four billion. In practice, the limit is lower than this for assorted reasons, and we’re fast approaching the limit on the number of computers the current IP addressing system can handle. IP masquerading can actually increase the limit because it allows several computers to share a single IP address. IP masquerading is, however, fundamentally a local solution to local IP address limitations.

## The Result of Data Wrapping

The end result of the data encapsulation described here is shown in Figure 2.2, which depicts a typical data packet. Figure 2.2 shows an ftp packet transmitted over Ethernet, but other protocols and media would result in similar layering.

Upon receipt, each layer of the TCP/IP stack strips away the header (and footer, if applicable) it’s assigned and uses the information in that header to pass the data on to the appropriate next layer in the stack. Ultimately, the destination application receives the data at the core of this packet, without the various headers.

| Ethernet Header | IP Header | TCP Header | ftp Header | Data | Ethernet Footer |

## FIGURE 2.2

Data transmitted over a TCP/IP network is "wrapped" in headers (and sometimes footers) for each layer of the TCP/IP stack.

## An Example: Following a Web Page Access

As an example of how all the preceding steps work, let’s follow what happens when you access a Web page using a browser such as Netscape Navigator:

- 1. You type the uniform resource locator (URL) for the Web page into the browser. For instance, you might type http://www.midwinter.com/lurk/eplist.html to get a list of episodes from the TV series Babylon 5.
- 2. Netscape calls the Linux library function gethostbyname, which links up with DNS. As name resolution could be as simple as looking up an address in a cache or as complex as an entire set of network accesses similar to the one I’m describing, we’ll just say it happens and leave it at that. The result is that Netscape now knows the numeric IP address of www.midwinter.com, which is 199.165.129.193.
- 3. Netscape prepares an appropriate hypertext transfer protocol (HTTP) request to ask for the file /lurk/eplist.html. Note that although you entered both the address and the file on one line, Netscape has broken these down into two separate parts of the request.
- 4. Netscape sends the HTTP request to the transport layer, specifying a TCP transmission.
- 5. TCP adds its own headers onto the request and, if necessary, breaks it down into packets.
- 6. TCP sends the request to the Internet layer for IP to process. Here, addresses, flags, and more headers are added to the data request.
- 7. IP passes the request on to the link layer.
- 8. The link layer determines to which network device the request should go and adds appropriate formatting for that device. Let’s suppose for the sake of argument that the request goes out over an Ethernet adapter. Once the Linux Ethernet drivers have transmitted the packet, it’s out of the Linux TCP/IP stack.
- 9. The data packet or packets make their way through some unknown number of intermediate hosts, each of which processes the packet to a greater or lesser extent. Ultimately, it reaches the link layer of www.midwinter.com.
