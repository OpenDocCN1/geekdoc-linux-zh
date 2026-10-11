+   * *Header verification*—A number based on the header’s contents, computed
+   when it is first built and each time it is changed. Recipient machines make the
+   same computation and ensure that their number matches the original. If the
+   numbers are not the same, the header was damaged, and a new copy of the
+   datagram is requested from the source.
+   * *Source IP address*—The IP address the datagram came from.
+   * *Destination IP address*—The IP address the datagram is headed to.
+   * *Options*—Various options that can be attached to the header. Mostly unused
+   except when a TCP/IP connection is being established.
+   * *Zeros*—The last part of an IP header is a sequence of zeros that ensure that
+   the full header size is a factor of 32.

> TIP: Go to www.faqs.org/rfcs/rfc760.html to read the official specification for how an IP datagram is put together.

# The Transport Layer

The Transport layer actually moves the data across the Internet. Two primary
protocols are used for this purpose: TCP and the User Datagram Protocol (UDP)—
not to be confused with the term *datagram* discussed in the previous section.
TCP handles services that require a steady connection with error checking and
recovery. Its data is sent in streams, where each part is sequentially numbered
and re-sent if not received at the other end. A value called the *Maximum Trans*
*mission Unit* (*MTU*) is set for each network, declaring the maximum packet size
this network handles. When a packet’s size exceeds the MTU, TCP breaks it into
*fragments*, which are pieces of a packet. Each fragment has its own header infor-
mation, which contains everything needed to piece the packet together again. If
only Humpty Dumpty had been so organized.

UDP, on the other hand, does no error checking and does not even truly connect
with the receiving machine. It still has its uses, however, for both very small
amounts of data and very large. In something like streaming audio or video, it is
not imperative that every single byte reach its source, and waiting to resend can
warp the results worse than losing bits and pieces. UDP is also useful on LANs
that have nearly ideal throughput. In fact, UDP is faster than TCP in these circum-
stances because there is no error checking overhead.

# The Application Layer

The top of the TCP/IP layer grouping is the Application layer, which is where the
various programs that utilize the Internet reside: Web browsers using the Hypertext
Transfer Protocol (HTTP), File Transfer Protocol (FTP) clients getting files from
servers, email programs sending mail over the Simple Mail Transfer Protocol
(SMTP), and more. Each of these protocols has its own way of doing things, but
at some point, each passes and receives data from the Internet layer. Table 7.2