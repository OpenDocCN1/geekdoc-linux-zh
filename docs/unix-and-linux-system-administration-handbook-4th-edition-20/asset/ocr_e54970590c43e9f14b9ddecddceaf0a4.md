# Wireshark and TShark: tcpdump on steroids

If you are using Solaris zones, note that snoop only works properly in the global zone, even when you are debugging a problem in a nonglobal zone.

# Wireshark and TShark: tcpdump on steroids

Wireshark includes both a GUI interface (wireshark) and a command-line interface (tshark). Linux distributions make it a snap to install. UNIX administrators should check wireshark.org, which hosts the source code and a variety of precompiled binaries.

Wireshark can read and write trace files in the formats used by many other packet sniffers. Another feature is that you can click on any packet in a TCP conversation and ask Wireshark to reveal (splice) the payload of all the packets in the stream. This feature is useful if you want to examine the data transferred during a complete TCP exchange, such as a connection to transferred an email message across the network.

Wireshark's capture filters are functionally identical to tcpdump's since Wireshark uses the underlying libcap library. Watch out, though—one important catch with Wireshark is the added feature of "display filters," which affect what you see rather than what was actually captured by the sniffer. The display filter syntax is more powerful than the libcap syntax supported at capture time. The display filters may look somewhat, but they are not the same.

Wireshark has built-in dissectors for a wide variety of network protocols, including many used to implement SANs. It breaks packets into a structured tree of information in which every bit of the packet is described in plain English.

Exhibit B on the next page shows Wireshark's capture of a DNS query and response. The table near the top of the screen shows the two packets involved. The first packet is the request on its way to the DNS server, and the second packet is the answer back. The response packet is selected, so the middle panel shows its disassembly. The lower panel shows the packet in the form of raw bytes.

The expanded section of the tree shows the packet's DNS payload. The raw content can also be interesting to look at because it sometimes contains telltale fragments that hint at what is going on. Scanning the text is especially handy when there is no built-in dissector for the current protocol. Wireshark's menu provides many great examples to get you started. Experiment!