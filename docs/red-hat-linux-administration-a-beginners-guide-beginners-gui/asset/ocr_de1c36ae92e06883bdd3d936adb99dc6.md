# Progress Check

+   1.  Name two mail delivery agents (MDAs) that can be used with Sendmail.

+   2.  Why is allowing any site to relay e-mail through your server a bad idea?

# CRITICAL SKILL 13.3  Choosing Postfix

Among the many criticisms commonly leveled against Sendmail, the biggest ones are its security, complexity, and performance. A number of programs have sprung up to try to address these (among other) criticisms, in hopes of doing a better job than Sendmail. Among the competitive replacements, one of the most popular (and the only one we’ll cover here) is Postfix.

Postfix was created at IBM’s T. J. Watson Research Center by Wietse Venema with the intention of being fast, easy to configure, and secure. Originally known as VMailer, and then as IBM Secure Mailer, the program finally settled on the name Postfix in 1998. While Postfix is most known for its security approach, it also claims to be three times faster than its closest competitor.

Postfix is often compared with qmail, another MTA replacement with a strong security focus. But while Postfix borrows a number of architecture ideas from qmail, they differ in at least one important way. Postfix strives to be a drop-in replacement for Sendmail, to make migrating as painless as possible. As a result, Postfix directly supports a number of Sendmail files, such as /etc/aliases, /var/spool/mail, and ~/forward. Since Postfix tries to be simple to configure, however, it does not try to support sendmail.cf.

Unlike Sendmail’s monolithic architecture, Postfix is made up of a dozen or so small programs that each perform a single, specific task. In addition to the security advantage of making it easier to find unwanted side effects in a small, simple program, this also provides a great deal of flexibility. Machines that don’t need a specific function (such as local delivery, for example) can easily omit that daemon from their install. The majority of the component pieces are run without any special privileges, so even if an attacker does manage to break them, the potential damage is minimized. Also because of security concerns, the individual Postfix programs don’t really trust data passed to them, even if it’s from another part of Postfix, but instead validate for themselves (where applicable) any data passed to them.

+   1.  The local **mail** program and Procmail are two that are mentioned.

+   2.  Allowing anyone to relay e-mail through your server opens your server up to being used for spam by unscrupulous people.