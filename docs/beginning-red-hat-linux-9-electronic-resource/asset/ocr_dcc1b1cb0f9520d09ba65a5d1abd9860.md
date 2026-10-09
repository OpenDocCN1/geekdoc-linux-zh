having your own mail server allow you to work on your e-mail without ever having to connect manually to the Internet. You can configure our email server to send and receive mail in batches, by connecting to Internet at specified times.

+   □ You can customize a mail server’s security and monitoring rules, so that it alerts you if it receives a message that contains certain blocked words or if it detects unusual activity.

Hosting your own mail server comes with its burdens, too. There’s the increased cost of support and maintenance, and the additional chance of being compromised (you’re protected from this if you use an ISP’s mail server). It’s also more important to ensure that you keep your antivirus software up to date, and that it scans each e-mail. And there is a risk that your mail server will become an open relay SMTP server (this is where another user uses your mail server as a gateway for sending mail).

So, there’s much to consider, and debate of these issues is outside the scope of this book. However, if you do decide to host your own mail server, then you won’t be surprised to learn that the Red Hat Linux 9 operating system comes with a default mail server. It’s called Sendmail, and we’ll examine it briefly here.

# ## What Is a Mail Server?

A mail server is a collection of applications that provide the functionality to manage the tasks of sending and receiving of e-mail, and delivering e-mail to user’s mailboxes. A mail server uses a number of different protocols to transfer e-mail from one system to other. Here’s a brief description of these protocols:

+   □ The Internet Message Access Protocol (IMAP) is a protocol used by an e-mail client application to access the remote e-mail mailbox. The main advantage of IMAP is that users can manage the e-mail messages on remote mailboxes instead of downloading the messages on to local machine. For more information about IMAP, take a look at http://www.imap.org/.

+   □ The Post Office Protocol (POP) is used by e-mail clients to download e-mail messages from a remote server and save it on their local machine. For more information about POP, please refer to RFC 1939 at http://www.rfc-editor.org/in-notes/rfc1939.txt.

+   □ The Simple Mail Transfer Protocol (SMTP) is used to send e-mails (this is in contrast with IMAP and POP, which are used to receive e-mails). Each e-mail message is transferred between remote e-mail servers using SMTP. Red Hat Linux 9 uses sendmail as its default SMTP software.

# ## E-mail Application Types

E-mail applications fall into the following three class:

+   □ Mail User Agents (MUAs). An MUA is an e-mail client – a program that is used to retrieve and manage e-mail messages via POP or IMAP protocols. Examples of MUAs