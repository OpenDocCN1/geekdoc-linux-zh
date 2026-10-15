
## 20 Electronic Mail

![](img/14d78e3cecac4581d37024baf1e94cca_790_0.png)

Social networks and SMS messages have started to push email into the “old technology” category as they reduce the world to relationships and microthoughts. Nevertheless, email remains the universal standard for on-line communication. Everyone from grandmas to the stodgiest of corporations now routinely uses email to communicate with family, co-workers, partners, customers, and even the government. It’s a mad, mad, mad, email-enabled world.

Email is easy and just works; if you know someone’s email address, you type a message addressed to them and press Send. Voilà! Seconds later, the message is delivered to their electronic mailbox, whether they’re next door or halfway around the world. From the user’s perspective, nothing could be easier.

The underlying infrastructure that makes electronic mail possible on such a large scale is complex. There are several software packages you can run on your system to transport and manage electronic mail (three of which are discussed later in this chapter), but they all require a certain degree of configuration and management. In addition, it’s important that you understand the underlying concepts and

> 1. Even as Evi is sailing in the middle of the ocean, she is almost always in email contact through her HAM/SSB radio and a “speedy” packet radio connection that approaches 30 baud at good times.

### 20.1 MAIL SYSTEMS

In theory, a mail system consists of several distinct components:

- A “mail user agent” (MUA or UA) that lets users read and compose mail
- A “mail submission agent” (MSA) that accepts outgoing mail from an MUA, grooms it, and submits it to the transport system
- A “mail transport agent” (MTA) that routes messages among machines
- A “delivery agent” (DA) that places messages in a local message store
- An optional “access agent” (AA) that connects the user agent to the message store (e.g., through the IMAP or POP protocol)

Attached to some of these agents are tools for recognizing spam, viruses, and (outbound) internal company secrets. Exhibit A illustrates how the various pieces fit together as a message winds its way from sender to receiver.

![](img/14d78e3cecac4581d37024baf1e94cca_792_0.png)

### User agents

Email users employ a user agent (sometimes called an email client) to read and compose messages. Email messages originally consisted only of text, but a standard known as Multipurpose Internet Mail Extensions (MIME) is now used to encode text formats and attachments (including viruses) into email. It is supported by most user agents. Since MIME generally does not affect the addressing or transport of mail, we do not discuss it further.

**/bin/mail** was the original user agent, and it remains the “good ol’ standby” for reading text email messages at a shell prompt. Since email on the Internet has moved beyond the text era, text-based user agents are no longer practical for most users. But we shouldn’t throw /bin/mail away; it’s still a handy interface for scripts and other programs. (One avid Linux user we know routes nightly emails from cron to calendaring software so that a glance at the calendar tells him the status of all his software builds. By default, cron uses /bin/mail to notify a user when it cannot run a scheduled job.)

One of the elegant features illustrated in Exhibit A is that a user agent doesn’t necessarily need to be running on the same system—or even on the same platform—as the rest of your mail system. Users can reach their email from a Windows laptop or smartphone through access agent protocols like IMAP and POP.

Wikipedia’s “comparison of e-mail clients” page contains a detailed listing of many, many email clients, the operating systems they run on, and the features they support. Popular clients include Thunderbird, Alpine, Zimbra, and of course, Microsoft Outlook. The “comparison of webmail providers” page has similar information for web-based services like Gmail, Hotmail, and Yahoo! Mail.

### Submission agents

MSAs, a late addition to the email pantheon, were invented to offload some of the computational tasks of MTAs. MSAs make it easy for mail hub servers to distinguish incoming from outbound email (when making decisions about allowing relaying, for example) and give user agents a uniform and simple configuration for outbound mail.

The MSA is a sort of “receptionist” for new messages injected into the system by local user agents. An MSA sits between the user agent and the transport agent and takes over several functions that were formerly a part of the MTA’s job. An MSA implements secure (encrypted and authenticated) communication with user agents and often does minor header rewriting and cleanup on incoming messages. In many cases, the MSA is really just the MTA listening on a different port with a different configuration applied.

MSAs speak the same mail transfer protocol used by MTAs, so they appear to be MTAs from the perspective of user agents. However, they typically listen for connections on port 587 rather than port 25, the MTA standard. For this scheme to work, user agents must connect on port 587 instead of port 25. If your user agents cannot be taught to use port 587, you can still run an MSA on port 25, but you must do so on a system other than the one that runs your MTA; only one process at a time can listen on a particular port.

An MSA can help with several spam-induced problems. Infected home PCs are being used to send large amounts of spam. As a result, many ISPs that offer home service either block outgoing connections to port 25 or require account verification as part of the SMTP conversation. A home PC could use the ISP’s own mail server for outgoing mail, but some of the newer spam-fighting mechanisms such
