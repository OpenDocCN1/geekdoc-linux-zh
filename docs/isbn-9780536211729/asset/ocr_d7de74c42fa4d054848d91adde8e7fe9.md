```
0x0000  4500 004c fe58 4000 3906 de9b 9252 8a06  E..L.x8.9..R..
0x0010  455d 0302 b2cc 0019 5892 21fd aa16 6506  E]......X!....e.
0x0020  8018 16d0 3cc4 0000 0101 080a 2f63 dfae  ....<....../c....
0x0030  4ec1 3cc0 4548 4c4f 206d 7572 70hy 792e  N..<EHLO.murphy.
0x0040  6465 6269 616e 2e6f 7267 0d0a            debian.org..
```

# ## CAPTURING AN SSH CONVERSATION

Although it’s not possible to actually capture an SSH conversation, you can look at some of the connection setup portions of the protocol. Because SSH is encrypted, though, none of the credentials or other data during the actual session is available for you to view. It should be noted, however, that if you can gain access to the private key of the server, you could theoretically decrypt the contents of the SSH connection. Doing this is well beyond the scope of this text.
	I’ll leave it as an exercise for the reader to capture an SSH connection, including setup, should you want to view what a normal connection looks like for SSH.

# ## CAPTURING OTHER TCP-BASED PROTOCOLS

Capturing other TCP-based protocols follows much the same process as that in the examples shown. For example, capturing POP3 connections can be accomplished and the entire stream can be captured because POP3, like SMTP, is not encrypted during transit. One protocol is of particular interest because it has confused network administrators for a long time. That protocol is FTP.
	FTP utilizes two TCP ports, 20 and 21. Port 21 is normally used for commands and is sometimes referred to as the control channel. Port 20 in FTP is used for data and is sometimes aptly titled the data channel. Therefore, if you want to capture FTP traffic with TCPDump, you need to grab both ports 20 and 21 to see everything.
	A trend over the past few years has been protocols that use nonstandard ports to circumvent firewalls and packet capturing and filtering. Such programs, including much of the peer-to-peer software, can be somewhat difficult to find during packet captures because most of the data during the conversation is binary and is thus not human-readable.

# ## CAPTURING A DNS QUERY

TCPDump handles DNS queries a little differently than a packet that’s simply TCP. More information can be gleaned from just the initial packet result line as opposed to making it necessary to increase the snaplen with the -s option. For example, consider the following trace of a simple DNS query that was looking for the IP address of a host named www.braingia.org:

```
21:18:39.289121  192.168.1.10.1514  > 192.168.1.1.53: 60792+ A?
www.braingia.org.  (34)  (DF)
21:18:39.289568  192.168.1.1.53  > 192.168.1.10.1514: 60792*- 1/2/
2  A  192.168.1.50  (118)  (DF)
```