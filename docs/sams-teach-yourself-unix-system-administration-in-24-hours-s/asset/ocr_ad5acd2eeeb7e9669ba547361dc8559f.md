![](bbox=[0.58, 0.02, 0.95, 0.45])

# Hour 20

# Working with E-mail

System administration involves managing a wide variety of services on one or more Unix system, but the one service that's guaranteed to get you into hot water if it breaks is electronic mail. Regardless of the level of sophistication of your user base, if they can't send and receive e-mail, you'll hear about it.

This hour focuses on how to work with sendmail, the standard mail transfer agent (MTA) on Unix systems. There are other MTAs available, including the popular postfix, exim, qmail, and smail programs, but just about every Unix I've seen ships with sendmail as the default.

It's also important to differentiate a mail transfer agent from other e-mail-related software. The program that lets you read, organize, and compose messages is know as a mail user agent, and examples of that range from Elm and Pine to Entourage and Outlook. There are X Window System-based applications, graphical applications like Apple Mail, and a wide variety of command line or shell-based mailers, but in Unix they all work by handing off outgoing messages to an MTA. The MTA—sendmail—is the program that either delivers mail locally, or connects to a remote system and feeds the message along the wire to the destination system (which is quite possibly also running sendmail).