Transfer Protocol (SMTP). The TCP/IP protocols provide the basic network services for the Internet. Higher-level protocols such as the File Transfer Protocol (FTP) and SMTP are built on top of TCP/IP. The advantage of such layering is that programs that implement the SMTP or FTP protocols don't have to know anything about transporting packets on the network and making connections to other hosts. They can use the services provided by TCP/IP for that job.

SMTP defines how programs exchange email on the Internet. It doesn't matter whether the program exchanging the email is sendmail running on a Sun workstation or an SMTP client written for an Apple Macintosh. As long as both programs implement the SMTP protocol correctly, they can exchange mail.

The following example of the SMTP protocol in action might help demystify it a little. The user betty at gonzo.gov is sending mail to joe at whizzer.com:

```
$ /usr/sbin/sendmail -v joe@whizzer.com < letter
joe@whizzer.com... Connecting to whizzer.com via tcp...
Trying 123.45.67.1... connected.
220-whizzer.com SMTP ready at Mon, 6 Jun 1997 18:56:22 -0500
220  ESMTP spoken here

>>> HELLO gonzo.gov
250 whizzer.com Hello gonzo.gov [123.45.67.2], pleased to meet you

>>>  MAIL From:<betty@gonzo.gov>
250 <betty@gonzo.gov>... Sender ok

>>>  RCPT To:<joe@whizzer.com>
250 <joe@whizzer.com>... Recipient ok

>>> DATA
354 Enter mail, end with "." on a line by itself
>>>
250 SA00680 Message accepted for delivery

>>> QUIT
221 whizzer.com closing connection
joe@whizzer.com... Sent
```

The first line shows one way to invoke sendmail directly rather than letting your favorite Mail User Agent (MUA), such as Elm, Pine, or Mutt, do it for you. The -v option tells sendmail to be verbose and shows you the SMTP dialog. The other lines show an SMTP client and server carrying on a conversation. Lines prefixed with >>> indicate the client (or sender) on gonzo.gov, and the lines that immediately follow are the replies of the server (or receiver) on whizzer.com. The first line beginning with 220 is the SMTP server announcing itself after the initial connection, giving its hostname and the date and time, and the second line informs the client that this server understands the Extended SMTP protocol (ESMTP) in case the client wants to use it. Numbers such as 220 are reply codes that the SMTP client uses to communicate with the SMTP server. The text following the reply codes is only for human consumption.