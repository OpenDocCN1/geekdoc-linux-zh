# The Generic Linux Configuration 119

MAILER(local) macro includes the local mailer that is used to deliver local mail between users of the system and the prog mailer that is used to send mail files to programs running on the system. Even though these mailers will be added by default, MILLER(local) is traditionally included in the configuration. In part this tradition arises from the fact that most configurations are built from a sample configuration file, and all of the generic configuration files include the MILLER(local) macro. It takes more effort to remove the mailer than it does to leave it in, and it costs nothing to leave it in the configuration. In fact, it provides the slight benefit of making the configuration "self-documenting."

The MILLER(smtp) macro includes all of the mailers needed to send SMTP mail over a TCP/IP network. The mailers included in this set are:

+   - smtp This handler can handle only traditional seven-bit ASCII SMTP mail. It is outdated because most modern mail networks handle a variety of data types.

+   - smtp This mailer supports Extended SMTP (ESMTP). It understands the ESMTP protocol extensions and it can deal with the complex message bodies and enhanced data types of MIME. This is the default mailer used for SMTP.

+   - smtp8 This mailer sends eight-bit data to the remote server, even if the server does not indicate that it can support eight-bit data. Normally, a server that supports eight-bit data also supports ESMTP and thus can advertise its support for eight-bit data in response to the EHLO command. (See Chapter 1, "Internet Protocols," for a description of the SMTP protocol and the EHLO command.) It is possible, however, to have a connection to a remote server that can support eight-bit data but does not support ESMTP. In rare circumstance, this mailer is available for use.

+   smtp This mailer allows the destination system to retrieve mail queued on the server. Normally, the source system sends mail to the destination in what might be called a "push" model, where the source pushes out to the destination. demand SMTP allows the destination to "pull" mail down from the mail server when it is ready to receive the mail. This mailer implements the ETRN command that permits on-delivery. (See Chapter 1 for a description of the ETRN command.)

+   relay This mailer is used when SMTP mail must be relayed through another mail server. Several mail relay hosts can be defined.

Every server that connects to or with the Internet uses the MILLER(smtp) set of mailers, and most systems on isolated networks use these mailers because they use TCP/IP on network. Despite the fact that a majority of Sendmail services require these mailers, installing them is not the default. To support SMTP mail, you must add the MILLER(smtp) macro to your configuration.

![](bbox=[0.933, 0.281, 0.982, 0.362])