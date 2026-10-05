# WORKING WITH exim4

exim4 receives email, from both local and nonlocal systems, it creates in the /var/spool/exim4/input directory two files that hold the message while exim4 processes it. To identify a particular message, exim4 generates a 16-character ID and uses string in filenames pertaining to the email. The exim4 daemon stores the body of the message in a file named by the message ID followed by -D (data). It stores the headers and envelope information in a file named by the message ID followed by -H (header).

Frozen messages

exim4 cannot deliver a message, it marks the message as frozen and makes no attempt to deliver it. If it has successfully delivered an email, exim4 removes all files pertaining to /var/spool/exim4/input.

Mail addressed to the local system

By default, exim4 delivers email addressed to the local system to users' files in the mail spool directory, /var/mail, in mbox format. In this directory, each user has a mail file named with the user's name. Mail remains in these until it is collected, typically by an MUA. An MUA collects the mail from the mail spool, the MUA stores the mail as directed by the user, or in the user's home directory.

Mail addressed to nonlocal systems

The scheme exim4 uses to process email addressed to a nonlocal system depends on how it is configured: It can send the email to a smarth, or send the email to the system pointed to by the DNS MX record of the domain it is addressed to, or it can refuse to send the email.

mbox versus maildir

The mbox format holds all messages for a user in a single file. To prevent corruption, a process must lock this file while it is adding messages to or deleting messages from messages; the MUA cannot delete a message at the same time the MTA is adding messages. A competing format, maildir, holds each message in a separate file. This format does not use locks, allowing an MUA to delete messages from a user at the same time as mail is delivered to the same user. In addition, the maildir format is better to handle large mailboxes. The downside is it uses a protocol such as IMAP to check messages. The exim4 daemon supports both mbox and maildir formats (see de_localdelivery on page 725). Qmail (page 715), an alternative to sendmail and exim4, uses maildir mailboxes.

# MAIL LOGS

By default, exim4 sends normal log messages to /var/exim4/mainlog, with other messages going to other files in the same directory. The lines in mainlog describe an email message sent directly to a remote system's SMTP server. The exim4 daemon writes one line each time it receives a message and one line each it attempts to deliver a message. The Completed line indicates that exim4 has completed its part in delivering the message. Each line starts with the date and time of the entry followed by the message ID.