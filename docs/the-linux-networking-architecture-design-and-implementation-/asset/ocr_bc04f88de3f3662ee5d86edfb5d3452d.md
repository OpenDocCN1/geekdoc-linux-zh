# 14.3.1 Standardized IP Packet Options

Figure 14–9 shows that the IP packet options are appended to the end of an IP header. The length of the Option field is variable, and the end of a packet header has to be aligned to a 32-bit boundary, so an additional padding field of the appropriate length is added (and set to 0 by default). "variable" also means that the packet options can be left out, if they are not required. The Option field can take one or several packet options, where an option can be given in either of two formats:

+   - One single byte describes only the option type. The length of these options is exactly one byte.

The first byte includes the option type, and the second byte contains the length of this packet option. The following bytes include the actual data of that option.

The byte stating the length of the packet option in the second case includes the number of data bytes. The first two bytes are not counted. The option type in the first byte is composed as follows:

The (1-bit) copy flag is required for packet fragmentation. If a packet has to be fragmented, then this bit sets whether this option has to appear in all fragments or may be set in the first fragment onlynThe option class is represented by 2 bits. The (5-bit) option number shows the length of a packet option implicitly (i.e., we can see whether the next byte belongs to this packet option or already belongs to the next option). Table 14–1 lists all IP packet options defined in RFC 791, including their lengths and their defined option numbers and option classes. There are four option classes in total, but only two are currently used. Option class 0 includes packet options for control and management; option class 2 includes debugging and measurement options. The option class 1 and 3 are reserved for future IP packet-option classes.

> FIGURE 14–9 The IP packet header.