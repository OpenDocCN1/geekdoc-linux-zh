![](bbox=[0.16, 0.12, 0.24, 0.19])

> You may recall that the *userdel* command, described in Chapter 7, includes options related to the handling of *users’ mail spools*. If you delete a user account but leave the user’s mail spool intact, the mail can still be accessed. If the mail server software stores mail in `/var/spool/mail/`, leftover mail spools can cause problems if you eventually re-use an old username.

E-mail can be sent as well as received. The traditional Linux approach to sending e-mail is to have local programs contact the local mail server to send e-mail. The local mail server then contacts its outgoing e-mail server, as in Figure 9.1. Most Linux e-mail clients (a.k.a. mail user agents, or MUAs), as well as similar programs on other platforms, provide the option to directly contact a remote SMTP server when sending e-mail. Such a configuration slightly simplifies the e-mail path but can make operation unreliable if the local network link goes down. If your e-mail client talks to an SMTP server that runs locally, the e-mail can be queued for delivery by the SMTP server even if the network is temporarily down.

# Choosing E-mail Software

Linux supports quite a few e-mail servers. Chances are, one of the major servers will be installed on your system by default. If not, and if you want to install one, you’ll have to pick one. You may also want to change your e-mail server if you need to configure it in advanced ways; some servers are easier to configure than others or support specific options that others don’t. Four e-mail servers are most popular on Linux:

Sendmail The sendmail program (http://www.sendmail.org) was for many years the dominant e-mail server package on the Internet. In recent years it’s lost some of its dominance to the other servers described here, as well as to Windows e-mail servers. Nonetheless, sendmail remains a popular server. It’s very powerful, but it’s also difficult to configure because its configuration file formats are rather arcane.

Postfix Postfix (http://www.postfix.org) was designed as a modular replacement for sendmail—rather than a single program that does everything (as sendmail is designed), Post-fix uses multiple programs, each of which handles its own specific small task. This design improves security, at least in theory. Postfix tends to be easier to configure than sendmail, and it’s become the default e-mail server on many Linux distributions.

Exim Although Exim (http://www.exim.org) is a monolithic server, like sendmail, it has a much simpler configuration file format and so is easier to configure. A few Linux distributions use Exim as the default e-mail server.

qmail The fourth major Linux e-mail server, qmail (http://www.qmail.org), is a modular server with security as a major design goal. Like Postfix and Exim, qmail is easier to configure than sendmail. It’s not the standard e-mail server in any Linux distribution because its license is a bit strange and complicates qmail distribution with Linux; however, many system administrators like qmail enough that they replace their distributions’ standard e-mail servers with qmail.