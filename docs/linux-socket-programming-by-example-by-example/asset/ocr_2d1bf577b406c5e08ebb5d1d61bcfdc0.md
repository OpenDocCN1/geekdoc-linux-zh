The programmer typically chooses one of the following values for the socket type argument:

+   - SOCK_STREAM \*
+   - SOCK_DGRAM \*
+   - SOCK_SEGPACKET
+   - SOCK_RAW

The entries marked with an asterisk (*) are the two you'll normally use. The SOCK_SEGPACKET type is commonly used on non-Internet protocols such as X.25, or the amateur radio protocol AX.25. There are a few additional types that could be listed here. However, they are outside of the scope of this text.

# NOTE

The SOCK_RAW macro specifies that the programmer wants a “raw” interface to the socket. This allows the programmer more direct control over the communications and its packets. However, it also requires an intimate knowledge of the protocol and its underlying packet structure. For this reason, the SOCK_RAW socket will not be studied in this book.

# Understanding the SOCK_STREAM Socket Type

The SOCK_STREAM socket type is used when you want to perform stream I/O with a remote socket. A stream in the socket sense is the same concept that applies to a UNIX pipe. Bytes written to one end of the pipe (or socket) are received at the other end as one continuous stream of bytes. There are no dividing lines or boundaries. There is no record length, block size, or concept of a packet at the receiving end. Whatever data is currently available at the receiving end is returned in the caller's buffer.

![](bbox=[0.1, 0.7, 0.15, 0.85])

An example to review might help illustrate the stream I/O concept. In this example, there is a local process on your host that has connected to a remote process on a remote host. The local host is going to send data to the remote host in two separate write(2) calls as follows:

+   1. The local process writes 25 bytes of data to be sent to the remote process, by socket. The Linux kernel might or might not choose to buffer this data. Buffering helps improve the performance of the kernel and the network facilities.
+   2. Another 30 bytes are written by the local process to be sent to the remote process.
+   3. The remote process executes a function designed to receive data from the socket. The receiving buffer in this example allows up to 256 bytes to be read. The remote process receives the 55 bytes that were written in steps 1 and 2.