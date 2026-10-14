| RFC Number | Title |
|---|---|
| RFC821 | Simple Mail Transfer Protocol (SMTP) |
| RFC822 | Format of Electronic Mail Messages |
| RFC1869 | SMTP Service Extensions |
| RFC1870 | SMTP Service Extensions for Message Size |
| RFC1939 | Post Office Protocol, Version 3 |

RFC1522) are draft standards. RFC2060, Internet Message Access Protocol Version 4rev1(IMAP4rev1), is a proposed standard.

# POP AND IMAP4REV1

POP and IMAP4rev1 utilize a client/server paradigm. The client contacts the server and is authenticated with a username and password. The server must have access to the maildrop directory, but is not necessarily an MTA. POP is older than IMAP4rev1. The majority of the newer email clients include both protocols.

POP is a very simple and effective protocol. Email is transferred from the server to the local client for manipulation. It is effective for users who utilize a single workstation for email.

IMAP4rev1 was developed for the user who utilizes multiple workstations for email. It incorporates all of the features of POP and adds the ability to access email/mailboxes on a remote server. IMAP4rev1 has the capability to manipulate mailboxes on a local machine or remote server. A mail client with IMAP4rev1 can be configured to download only message header or message body. These configuration options are utilized when accessing email remotely or when bandwidth is limited. The default configuration is to download a complete message when bandwidth is not a problem or the user requires attachments. By providing download options, IMAP4rev1 clients can be written to provide a quick email scanning capability, by allowing the client to only download certain message information. This is advantageous in situations where network connections are slow or client resources are limited (PDAs). There is also the capability to resynchronize an off-line client with the server. Information on IMAP4rev1 can be obtained at http://www.imap.org.