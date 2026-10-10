things that many other MTAs cannot. However, if ease of use or speed is a concern to you, you might want to consider replacing Sendmail with Postfix, Exim, or Qmail. Because Sendmail is the default MTA included with Fedora, it is covered in more detail over the following sections.

# The Mail Delivery Agent

SMTP is a server-to-server protocol that was designed to deliver mail to systems that are always connected to the Internet. Dialup systems connect only at the user’s command; they connect for specific operations, and are frequently disconnected. To accommodate this difference, many mail systems also include a mail delivery agent, or MDA. The MDA transfers mail to systems without permanent Internet connections. An MDA is similar to an MTA (see the following note), but does not handle deliveries between systems and does not provide an interface to the user.

> **NOTE**
> 
> Procmail and Spamassassin are examples of MTAs; both provide filtering services to the MTA while they store messages locally and then make them available to the MUA or email client for reading by the user.

The MDA uses the POP3 or IMAP protocols for this process. In a manner similar to a post office box at the post office, POP3 and IMAP implement a “store and forward” process that alleviates the need to maintain a local mail server if all you want to do is read your mail. For example, dialup Internet users can intermittently connect to their ISPs’ mail servers to retrieve mail by using Fetchmail—the MDA provided by Fedora (see the section “Using Fetchmail to Retrieve Mail,” later in this chapter).

# The Mail User Agent

The mail user agent, or MUA, is another necessary part of the email system. The MUA is a mail client, or mail reader, that enables the user to read and compose email and provides the user interface. (It is the email application itself that most users are familiar with as “email.”) Some popular UNIX command-line MUAs are elm, pine, and mutt. Fedora also provides modern GUI MUAs: Evolution, Thunderbird, Mozilla Mail, Balsa, Sylpheed, and KMail. For comparison, common non-UNIX MUAs are Microsoft Outlook, Outlook Express, Pegasus, and Eudora.

The Microsoft Windows and Macintosh MUAs often include some MTA functionality; UNIX does not. For example, Microsoft Outlook can connect to your Internet provider’s mail server to send messages. On the other hand, UNIX MUAs generally rely on an external MTA such as Sendmail. This might seem like a needlessly complicated way to do things, and it is if used to connect a single user to her ISP. For any other situation, however, using an external MTA provides you much greater flexibility because you can use any number of external programs to handle and process your email functions and customize the service. Having the process handled by different applications gives you