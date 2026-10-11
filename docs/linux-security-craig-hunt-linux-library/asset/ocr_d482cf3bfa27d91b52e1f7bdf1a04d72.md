by looking at the Post Office Protocol (POP), and continue by examining the Internet Mail Access Protocol (IMAP).

# # The Post Office Protocol (POP) V.3

When the Internet saw the transition away from time-sharing systems where all the mail was read online, to the PC-on-every-desktop model, it became evident that most PCs were not going to be up and running all the time. This made it necessary to devise a protocol by which users could send mail and request their incoming mail from a dedicated server. While the existing SMTP protocol was a good fit to handle outgoing mail, a new protocol had to be created to address the incoming mail. Enter the POP protocol. In 1984, the IETF drafted the first RFC document outlining the standard (RFC918) only to be enhanced in 1988 (RFC1081) into version 3 of the protocol (POP3), which is still in use today.

POP3 became the de facto standard for mail-retrieval clients throughout the late 1980s and early 1990s, until it began losing steam in favor of the IMAP protocol (discussed in the next section). There are still, however, millions of POP3 clients in operation today, with thousands of POP3 servers to which they connect, many of them hosted by Linux servers.

Of all the POP3 server packages, the one that has enjoyed the most popularity in the Linux community is the Qualcomm, Inc.'s Qpopper. Originally developed as a companion to the (also wildly successful) Eudora mail client, Qpopper was positioned as a full-featured, open-source POP3 server, whose development continues today. This section focuses on Qpopper because it's the best representative of this class of servers and discusses the security issues involved with its installation and use.

# ## APOP

The APOP functionality extends the standard POP3 authentication sequence by adding the ability to send authentication information without exposing the password in the clear. The basic operation of the POP3 protocol is as follows:

+   1. The client connects to the appropriate port (TCP 110) of the POP3 server.
+   2. The client supplies a username and password that authenticates them to some mailbox on the server.
+   3. The client queries mailbox statistics (for example, number of new messages, total messages, etc.).
+   4. The client retrieves a number of messages.
+   5. The client deletes a number of messages.
+   6. The client closes connection.