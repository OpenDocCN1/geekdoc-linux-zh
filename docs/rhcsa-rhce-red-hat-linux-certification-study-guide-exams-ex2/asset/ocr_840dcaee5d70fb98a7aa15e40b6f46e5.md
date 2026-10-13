TABLE 13-1
Mail Server Components

| Abbreviation | Meaning | Examples |
|---|---|---|
| MTA | Mail transfer agent | Postfix, sendmail, Dovecot |
| MUA | Mail user agent | mutt, Evolution, mail, Thunderbird |
| MDA | Mail delivery agent | procmail |
| MSA | Mail submission agent | Postfix, sendmail |

E-mail systems are heavily dependent on name resolution. While you could handle name resolution through /etc/hosts on a small network, any mail system that requires Internet access needs access to a fully functional DNS server. For spam protection and more, it's important to make sure that the system that intends to send an e-mail is actually transmitting with the assigned IP address.

But that is only one component of how e-mail works, from transmission to delivery. E-mail messages start with a mail user agent (MUA), a client system for sending and receiving e-mail such as mutt, Evolution, or Thunderbird. With the help of a Mail Submission Agent (MSA), such mail is normally sent to an MTA such as Postfix or sendmail. A Mail Delivery Agent (MDA) such as Procmail works locally to transfer e-mail from a server to an inbox folder. Procmail can also be used to filter e-mail. Red Hat also supports additional MTA services such as Dovecot to enable POP3 and/or IMAP (or the secure cousins, POP3s and IMAPs) to receive e-mail.

SMTP, the Simple Mail Transfer Protocol, has become one of the most important service protocols of the modern era. Much of the Internet-connected world lives and dies by e-mail and relies on SMTP to deliver it. Like POP3 and IMAP, SMTP is a protocol, a set of rules for transferring data used by various mail transfer agents.

# Relevant Mail Server Packages

The packages associated with sendmail and Postfix are both part of the “E-mail server” package group. Key packages are listed in Table 13-2. You can install them with the rpm or yum command. Just remember that you do not need to install everything in this table.

When installed, the default E-mail server package group includes packages for the Postfix and Dovecot servers, along with the Spamassassin filter. Since you may not need all of these packages, it may be faster to install just Postfix or sendmail with the rpm or yum command, especially if you’re configuring your Linux computer from the text console. It takes time to start the GUI.