# Chapter 14

# Simple Security:
A GroupWise/SMTP Connection

*Jonathan Feldman*

Getting Internet e-mail to your LAN in a secure way does not necessarily imply the existence of a TCP/IP firewall. In fact, if you run another protocol on your LAN, such as IPX/SPX or VINES, it is possible to use a translating gateway as a “mail courier” so that only mail protocols are dispatched. This effectively leaves the rest of your network secure—even if you use TCP/IP on your LAN.

Imagine two couriers exchanging top-secret packages. Ideally, the manager of the courier agency, you would want these couriers to speak different languages, so that all they could do is exchange packages and not communicate in any other way.

This method can be a good one if you don’t have funds for a firewall, the expertise to build one yourself, or even if you’re suspicious of the complexity of a firewall. As Chesnick and Belovitz observe in Firewalls and Internet Security (Addison Wesley, 1994): “All programs are buggy. . . . Large programs are even buggier than their size would indicate. . . . A security program has security bugs. . . . Exposed machines should run as few programs as possible; the ones that are run should be as small [and simple] as possible.”