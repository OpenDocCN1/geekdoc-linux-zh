# **Introducing SMTP and sendmail**

Even with multimedia attachments and HTML encoding prevalent in e-mail messages today, the technology behind message transfer hasn’t changed significantly since the early 1980s. The framework for the Simple Mail Transfer Protocol (SMTP) was initially described in RFC 821 in 1982. The protocol itself was extended in 1993 (RFC 1425), yielding the Extended Simple Mail Transfer Protocol (ESMTP), which provides more commands and new delivery modes.

The three parts to message transfer are the Mail Transfer Agent (MTA), the Mail Delivery Agent (MDA), and the Mail User Agent (MUA). The MTA, commonly referred to as the mail server (of which sendmail and postfix are examples), actually handles distributing outgoing mail and listening for incoming mail from the Internet. The MDA accepts messages from the MTA and copies the message into a user’s mailbox. Fedora uses procmail as the default MDA, as specified in the sendmail configuration file (`sendmail.conf`). End users, for whom the mail is ultimately intended, use MUAs to get mail from the server and read it from their desktops. Most MUAs support Post Office Protocol (POP3) and Internet Message Access Protocol (IMAP) features for getting mail from the server so it can be read and managed from the user’s desktop computer.

> **CROSS-REFERENCE:** See Chapter 9 for details on Mail User Agents available with Fedora.

This chapter focuses on the sendmail MTA, the most common mail server on the Internet. Nearly 70 percent of all e-mail messages on the Internet are delivered by sendmail. With the growing Internet population, billions of e-mail messages are sent and received each day. As an alternative to sendmail, this chapter also includes a short description of postfix.

For getting mail from the server, this chapter describes the dovecot software package, which includes POP3 and IMAP server software. As an alternative, for allowing users to read and manage e-mail from a Web browser, this chapter describes how to configure SquirrelMail.

There have been three major releases of sendmail. The original sendmail (sendmail version 5) was written in 1983 by Eric Allman, a student at the University of California at Berkeley. He maintained the code until 1987, when Lennart Lövdström enhanced the program and developed IDA sendmail. Eric Allman returned to Berkeley in 1991 and embarked on a major code revision, releasing sendmail V8 in 1993, which incorporated the extensions from IDA sendmail. The current version (8.12.9) is based on this “version 8” code.

# **Installing and Running sendmail**

In Fedora, the sendmail distribution consists of three RPM packages: sendmail, sendmail-cf, and sendmail-doc. Only the first package is truly necessary to send and receive mail on your machine. The second package includes configuration macros and other files that can help you reconfigure your site’s sendmail installation if the defaults are insufficient. The third package contains documentation files that help to explain some of the details of the current version.