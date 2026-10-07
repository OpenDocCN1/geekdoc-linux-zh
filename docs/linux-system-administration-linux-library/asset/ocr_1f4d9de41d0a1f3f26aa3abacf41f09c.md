# Configuring Sendmail 583

You should change desired-address.com to the address you want to use as the return address, of course. The first line causes the From: header to change. This header is the one that most MUAs use to determine the sender and the address to which replies are sent. The FEATURE(masquerade_envelope) line causes sendmail to make additional header substitutions, which can be useful if an MUA uses a nonstandard header to determine the sender's address. These options do not change the Received: headers, which are the most diagnostic for tracing mail back to its true source.

NOTE Some MUAs can change the From: header. Changing your sendmail configuration may therefore be overkill. If you use a From: address using an MUA, that overrides anything else using sendmail's masquerading features.

# Configuring Relays

Declared earlier, in “Push and Pull Protocols,” it's common for an email message to be relayed several times from its source and its destination. There's a good chance you must cope with this situation in one way or another. In some cases, you might want or need to use an outgoing relay, which in your computer passes its mail to another system, which delivers the mail to its destination. In other cases, you might need to configure a computer so that it functions as an outgoing relay; other computers (such as mail clients on your own domain) configure your Linux box to send their mail. Each configuration requires its options.

# Using an Outgoing Relay

All things being equal, sendmail is capable of delivering mail to any other MTA to the sendmail program can connect. In most cases, this means that sendmail can deliver mail to any system on the Internet that runs its own SMTP server. It is either to configure a Linux computer to deliver mail directly, which makes this efficient use of network resources and bypasses a potentially unreliable relay mail. The Linux computer might be the official mail server, well. There are, however, possible problems and limitations associated with sending mail directly. These include:

Unreachable destinations If the destination mail server is unavailable because it's crashed or because of network problems, sendmail must hold the mail locally until the problem clears up. It also periodically reattempt delivery. These actions consume CPU time, disk space, and network resources, in all probability very little of each. Of potentially greater importance, if the system that's sending the mail has an intermittent Internet connection (such as a PPP link), subsequent attempts may fail because that connection is down, resulting in a failure to deliver the mail at all, rather than a short delay.

Networking and Troubleshooting nPART 5