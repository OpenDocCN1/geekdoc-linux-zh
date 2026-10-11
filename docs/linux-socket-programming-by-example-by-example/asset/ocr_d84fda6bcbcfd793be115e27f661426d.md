There, you will see that the service labeled telnet is configured as a tcp service on port number 23. This is how the inetd daemon determines the port number it must listen for connects on.

Alternatively, you can simply supply a port number. You will see an example of this later in this chapter.

# ## The SOCKET TYPE FIELD

Although the Linux inetd daemon can accept a number of socket types here, only the types stream or dgram will be discussed for simplicity's sake. For the more curious reader, the inetd(8) man page also lists socket types raw, rdma, and seqpacket types as additional possibilities.

The stream type corresponds to the SOCK\_STREAM socket type for the socket(2) function call. The value dgram requests a SOCK\_DGRAM socket type.

# ## The PROTOCOL FIELD

As you might guess, this selects the protocol to be used for the socket. This value must be a valid entry that appears in the /etc/protocols file (see the section in Chapter 7 titled, “Consulting /etc/protocols File”). Two often- used selections are

+   * tcp for the TCP protocol
+   * udp for the UDP protocol

Other possibilities also exist, but these are the most commonly used.

# ## The FLAGS FIELD

This field is intended for datagram sockets only. Non-dagram sockets (such as stream tcp, for example) should specify the value nowait.

Datagram-oriented servers come in two types. They are

+   * Servers that keep reading UDP packets until they timeout and exit (specify wait for these).
+   
+   * Servers that read one packet and exit (specify nowait for these).

This information is needed by inetd because the handling of dgram traffic is more complex than it is for stream-oriented protocols. This helps the dae- mon determine how it should handle future dgram connects while the server for that service is running. This will be explained in detail later in this chapter.