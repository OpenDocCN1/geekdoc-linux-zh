**stream** In the socket context: A stream socket is a connection-orientated socket. This is different from a datagram socket, which is connectionless. In the standard I/O context: a stream represents a FILE control block that is open for reading or writing.

**TCP** Transport Control Protocol layer, which is used on top of the IP protocol layer. This layer adds flow control and data integrity to the lower IP level.

**telnet** A network client program that provides a terminal session for the user. See also *login*.

**thread** A sequential flow of control within a process. There can be several threads operating in parallel within one process, each representing an independent flow of control. All memory is shared between all threads within one process.

**Trojan horse** A usually dangerous program designed to masquerade as some other program. By impersonating a normal program, it gets run by an unwitting user, which can then cause harm or capture information that should be kept secret.

**UDP** User Datagram Protocol.

**URG bit** A TCP protocol header bit that indicates urgent data is present.

**urgent data** The special data that is sent in urgent mode. See also *urgent mode*.

**urgent mode** The TCP protocol provides a facility where the sending end can indicate to the receiving end that “urgent data” has been placed into the normal stream of data. The receiving end then becomes notified that urgent data exists in its incoming data stream, but it remains up to the receiving end to determine how to process this data.

**urgent pointer** This is a TCP protocol pointer that points to either the urgent data byte itself (RFC793) or the byte that follows the urgent data byte (BSD). This pointer is only computed and used at the receiving end when the TCP URG bit is set in the packet header.

**wild socket address** This is a socket address that is left unspecified. This is often done when the choice of network interface is not known in advance, allowing the address to be dynamic.

**X.25** A packet-switched network protocol recommended by CCITT in 1976, based upon the ISO networking model.

**YP** Sun Microsystems's Yellow Pages is now known as NIS (the name Yellow Pages is a registered trademark of British Telecom PLC in the