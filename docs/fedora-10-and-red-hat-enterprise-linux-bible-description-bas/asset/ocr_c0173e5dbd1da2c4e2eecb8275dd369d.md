# Part IV: Fedora RHEL Network and Server Setup

# Introducing SMTP and sendmail

With multimedia attachments and HTML encoding prevalent in e-mails today, the technology behind message transfer hasn't changed significantly since the early 1980s. The framework for the Simple Mail Transfer Protocol (SMTP) was initially described in RFC 821 in 1982. The protocol itself was extended in 1993 (RFC 1425), yielding the Extended Simple Mail Transfer Protocol (ESMTP), which provides more commands and new delivery modes.

The three parts to transfer message are the Mail Transfer Agent (MTA), the Mail Delivery Agent (MDA), and the Mail User Agent (MUA). The MTA, commonly referred to as the server (of which postfix are examples), actually handles distributing outgoing mail and listening for incoming mail from the Internet. The MTA accepts messages from the MTA and copies the message into a user's mailbox. Fedora procmail as the default MDA, as specified in the sendmail configuration file (sendmail.cf). Other MDAs (also referred to as Local Delivery Agents or LDAs) include Maildrop and Postfix.

End users, for whom the mail is ultimately intended, use MUAs to get mail from the server and read it from their desktops. Most MUAs support Post Office Mail Access Protocol (IMAP4) for getting mail from the server so it can be read and managed from the user's desktop computer. When possible, you should use the more Secure POP and IMAP protocols (pops and imaps, respectively).

> CROSS-REFERENCE: See Chapter 9 for details on Mail User Agents available with Fedora.

This chapter focuses on the sendmail MTA, the most common server on the Internet. Nearly 70 percent of all e-mail messages on the Internet are delivered by sendmail. With the growing Internet population, billions of e-mail messages are sent and received each day. As an alternative to sendmail, this chapter also includes a short description of postfix.

For getting mail from the server, this chapter describes the dovecot software package, which includes POP and IMAPv4 server. For an alternative, allowing users to read and manage e-mail from a web browser, this chapter describes how to configure SquirrelMail.

There have been three releases of sendmail. The original (sendmail version 5) was written in 1983 by Eric Allison, a student at the University of California at Berkeley. He maintained the code until 1987, when Lennart Lövstrand enhanced the program and developed IDA daemon. Eric Allison returned to Berkeley in 1991 and embarked on a major code revision, releasing sendmail V8 in 1993, which incorporated the extensions to IDA sendmail. The current version (8.14) is based on this “version 8” code.

# Installing and Running sendmail

In Fedora, the sendmail distribution consists of three RPM packages: sendmail, sendmail-cf, and sendmail-doc. Only the first package is truly necessary to send and receive mail on your machine. The second package includes configuration macros and other files that can help you