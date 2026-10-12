
## 11.6 Components of an SMTP session (1) – the envelope

SMTP was described in the now obsolete RFC-821, which has been superseded by the very recent RFC-2821. These RFCs give full details of the SMTP commands, but here we'll cover just the few we need to send a simple message. We'll use the message we sent in the previous module as an example, so we duplicate it here:

```
alice% telnet dave smtp
      Trying 192.0.2.5...
      Connected to dave.
      Escape character is '^}'.
      220 dave ESMTP Sendmail 8.7.3/8.7.3/dave; Fri, 6 Jul 2001 13:55:36
EHLO mydom.com
      250-dave Hello alice [192.0.2.17], pleased to meet you
MAIL FROM:<vanderb@mydom.com>
      250 <vanderb@mydom.com>... Sender ok
RCPT TO:<taybay@example.com>
      250 Recipient ok
DATA
      354 Enter mail, end with "." on a line by itself
from: <vanderb@mydom.com>
to: <taybay@example.com>
subject: cat food

Are there any tins of Yum Yum in the fridge?

      Bye, v.
      250 NAA21635 Message accepted for delivery
QUIT
      221 dave closing connection
      Connection closed by foreign host.
alice%
```

**telnet dave smtp** is not an SMTP command. From Alice we **telnet** to Dave, to connect to the SMTP server which we hope is listening on the well-known **smtp** port (which our **services** file maps to the numeric port number 25). An equivalent command is:

```
telnet dave 25
```

The server replies with its greeting, which is prefixed with the code **220**. All SMTP response codes consist of three digits, divided into four classes:

- 2xx: OK – all is well
- 3xx: server is asking you to send data
- 4xx: temporary error. If the sender tries again it might work correctly next time
- 5xx: permanent error. If the sender tries again, the same error will occur.

`EHLO mydom.com` *incorrect but it works*  
`EHLO alice.mydom.com` *correct*

(EHLO = "Extended Hello") This identifies the client to the server. The argument ought to be either the full name of the client machine ("**alice.mydom.com**") or the IP address in square brackets (“[192.0.2.17]”) but most servers don't insist on this and usually extract the client's IP address from the TCP packets as happened here. Alice didn't give her proper machine name but Dave saw from the TCP data that her IP address was 192.0.2.17 and looked this up in the DNS. The server acknowledges the client with a line beginning with code 250.

EHLO is an extended version of the HELLO (“hello”) command from the early RFC-821 standard for SMTP. EHLO was introduced in the more recent RFC-2821, which allows a range of extensions to SMTP to be supported. However, for checking out the network and the basic operation of the mail service, the old HELLO command is adequate, even though almost obsolete.

```
MAIL FROM:<vanderb@mydom.com>
```

The client gives the e-mail address of the sender, and the server acknowledges it, prefixed with code 250. This starts the mail sending transaction proper. Note that angle brackets are used here but not in EHLO.

```
RCPT TO:<taybay@example.com>
```

The client gives the e-mail address of the recipient (RCPT stands for recipient) and if the server can send (or accept) the message for that recipient, it acknowledges positively with a 250 line.

You can enter multiple RCPT TO lines, with one recipient named on each, to send to many people at the same time. Where there's more than one recipient at the same site (same domain) this is very efficient: only one copy of the message is transmitted to the recipient server, and it then delivers multiple copies of the message, one to each recipient. However, some may be accepted and some rejected.

```
DATA
```

This introduces the start of the “mail data”, i.e. the content of the message to be sent. The server acknowledges with a 354 (“intermediate” reply, i.e. “I expect more to follow. But you're OK so far”).

At this point the client has told the server who the client is, and the address(es) the server is to send the message to. In SMTP terminology all this information forms the *envelope*, by analogy with regular snail-mail. The envelope information is used for routing the message through the mail system, and determines where it will be delivered. But just like a paper letter, the address on the inside – on the letter itself rather than the envelope – can be different. (This is often the case when you are sending to a third party a copy of something you received.) What follows after the DATA command is the equivalent of the letter itself, “inside the envelope.” The server doesn't give any further acknowledgments until you've finished entering the body of the “letter” or mail message. That's what we cover in the next module.

## 11.7 Components of an SMTP session (2) – the message body

We're using the same example message as in Modules 11.3 and 11.4, so we duplicate it here:

```
alice% telnet dave smtp
       Trying 192.0.2.5...
       Connected to dave.
       Escape character is `^]'.
       220 dave ESMTP Sendmail 8.7.3/8.7.3/dave; Fri, 6 Jul 2001 13:55:36
EHLO mydom.com
       250-dave Hello alice [192.0.2.17], pleased to meet you
MAIL FROM:<vanderb@mydom.com>
       250 <vanderb@mydom.com>... Sender ok
RCPT TO:<taybay@example.com>
       250 Recipient ok
DATA
       354 Enter mail, end with "." on a line by itself
from: <vanderb@mydom.com>
to: <taybay@example.com>
subject: cat food

Are there any tins of Yum Yum in the fridge?

        Bye, v.

       250 NAA21635 Message accepted for delivery
QUIT
       221 dave closing connection
       Connection closed by foreign host.
alice%
```

`from: <vanderb@mydom.com>`

In this and the next two lines the client specifies the *header lines* to appear in the actual mail message the recipient will receive. The **from** header identifies the sender. As this is “inside the envelope” and not used for mail routing, it doesn't have to be just an e-mail address, so lines like:

```text
“Fred Blogs” <fred@blogs.com>
fred@blogs.com (Fred Blogs)
```

make sense. (The format is described in RFC-2822.)

`to: <taybay@example.com>`

This header specifies the recipient(s) that are *to be shown in the message headers*. They are normally the same as the **RCPT TO** recipients, but could be different for several good reasons and some bad ones. A good reason is the message is delivered (**RCPT TO**) to several people, A, B, C, and D, but the **to** header lists only A and another header, **cc**, includes B and C. What about D, you ask? D is in fact a **bcc** (blind carbon copy) recipient: they get a copy of the message, but there's nothing in the message itself to indicate this. We'll look at bad reasons (e.g. junk mail) in Module 11.14.

`subject: cat food`

This is the subject header line. The blank line indicates that we’ve entered all the headers we want to enter. Anything else that follows is the body of the message.

```
Are there any tins of Yum Yum in the fridge?
Bye, v.
```

These three lines are the body of this profound message. A period at the beginning of a line and followed by nothing else indicates that we’ve finished entering body lines. The server replies with a 250 code line, saying the message has been accepted. Depending on your server, it may deliver it immediately.

At this point we could start another whole transaction, repeating the commands in the previous module to send another message. (You can omit the initial EHLO though, if you want.) We’d have to enter all the details again even if sending to the same recipients because the first message is completely finished with.

`QUIT`

We want to exit. The server acknowledges with a code 221 termination message, and the TCP connection is terminated.

These commands insert basic mail headers in the message – to:, from:, and subject:. Other headers are inserted into the message automatically:

- Real e-mail clients include headers giving the date and information about themselves, e.g. product name and version information
- Any mail servers that handle the message on its way to its destination should insert a “Received:” header. For example, the smart host at your ISP, the recipient’s own mail server/ISP, and any backup relay (e.g. at the recipient’s ISP) that might have been involved.

A real mail client obviously includes a lot more functionality than we’ve shown, to make it easy to send and receive messages, and must store and retrieve messages in a local file, etc. But in principle, those extras are just conveniences for the user – the fundamental operation of sending mail happens just as you’ve done it by hand.

If you’re a programmer or do crosswords, you’ve probably asked yourself a couple of interesting questions. First, if the mail message we’re sending contains a line consisting of a single period, will that cause our e-mail program to go wrong? (It obviously doesn’t, but why not? See the Notes.) Second, if I want to send a binary file such as a spreadsheet or executable program, or a graphics file, how can I do it, because these could easily contain runs of characters that appear to be SMTP commands? Binary files do cause problems, for the reason above and because RFC-2821 says the maximum length of a text line is 1000 characters. The solution to these problems is MIME (Multipurpose Internet Mail Extension) (Module 12.1).

We examine the mail headers in more detail in the next module.
