# CHAPTER 20 Post Office Protocol and Internet Mail Access Protocol (POP and IMAP) 515

![](bbox=[0.159, 0.118, 0.841, 0.516])

Figure 20-1 Sending and receiving mail with SMTP and POP

the message, taking care of retransmissions, handling delays, and so on, is then left to the well-connected server. Figure 20-1 shows this relationship.

Early users of POP found certain aspects of the protocol too limiting. Features such as being able to make a master copy of a user's e-mail on the server with a cached copy on the client were missing. This led to the development of IMAP.

The earliest Request for Comments (RFC) RFC 1064, 1988. After IMAPv2 led to another update in the protocol specifications, and thus, IMAPv4 is currently at its first revision—IMAP4rev1 (RFC 3501).

The essence of IMAP has evolved can be best understood by thinking of how access works in one of three modes: online, offline, and disconnected. The online mode is as having direct file system access to the mail store (for example, having read access to the /var/mail file system). The offline mode is how POP works, where the client is assumed to be disconnected from the network except when explicitly pulling its e-mail. In offline mode, the server normally does not retain a copy of the mail.