you might launch Mozilla Firefox to test the response of a computer that runs a Web server program, or you might use an e-mail client program to test a mail server computer.

One particularly helpful test program is **telnet**. This program is a simple text-mode remote login program, and when it’s used for its original intended purpose, it enables you to connect to a remote system and run text-mode programs on it. The **Telnet** protocol, however, is unencrypted and so is no longer recommended for remote logins; instead, you should use Secure Shell (SSH) for this task. The **telnet** program remains useful as a network diagnostic tool, however, because you can pass a port number after the system name to connect to any TCP port on the target system:

```
```
$ telnet mail.example.com 25
Trying 192.168.1.2...
Connected to mail.
Escape character is '^]'.
220 mail.example.com ESMTP Postfix (Ubuntu)
```
```

This example shows a connection to port 25 on **mail.example.com**. This port is ordinarily used by the Simple Mail Transfer Protocol (SMTP), and the example shows an SMTP server (Postfix) responding on this port. In other words, the target system’s mail server program is functioning, at least in a minimal way. If you can’t send e-mail, therefore, the problem doesn’t lie in basic connectivity.

If you know enough about the protocols involved, you can use **telnet** to simulate a data exchange session. For instance, the preceding exchange might be continued:

```
```
mail from:<ben@example.com>
250 2.1.0 Ok
rcpt to:<george@example.com>
250 2.1.5 Ok
data
354 End data with <CR><LF>.<CR><LF>
This is a message!
.
250 2.0.0 Ok: queued as 8B00C6735
quit
```
```

The **mail from**, **rcpt to**, **data**, and **quit** commands are all legal ones in SMTP, while the text of the message (*This is a message!*) is the body of an e-mail message. This example shows a message being accepted for delivery by the server, but if an error occurred, the server would present an error message that might be diagnostic—for instance, the server might complain that it’s not configured to forward e-mail between sites.

Of course, to do more than check for a basic connection, you must know enough about the protocol to issue valid commands. This knowledge is fairly advanced, and you won’t be expected to do such things on the Linux+ exam!