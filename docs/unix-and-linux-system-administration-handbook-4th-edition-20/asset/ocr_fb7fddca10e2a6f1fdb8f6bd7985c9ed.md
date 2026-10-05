# Chapter 20 Electronic Mail

as SPF (page 767) and DKIM (page 845) require that mail that appears to be sent from an organization actually originate there.

If you use an MSA, be sure to configure your transport agent so that it doesn't duplicate any of the rewriting or header fix-up work done by the MSA. Duplicate processing won't affect the correctness of mail handling, but it represents less extra work.

Since your MSA uses your MTA to relay messages, the MSA and MTA must use SMTP-AUTH to authenticate each other. Otherwise, you will have a so-called open relay that spammers can exploit and other sites will blacklist for you.

# Transport agents

A transport agent must accept mail from a user agent or submission agent, understand the recipients' addresses, and somehow get the mail to the correct hosts for delivery. Transport agents speak the Simple Mail Transport Protocol (SMTP), which was originally defined in RFC2621 but has now been superseded and extended by RFC5321. The extended version is called ESMTP.

An MTA's list of choices, as both a mail sender and receiver, includes

+   * Receiving email messages from remote mail servers
* Understanding the recipients' addresses
* Rewriting addresses to a form understood by the delivery agent
* Forwarding the message to the next responsible mail server or passing it to a local delivery agent work to be saved to a user's mailbox

The bulk of the work involved in setting up a mail system relates to the configuration of the MTA. In this book, we cover three open source MTAs: sendmail, Exim, and Postfix.

# Local delivery agents

A delivery agent, sometimes called a local delivery agent (LDA), accepts mail from a transport agent and delivers it to the appropriate recipients' mailboxes on the local machine. As originally specified, email can be delivered to a person, to a mailing list, to a file, or even to a program. However, the last types of recipients can weaken the security and safety of your system

MTAs usually include a built-in local delivery agent for easy deliveries. procmail (procmail.org) and Maildrop (courier-mta.org/maildrop) are LDAs that filter or sort mail before delivering it. Some access agents (AAs) also have built-in-LDAs that do both delivery and local housekeeping.

# Message stores

The message store is the final resting of an email message once it has completed its journey across the Internet and been delivered to recipients.