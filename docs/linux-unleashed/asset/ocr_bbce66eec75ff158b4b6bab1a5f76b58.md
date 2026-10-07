TFTP enables both text and binary transfers. As with both Telnet and FTP, TFTP uses a server process (tftpd on a UNIX system) and an executable, usually called tftp. Because of the nature of TFTP, Windows and similar PC-based operating systems don't usually support it. In most cases, TFTP is used between UNIX machines.

A sample character-based TFTP session is shown here, with full trace options and binary transfers turned on:

```
> tftp
tftp> connect tpci_hpw54
tftp> trace
Packet tracing on.
tftp> binary
Binary mode on.
tftp> verbose
Verbose mode on.
tftp> status
Connected to tpci_hpw54.
Mode: octet Verbose: on Tracing: on
Rexmt-interval: 5 seconds, Max-timeout: 25 seconds
tftp> get /usr/rmaclean/docs/draft1
getting from tpci_hpw54:/usr/rmaclean/docs/draft1 to /tmp/draft1 [octet]
sent RRQ <file=/usr/rmaclean/docs/draft1, mode=octet>
received DATA <block1, 512 bytes>
send ACK <block=1>
received DATA <block2, 512 bytes>
send ACK <block=3>
received DATA <block4, 128 bytes>
send ACK <block=3>
Received 1152 bytes in 0.2 second 46000 bits/s]
tftp> quit
```

You may have to use TFTP in some cases where network conditions are bad or the server doesn't accept standard FTP. Usually, though, FTP should be your choice of protocol.

# Using Telnet

Telnet gives you the capability to log into a remote server and act as though you were physically attached to that machine and all its resources. If the server has a powerful CPU, you can use that CPU instead of your weaker local processor. If the server has some special devices, such as a scanner, CD-writer, or magneto-optical storage device, you can use them. You can also use the remote server's file system.

Using Telnet is quite simple because the protocol takes care of all the configuration and setup processes for you. As part of its startup, Telnet passes a series of messages between the client and server that establish the terminal identifications and special features your