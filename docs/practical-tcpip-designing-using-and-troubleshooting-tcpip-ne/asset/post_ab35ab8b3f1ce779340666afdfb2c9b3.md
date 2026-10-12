
## Summary

- a typical e-mail client on a LAN PC uses SMTP to send e-mail messages and POP3 to receive them. SMTP and POP both run over TCP as transport
- using SMTP, your client sends the message to your e-mail server (or your ISPs) for delivery to the ultimate destination
- your server determines the IP address of the server for the final destination by looking up MX (mail exchange) records in the DNS
- a site (domain) can have multiple MX records for resilience and load sharing
- an SMTP session consists of an exchange of plain-text lines over a TCP connection, and consequently ...
- you can use **telnet** as a test and debugging tool to sending and receiving messages "manually"
- there are two parts to an SMTP session:
  - the envelope. This is the level at which SMTP servers converse and the destination address in the envelope determines which machine will receive the message
  - the body. This contains the **From**, **To**, **Subject**, etc. headers that you see when you read the message in your e-mail client
- a POP session also consists of an exchange of plain-text lines over a TCP connection between your e-mail client and a POP server
- when troubleshooting, **tcpdump** can show you the DNS queries and other traffic that sending/receiving a message involves
- using **telnet** as a test client bypasses a lot of the complexity and possible configuration errors in a normal e-mail client
- open relay e-mail servers are often a source of spam.

## What’s next?

Chapter 12 looks at MIME, which allows you to send arbitrary data conveniently over e-mail using attachments. We also look briefly at IMAP and other mail systems.

## Notes and further reading

The scenarios we described are what is typical nowadays. In the past, at sites with networks of UNIX machines, it was common for every desktop machine to to:

- send its own messages using SMTP
- receive messages from other internal workstations, and from the outside world, using SMTP.

This involved running a full mail server, and often a DNS server, on every machine on the network, and each one had to have its own MX record(s) listed in the public DNS. It was dreadful: SMTP traffic had to be allowed in from the Internet to each machine, potentially causing security holes, you had to maintain dozens or hundreds of copies of the mail server, and if there was a problem you had to debug the e-mail and network configuration on the specific machine. Running a centralized mail server or two on high-performance machines with good redundancy (e.g. RAIDed disks), a good backup system, and plenty of disk space for mail messages in transit is very much easier and more reliable.

(You still can have separate MX records for an individual host if you want, e.g. for `pc29.sales.example.com`, but we haven't dealt with that because almost nobody uses that type of configuration nowadays. We have described today's common practice for MX configurations.)

MX records were introduced in:

- RFC-973 **January 1986** _Domain System Changes and Observations_

MX record priorities let you modify your mail system without any downtime. See Web Appendix 8.

In Module 11.4 we said that if you have an intermittent connection to the Internet, including your own (intermittently available) mail servers in your MX list causes wasted effort on the part of servers trying to send to you. There is now an Internet Draft RFC saying that you should not do this:

- [http://www.ietf.org/internet-drafts/draft-ietf-dnsop-dontpublish-unreachable-03.txt](http://www.ietf.org/internet-drafts/draft-ietf-dnsop-dontpublish-unreachable-03.txt) _IP Addresses that should never appear in the public DNS_

# Terminology

The SMTP server is sometimes called a _Message Transfer Agent_ (MTA) and the client a _Message User Agent_ (MUA) to emphasize that they perform very different functions. An MTA doesn't include POP functionality. The POP server is sometimes called a _mailbox server_ or _message store_. When discussing how the components interact on large e-mail networks, these terms let you specify clearly which aspect of a “mail server” you are referring to. For example, the **sender** and **Exim** mail servers are MTAs; if you're using one of these you need another server application to provide POP services. (Instead of using POP to retrieve messages, some sites use IMAP, which is a newer and more flexible protocol; see Module 12.5.)

For a glossary, see the Internet Mail Consortium site:

- [http://www.imc.org/terms.html](http://www.imc.org/terms.html) _Terms Used In Internet Mail_

# SMTP and ESMTP

SMTP and the message format were defined in:

- RFC-821 **August 1982** _Simple Mail Transfer Protocol_
- RFC-822 **August 1982** _Standard for the Format of ARPA Internet Text Messages_

These have been superseded by:

- RFC-2821 **April 2001** _Simple Mail Transfer Protocol_
- RFC-2822 **April 2001** _Internet Message Format_

"ESMTP" is "extended SMTP," which defines the EHLO command – see:

- RFC-1869 November 1995 SMTP Service Extensions

RFC-821 defined the TURN command. The ETRN command was introduced in:

- RFC-1985 August 1996 SMTP Service Extension for Remote Message Queue Starting

In Module 11.6 we explained the `MAIL FROM:` command. When a mail server sends a "bounce message" to say it cannot deliver a message, it uses `MAIL FROM:<>` i.e. a null sending domain name. Occasionally you will find mail servers that incorrectly won't accept such a message, because of bugs or mis-configuration.

## POP3 and mail clients

The original and current standards for POP3 are, respectively:

- RFC-1081 November 1988 Post Office Protocol – Version 3
- RFC-1939 May 1996 Post Office Protocol – Version 3

Linux and most if not all UNIX systems have a command-line e-mail client (or several) that you can use in scripts. These are useful for sending alerts to the system administrator. We use it within a security system that detects whether any files have been changed without authorization (and also in a script which retrieves the lottery results from a Web page and e-mails them to us). These clients can also read mail messages but they don't use POP: they just extract the messages directly from the message store on this machine.

## Spam and security

The **sendmail** mail server has historically been a great source of security problems. (Lots of other mail servers have security holes too, probably because they are such large and complex programs.) Module 24.6 and Chapter 25 explain how you can protect your mail server by hiding it behind your firewall, and interposing a small designed-for-security proxy mail server to send/receive messages on the Internet. Chapter 25 also explains how you can counter e-mail virus threats and block spam automatically.

One dial-up ISP (let's call them *some-isp.com*) in the UK does strange things with mail traffic. When you try to connect to any mail server, e.g. with "`telnet mailserver.example.com smtp`," the ISP hijacks the connection and connects you to their own mail server, at *some-isp.com*, instead. We assume this is so they can control people sending spam, but it can be confusing when you are troubleshooting if you haven't seen it before.

For pointers on how to combat spam, see:

- http://spam.abuse.net
- http://mail-abuse.org MAPS, the Mail Abuse Prevention System

## Appendices

- Web Appendix 8: future-proofing your DNS
- Web Appendix 37: configuring e-mail settings on different Netscape versions

# 12 E-mail – MIME, IMAP; other mail systems

- 12.1 Sending and receiving non-text messages
- 12.2 E-mail attachments and MIME
- 12.3 MIME headers (1) – Content-Type
- 12.4 MIME headers (2) – Content-Transfer-Encoding, etc.
- 12.5 IMAP – the Internet Message Access Protocol
- 12.6 Other mail systems
- Summary

## Introduction

This chapter explains MIME – the mechanism Internet e-mail uses to include files and arbitrary content in e-mail messages as “attachments.” We also look briefly at the IMAP system, which can give you distributed, network-wide access to your e-mail messages stored centrally, and at other e-mail systems.

![](img/a2132b646d336d5f9a21102d6320e537_346_0.png)
