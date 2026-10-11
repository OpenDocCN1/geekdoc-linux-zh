+   * Shutting down a socket does not permit recovery if more communication is to be continued.

+   * The addition of an extra connection can be quite expensive when hundreds or thousands of users are pondering on your server.

+   * Company firewall restrictions make it even more desirable to perform all your networking needs within the one socket connection.

Practical examples of programs that use out-of-band data are the telnet, rlogin, and ftp commands. The first two programs send the interrupt character as urgent data to the remote end. This allows the remote end to flush all unprocessed input and to discard with any unsend terminal output. This facilitates a quick interrupt of a running process, which might have been spewing oodles of output to your screen. The ftp command uses out-of-band data to abort a file transfer.

# Sockets and Out-of-Band Data

It was stated earlier that TCP streams have some pitfalls when using the socket out-of-band concept. It is important to re-emphasize that the socket interface itself is not the limiting factor. The out-of-band concept is actually mapped to the urgent data mode of TCP/IP communications. TCP streams are important to networking today and this chapter will focus only on the socket use of out-of-band data as it applies to TCP urgent data.

Consequently, while the two terms are technically different, they will often be used interchangeably.

It is also necessary to point out that the limitations pertaining to TCP urgent data do not necessarily apply to other protocols that might be used with the socket interface. For example, if you look at out-of-band data for infrared communications, you’ll need to research the underlying protocol for it before reaching any conclusions about its capabilities.

# Variations in Implementation

The implementation of TCP, unfortunately, has two different interpretations of how urgent data should be handled. These differences will be described fully, later in the chapter (the impatient can refer to Table 14.2 later in the chapter). The different interpretations are

+   * The RFC793 interpretation of the TCP urgent-pointer

+   * The BSD interpretation of the TCP urgent-pointer

This dichotomy has come about because the original TCP specification permitted both interpretations. Subsequently, a “Host Requirements” RFC