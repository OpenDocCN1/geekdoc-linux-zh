The format of the EHLO command is simple—just the keyword EHLO followed by the domain name of the sending system. The response from the receiving system is the standard hello acknowledgement followed by a list of keywords. The keywords shown in Listing 1.5 are from a Red Hat Linux system running Sendmail version 8.11.0. By its nature, the EHLO command evokes different responses from different systems.

# Extended Service Keywords

Two of the advertised services are basic SMTP commands defined in RFC 821. HELP provides access to the online help system, EXPN displays the addresses in a mailing list. This system advertises these services in the keyword list because many sites do not implement these commands.

Some of the keywords in list indicate service extensions that are defined in various RFCs.

ENHANCEDSTATUSCODES This server uses the enhanced status codes that with Delivery Status Notifications (DSNs). The enhanced status codes are defined in RFC 1893, "Enhanced Mail System Codes."

8BITMIME This keyword indicates that the server can accept eight-binary data, which means 8bit and binary data types can be sent to this system without any additional encoding. This extension is defined in RFC 1652 ("SMTP Service Extension for 8-bitMIMEtransport").

+   >>> Mail From:<craigani.foobirds.org> SIZE=73

In this example, the SIZE keyword tells the receiving system that the message carries 73 bytes.

DSN This server can provide delivery status notification. For example, the remote user can receive a receipt notification when the message is read. This extension is defined in RFC 1891 ("SMTP Service Extension for Delivery Status Notifications").

ETRN This server allows remote sites to retrieve messages from the server's queue that are bound for the remote site . ETRN is an updated version of the TURN command that fixes the security problems that existed in TURN. This extension is defined in RFC 1985 ("SMTP Service Extension for Remote Message Queueing Starting").