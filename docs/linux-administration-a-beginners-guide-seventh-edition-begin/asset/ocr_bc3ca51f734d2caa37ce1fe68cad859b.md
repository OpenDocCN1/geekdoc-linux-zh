# CHAPTER 19 Simple Mail Transfer Protocol (SMTP) 50

SMTP requires only that a host be able to send straight ASCII text to another host. Typically, this is done by contacting the SMTP port (port 25) on a mail server. You can do this using the Telnet program. For example,

```
[root@server ~]# telnet mailserver 25
```

Here, the mailserver is the recipient's mail server. The 25 that follows mailserver tells Telnet that you communicate with the server's port 25 rather than the normal Telnet port 23. (Port 23 is used for remote logins, and port 25 is for the SMTP server.)

The mail server will respond with a greeting message such as this:

```
220 mail SMTP Postfix
```

You are now communicating directly with the SMTP server. Although there are many SMTP commands, four are worth noting:

+   - HELO
- MAIL FROM:
- RCPT TO:
- DATA

The HELO command is used when a client introduces itself to the server. The parameter to HELO is the hostname that is originating the connection. Of course, most mail servers take this information with a grain of salt and double-check themselves. Here's an example:

```
HELO example.org
```

If you aren't coming from the example.org domain, many mail servers will respond by telling you they know your real IP address, but they may may not stop the connection from continuing.
The MAIL FROM command requires the sender's e-mail address as its argument. This tells the mail server the e-mail's origin. Here's an example:

```
MAIL FROM: puffer-up@example.org
```

This means the message is from puffer-up@example.org.
The RCPT TO: command requires the receiver's e-mail address as an argument. Here's an example:

```
RCPT TO: manager@example.org
```

This means the message is destined to manager@example.org.
Now the server knows who the sender and recipient are, it needs to know what message to send. This is done by using the DATA. Once it's issued, the server will expect the entire message, with relevant header information, followed by one