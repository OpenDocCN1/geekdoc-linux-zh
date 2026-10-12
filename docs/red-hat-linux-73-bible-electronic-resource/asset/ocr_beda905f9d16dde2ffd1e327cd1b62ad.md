```
# makemap hash access.db < access
```

Sendmail should now discard e-mail from the addresses you added.

# ## Spam relaying

Another way in which your e-mail services can be abused is by having your system used as a Spam Relay. *Spam* refers to the unsolicited junk e-mail that has become a common occurrence on the Internet. Spammers usually deliver their annoying messages from a normal dial-up Internet account. They need some kind of high capacity e-mail server to accept and buffer the payload of messages. They deliver the spam to the server all in one huge batch, and then log off and let the server do the work of delivering the messages to the many victims.

Naturally, no self-respecting Internet Service Provider will cooperate with this action, so spammers resort to hijacking servers at another ISP to do the dirty work. Having your mailserver hijacked to act as a spam relay can have a devastating effect on your system’s performance. Fortunately, mail relaying is deactivated by default on new Red Hat Linux installations. This is one security issue that you will not have to attend to. You can allow specific hosts or domains to relay mail through your system by adding those senders to your /etc/mail/access file with keyword RELAY. Refer to the chapter “Setting Up a Mail Server” as well as the sendmail documentation for more information.

# ## Smurfing

*Smurfing* refers to a particular type of denial-of-service attack aimed at flooding your Internet connection. It can be a difficult attack to defend against because it is not easy to trace the attack back to the attacker. Here is how smurfing works.

The attack makes use of the ICMP protocol, a service intended for checking the speed and availability of network connections. Using the ping command, you can send a network packet from your computer to another computer on the Internet. The remote computer will recognize the packet as an ICMP request and echo back a reply packet to your computer. Your computer can then print a message revealing that the remote system is up and telling you how long it took to reply to the ping.

A smurfing attack uses a malformed ICMP request to bury your computer in network traffic. The attacker does this by bouncing a ping request off an unwitting third party in such a way that the reply is duplicated dozens or even hundreds of times. An organization with a fast Internet connection and a large number of computers is used as the relay. The destination address of the ping is set to an entire subnet instead of a single host. The return address is forged to be your machine’s address instead of the actual sender. When the ICMP packet arrives at the unwitting relay’s network, every host on that subnet replies to the ping! Furthermore, they reply to your computer instead of the actual sender. If the relay’s network has hundreds of computers, your Internet connection can be quickly flooded.