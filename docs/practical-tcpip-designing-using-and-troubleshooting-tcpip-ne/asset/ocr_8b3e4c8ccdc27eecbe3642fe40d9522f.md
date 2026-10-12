# ## 14.3 Lab – components of a very simple HTTP session

Like POP, SMTP, and IMAP e-mail, HTTP uses TCP as its transport, and the conversation between client and server consists of plain-text commands. This lets us use *telnet* as a simple client to interact with a Web server, by connecting to HTTP's well-known port, which is 80. We'll use the **HTTP GET** command to retrieve a page. Below is a very simple **HTTP** session, connecting from Bob to the Web server on Alice, and retrieving a small **HTML** page:

```
```
bob# telnet alice http
Trying 192.0.2.17...
Connected to alice.example.com.
Escape character is '^]'.
GET /htiw.htm
<HTML>
  <HEAD>
    <TITLE>Baby's first web page</TITLE>
  </HEAD>
  <body>
    <P>The fat cat sat on the rat.</P>
  </BODY>
</HTML>
Connection closed by foreign host.
bob#
```
```

Running *tcpdump*, with options “-N” (print only local machine addresses as names rather than numbers), “-t” (no timestamps), and “-f” (don't print the domain part of the name), we can see what's involved:

```
```
bob.1024 > resbox.domain:   49507+ A? alice.  (33)
resbox.domain > bob.1024:    49507 1/2/2 A alice (132)
bob.1031 > alice.www:       S 1691288354:1691288354(0) win 16060
alice.www > bob.1031:       S 2962874098:2962874098(0) ack 169128
bob.1031 > alice.www:       .   ack 1 win 16060 <nop,nop,timestam
bob.1031 > alice.www:       P 1:16(15) ack 1 win 16060 <nop,nop,t
alice.www > bob.1031:       .   ack 16 win 16060 <nop,nop,timestam
alice.www > bob.1031:       P 1:128(127) ack 16 win 16060 <nop,no
alice.www > bob.1031:       F 128:128(0) ack 16 win 16060
bob.1031 > alice.www:       .   ack 128 win 16060 <nop,nop,timestam
bob.1031 > alice.www:       .   ack 129 win 16060 <nop,nop,timestam
bob.1031 > alice.www:       F 16:16(0) ack 129 win 16060 <nop,nop
alice.www > bob.1031:       .   ack 17 win 16060 <nop,nop,timestam
```
```

+   1. Bob looks up the hostname “alice” in the DNS server on Resbox and gets Alice's IP address

+   2. Bob connects to Alice's IP address on port **www** (which is 80), and you see the three-way handshake (SYN, SYN-ACK, ACK)

+   3. Bob sends an **HTTP GET** request. This consists of a single line, containing the command and the name of the page that the client is requesting, */htiw.htm*. The request in this case consists of 15 bytes, including the carriage-return and linefeed at the end, as line 6 of the trace shows.

Request names are case sensitive: if you use *get* instead of **GET** the server will return an error

+   4. Alice replies with the little Web page above, which consists of 127 bytes

+   5. Alice terminates the connection, and we see the usual connection close – **FIN**, **ACK**, **FIN**, **ACK**.