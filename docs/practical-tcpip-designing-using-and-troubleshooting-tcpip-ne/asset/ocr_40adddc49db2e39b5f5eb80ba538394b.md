# 15.1 UDP is a connection-less and “unreliable” transport protocol

The end-user applications that we've looked at so far (SMTP, POP, and IMAP e-mail, HTTP Web browsing, the telnet application itself) all use TCP as their transport:

+   * there are usually multiple transfers between client and server, involving an ongoing session rather than the exchange of a single packet. The effect of one command or request depends on what occurred earlier in the client/server conversation (e.g. if you delete a file abc.txt in an FTP session, exactly which file is removed depends on what directory you were in at the time, which is determined by your earlier commands)
+   
+   * they often exchange large amounts of data.

In this chapter we consider a different transport, UDP (User Datagram Protocol). In some ways, UDP is similar to TCP:

+   * UDP is a transport protocol: it deals with communication only between the two end-points (e.g. the client application on your machine, and the server application on the remote machine). Intermediate routers don't bother with the UDP data in the packets they are forwarding – the routers operate only at the lower-down IP or network layer (Figure 15.1).
+   
+   * UDP uses ports to distinguish between traffic for multiple UDP applications on the same machine, and to send the correct packets to the appropriate application. (This is called demultiplexing.) UDP and its port provides the interface between the application program and the IP networking layer. We discuss ports in more detail in Module 15.3.

![](bbox=[0.13, 0.52, 0.9, 0.81])

UDP differs from TCP in some important respects:

+   * UDP is "datagram-oriented," TCP is session-oriented. A datagram is a self-contained packet of information; UDP deals with individual datagrams or packets sent from client to server, or vice versa