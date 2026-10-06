```
250-SIZE 1024000
250-VRFY
250-ETRN
250 8BITIME
mail from: justin@bible
250 OK
rcpt to: justin@palmcoder.net
250 Ok
data
354 End data with <CR><LF>,<CR><LF>
This is a test mail that I am sending you.
Justin

250 Ok: queued as 6D5CF18490
```

We have used the SMTP protocol to specify that we are sending a mail to the user justin@palmcoder.net from the user justin@bible from the machine localhost (ehlo localhost). This is a standard SMTP transaction that can be used to quickly send an SMTP server's ability to send mail to a specific user.

We discuss mail servers and a further example of using Telnet to test a service in Chapter 17.

The command line, telnet localhost smtp, is the same command used previously with the addition of the port specification (smtp). The port you connect to can either be in text form (as we used) or in numerical format. The number for the SMTP port is 25.

From now on in the book, we will refer to TCP/IP ports and more. A TCP/IP port can be thought of as a virtual port that serves a specific purpose. Each port has a unique number and a number of well-known numbers have been reserved for specific purposes. For example, port 80 is HTTP, port 25 is SMTP, and port 21 is FTP. View the file /etc/services for more information on what well-known ports are.

If security is a concern for your organization, Telnet should not be used to transmit sensitive information. As all information is plain text, it is just not safe.

# Using SSH

SSH can be thought of as a secure extension using Telnet. It provides virtual terminal services that are encrypted to the user; this includes encrypting the password that the user sends to the server. However, SSH, is actually a technology that provide not only virtual terminal services, but also file transfer and