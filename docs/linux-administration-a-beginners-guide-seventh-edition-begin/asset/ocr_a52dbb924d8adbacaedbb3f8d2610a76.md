# CHAPTER 14 Local Security 403

the sizes of the web or FTP directories grow significantly without reason, it may signal trouble looming with unauthorized use of your server.

A server disk fills fully unexpectedly is also a potential source of local (and/remote) DoS attack. A full disk may prevent legitimate users from storing new data or manipulating existing on the server. The server may also have to be temporarily taken offline to rectify the situation, thereby denying access to other services that the server should be providing.

# Automated Monitoring

Most of the popular automated system-monitoring solutions specialize in monitoring network-based services and daemons. However, most of these also have extensive resource-monitoring capabilities. The automated tools can monitor things as disk usage, CPU usage, process counts, changes in file system objects, and so on. A couple of these tools include sinuso utilities, Nagios plug-ins, and Tripwire.

# Mailing Lists

As part of managing your system's security, you should be subscribed to security mailing lists, as BugTraq (www.securityfocus.com). BugTraq is a moderated mailing list that generates only a small handful of e-mails a day, most of which may not pertain to the software you are running. However, this is where critical issues are likely to show up first and deal with real time as you do.

In addition to BugTraq, any security lists for software for which you are responsible are also must. Look for announcement lists for security issues that pertain to their specific distributions. Major software vendors also maintain their own lists. Oracle, for example, keeps its My Oracle Support portal and corresponding e-mail lists. Although this may seem like a lot of e-mail, consider that most of the lists that are announcement-based are extremely low volume. In general, you should not find yourself needing to deal with significantly more e-mail than you already do.

# Summary

In this chapter you learned about securing your Linux system and what you learned to look for when making decisions about how to balance features/functions with the need to secure. Specifically, the chapter covered the risks inherent in SetUID programs (programs that run in the context of a user, such as root), as well as the risks in running unnecessary programs. It also covers mitigating risk through the use of chroot environments and controlling access to users. We briefly discussed two popular implementations of the MAC security model in Linux: SELinux and AppArmor. Finally, you learned about some of the things that should be monitored as part of daily housekeeping.