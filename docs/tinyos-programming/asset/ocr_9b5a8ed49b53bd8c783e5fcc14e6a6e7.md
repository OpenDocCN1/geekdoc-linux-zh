# 7  Mote-PC communication

This chapter shows how to build a PC application that talks to motes. As we saw in Section 6.4, a PC typically interacts with a mote network by exchanging packets with a distinguished base station mote (occasionally, several motes) over a serial connection (Figure 6.2, page 95). The PC code in this chapter is written in Java, using the Java libraries and tools distributed with TinyOS. TinyOS also includes libraries and tool support for other languages (e.g. C). Please refer to the TinyOS documentation for more information on these other languages. The TinyOS Java code for communicating with motes is found under the net.tinyos package.

# 7.1  Basics

At the most basic level, PCs and motes exchange packets that are simply sequences of bytes, using a protocol inspired by, but not identical to, RFC 1663 [24] (more details on the protocol can be found in TEP 113 [7]). This packet exchange is not fully reliable: the integrity of packets is ensured by the use of a CRC, but invalid packets are simply dropped. Furthermore:

+   - Packets sent from a PC to a mote are acknowledged by the mote (but there is no retry if no acknowledge is received) – this prevents the PC from overloading the mote with packets.
+   - Packets sent from a mote to a PC are not acknowledged.

While it is possible to write mote communication code by reading and writing the raw bytes in packets, this approach is tedious and error-prone. Furthermore, any changes to the packet layout (e.g. adding a new field, changing the value of a constant used in the packets) requires corresponding changes throughout the code.

These problems are avoided on motes by using nesC’s external types (Section 3.5.3) to specify packet layouts, and named constants to specify values. Two tools, mig and ncg, allow these packet layouts and constants to be used in PC programs: mig (for “message interface generator”) generates code to encode and decode a byte array whose layout is specified by a nesC external type, and ncg (for “nesC constant generator”) extracts named constants from a nesC program. Both tools generate code for multiple languages, including Java.