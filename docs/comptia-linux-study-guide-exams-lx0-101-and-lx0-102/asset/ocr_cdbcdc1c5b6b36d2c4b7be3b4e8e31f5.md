You can also look for executable filenames for each email server in /usr/bin or /usr/sbin; but be aware that most Linux email servers include a program called sendmail. This is done for compatibility reasons; the original sendmail program was ubiquitous, providing a compatible interface for scripts and administrators helps other SMTP servers.

In addition to the SMTP server, a fully functional Linux email system is likely to include other software:

Pull Mail Servers Two pull mail protocols, POP and IMAP, are popular. If a Linux system function as a mail server from which users can read their email remotely, chances you'll install a POP or IMAP mail server package, such as Cyrus IMAP (http://cyrusimap.web.cmu.edu/) or Dovecot (http://www.dovecot.org).

Fetchmail This program, based at /fetchmail.berlos.de, fills an odd gap in the email-delivery chain. If you run a site that runs on an external ISP for email delivery, chances the ISP only supports POP or IMAP. If you want to use a variety of clients, you may want to run your own SMTP server, and perhaps you POP or IMAP to deliver mail locally. To do this, you need a program that pulls mail using POP or IMAP and injects it into a local SMTP queue. And that is of Fetchmail. Most sites don't need it, but for those who do, it's indispensable.

Mail Readers The final chain in email is the mail reader. Examples in Linux include Evolution (http://projects.gnome.org/evolution/), KMail (http://userbase.kde/KMail), Thunderbird (http://www.mozilla.org/en-US/thunderbird/), and mutt http://www.mutt.org). The mail utility, which is installed on most Linux systems by default, is the lowest-common-denominator email utility. It's described shortly, in "Sending and Receiving Mail". Most Linux clients enable reading from a local mail queue or from a remote POP or IMAP server. A multi-user system is likely to have multiple email clients, enabling each user to choose which client to use.

Neither not this book covers mail servers, Fetchmail, or mail readers in any detail. As a practical matter, you may need to learn how to configure any or all of the packages, depending on your site's needs. Fortunately, mail reader configuration, which is the most common task, is usually fairly straightforward, as long as you have information on the hostnames of your outgoing (SMTP) and incoming (POP, IMAP, or local queue) email servers.

# Working with Email

Although setting up an email server for a site is beyond the scope of this book and the exam, managing a few common mail server administrative tasks is not. I therefore describe some common administrative tasks involving sending and receiving mail using the mail1 utility, email queue management, configuring aliases, and forwarding email.