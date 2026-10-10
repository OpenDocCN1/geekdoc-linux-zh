# Email Basics

Several protocols exist to manage email. The most common of these is SMTP, which is designed as a push mail protocol, meaning that the sending system initiates the transfer. This design is good for sending data, so SMTP is used through most of a mail delivery system. The final stage, though, often employs a pull mail protocol, such as POP or IMAP. With these protocols, the receiving system initiates the transfer. This is useful when the receiving system is an end user's workstation, which might not be powered on at all times or able to receive incoming connections.

SMTP was designed to enable a message to be relayed through an arbitrary number of computers. For instance, an end user might compose a message on a workstation (say, `client.example.com`), which is sent to the local SMTP server (`mail.example.com`). This server looks up a recipient system using DNS and sends the message to that system (for instance, `mail.pangaia.edu`). This system enables the message might be read, either directly or via a POP or IMAP server. In the latter case, the final recipient system would be a fourth computer (such as `wegener.pangaia.edu`). This arrangement is illustrated in Figure 6.3. Bear in mind that the number of links in this chain is variable and depends on how each system is configured. In the simplest case, local email stays on just one system. In theory, an arbitrarily large number of computers can be involved in an email exchange, although in practice it's rare to see email pass through more than half a dozen systems.

![](bbox=[0.14, 0.48, 0.85, 0.62])

At each step in a relay chain, mail is altered. Most importantly, each server adds a *header* to the email, which is a line that provides information about the message. In particular, mail servers add `Received:` headers to document the path the mail has taken. In theory, this enables you to trace the email back to its source. Unfortunately, spammers and other email abusers often forge email headers, which greatly complicates such analysis.

Because an SMTP server can function as both a server (receiving mail from other systems) and a client (sending mail to other systems), you must deal with both sides of the configuration equation. Sometimes a system will never function in one role or the other, which can simplify matters—but you must then be careful not to accidentally configure the system incorrectly. In particular, open relay configurations, in which a mail server relays mail from anybody, should be avoided.

# Sendmail Configuration Files

Sendmail uses a number of configuration files, each with its own unique purpose:

`sendmail.cf` This file is the official primary sendmail configuration file. It includes information relating to relaying options, the server's hostname, and so on. Unfortunately, its syntax