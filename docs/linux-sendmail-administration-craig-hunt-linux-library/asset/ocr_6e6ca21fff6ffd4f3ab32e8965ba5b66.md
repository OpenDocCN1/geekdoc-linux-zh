SAML sends the mail message to a terminal and delivers it to a mailbox.

TURN turns the connection around so that the mail source is now the destination and the mail destination is now the source.

RFC 821 was written back in 1982 when central computers with user terminals were in widespread use. SEND, SMTP, and SAML assumed that there would be times when the source world would want to display a message on the recipient's terminal in a manner similar to the Linux write command. In reality, SMTP turned into a pure mail system that sends e-mail to a mailbox and does not send messages to a terminal.

The TURN command reverses the role between the sending and receiving mail systems. In a normal connection, the system that initiates the connection is the system that has to send. With the TURN command, the system that initiates the connection does not necessarily have to send. The initiating system is hoping to receive mail. It creates the connection to find out if the remote system has mail to send to it. In a global Internet it is, of course, impossible to know what systems have mail to send you. So the TURN command was really intended as a way to move mail from a mailbox to a server that has limited network service. Mail protocols like POP and IMAP, covered in later chapter, reduced the demand for TURN, as the wide deployment of full-time Internet access. Security concerns about the TURN command killed it.

For these reasons, SEND, SMTP, SAML, and TURN were never widely implemented and can safely ignore when you see them in RFC 821. The 10 commands listed in Table 1.1 are the basic SMTP commands implemented on most systems.

As you'll see in the following sections, SMTP is such a simple protocol that it is possible to watch the protocol in action and understand what is happening when you do. This is both a useful way to learn how the protocol functions and to detect when it is malfunctioning.

# Using SMTP through telnet

The SMTP protocol is simple enough for you to “do it yourself.” Use telnet to connect to port 25 on a destination host and manually type in a few SMTP commands. The example in Listing 1.1 was created on a Red Hat system running Sendmail 8.11.0.

# Listing 1.1 Telnetting to the SMTP Port

```
[craig]$ telnet wen.foobirds.org 25
Trying 127.0.0.1...
Connected to wen.foobirds.org.
Escape character is '^'.
220 wen.foobirds.org SMTP Sendmail 8.11.0/8.11.0; Mon, 23 Oct 2000
11:23:14 -0400
```