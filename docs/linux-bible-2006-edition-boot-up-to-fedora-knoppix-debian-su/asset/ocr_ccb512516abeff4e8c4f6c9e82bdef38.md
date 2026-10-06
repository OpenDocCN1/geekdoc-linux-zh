# Chapter 6 - Securing Linux 219

# Spam Relaying

Your e-mail services can also be abused by having your system used as a spam relay. Spam refers to the unsolicited junk e-mail that has become a common occurrence on the Internet. refers to the mail server feature that causes it to send mail it receives to another server.(Normally, only users with valid e-mail accounts on the server are allowed to use a mail server to relay messages in their behalf.) A mail server configured as an open relay will allow anyone to forward e-mail messages through it, and is therefore, considered to be a very bad practice.

Spammers often deliver their annoying messages from a normal dial-up Internet account. They need some kind of high-capacity mail server to accept and buffer the payload of messages. They deliver the spam to the server all in one huge batch and then log off, letting the server do the work of delivering the messages to many victims.

Normally, no-respecting Internet service provider will cooperate with this action, so spammers resort to hijacking servers at ISP to do the dirty work. Having your mail server hijacked as a spam relay can have a devastating effect on your system and your reputation. Fortunately, open mail relaying is deactivated by default on Fedora and Red Hat Linux installations. Open mail relaying is one security issue that you will not have to worry about.

You can allow specific hosts or domains to relay your mail through your system /etc/mail/access file with keyword Relay. By default, relaying is allowed from the local host only.

> One package might consider using to filter out spam on your mail server is SpamAssassin. SpamAssassin examines the text of incoming mail messages and attempts to filter out messages that are determined to be spam. SpamAssassin is described in Chapter 25.

# Smurf Amplification Attack

Smurfing refers to a particular type of service attack aimed at flooding your internet connection. It can be a difficult attack to defend against because it is not easy to trace the attack to the attacker. Here is how smurfing works.

The attack uses the ICMP protocol, a service intended for checking the speed and availability of network connections. Using the ping command, you send a network packet from your computer to another computer on the Internet. The remote computer will recognize the packet as an ICMP request and echo a reply to your computer. Your computer can then print a message revealing that the remote system is you and telling you how long it took to reply to the ping.

A smur attack uses a malformed ICMP request to bury your computer in network traffic. The attacker does this by bouncing a ping request off an unwitting third party in such a way that the reply is duplicated dozens or hundreds of times. An organization with a fast Internet connection and a large number of computers is used as the relay. The destination address of the ping is set to entire