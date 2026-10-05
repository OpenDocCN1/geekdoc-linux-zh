# amavisd-new

RCPTs and can introduce a delay of, say, 15 seconds between RCPTs for connections that are abusing them.

We cover spam-related configuration options with the rest of the details of MTA configuration. For sendmail, see page 789; for Exim, see page 818; for Postfix, see page 840. DKIM and ADSP are discussed in more detail on page 845 of the chapter and in Chapter 17, beginning on page 590.

# MailScanner

Julian's MailScanner (mailscanner.info) is an actively maintained, flexible, open source scanner for mail hubs; it recognizes spam, viruses, and phishing tactics. It is written in Perl and uses external antivirus (ClamAV and 25 other tools) and antisam (Spam.Assassin) software. This antiphishing component, called ScamNail (mailscanner.info), is independent and does not depend on MailScanner. You can adjust MailScanner's configuration rules at the granularity of users, domains, or IP addresses.

MailScanner is not a milter, but rather a stand-alone program that operates on the MTA's mail queues. For example, you might configure the MTA in your DMZ to accept messages (in-line checks with milters, blacklists, etc.) and put them in an inbound queue. You would have MailScanner read messages from that queue, do its antisam, antivirus, and antiphishing magic, and transfer the messages that must enter a separate outbound queue. Another instance of the MTA could then process the outbound queue and deliver the messages.

One disadvantage of this system is that mail rejected by MailScanner creates bounce messages and can therefore contribute to backscatter spam.

Although MailScanner is free, commercial support is available. It also has an active user mailing list and a dedicated IRC channel that is monitored 24/7. It's well documented both-line and in the book MailScanner: A User Guide and Training-Manual by Julian Field. MailScanner's configuration file comes with many comments that the configuration primitives almost get lost; once you're an expert, you might want to delete some of the boilerplate.

You can capture statistics from MailScanner through a web front-end called MailWatch. MRTG can graph the data, as illustrated in Exhibit C (next page). Note the huge spike that occurred on September 19th, probably an attack of some type.

# amavisd-new

amavisd-new is an interface between MTAs and various spam and scanners such as ClamAV and SpamAssassin. It was originally based on AmAV (A Mail Virus Scanner) but has little in common with the original these days. It is written in Perl and is developed by Mark Martinec; the web site is ijs.si/software/amavis. We follow the maintainers' conventions in referring to the overall package as **amavisd-new**: however, the daemon itself is called amavisd.

![](bbox=[0.953, 0.226, 0.992, 0.353])