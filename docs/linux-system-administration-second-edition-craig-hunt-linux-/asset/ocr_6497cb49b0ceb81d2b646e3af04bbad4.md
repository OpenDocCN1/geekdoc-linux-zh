In the end, the principal advantage—and disadvantage—of IMAP is that it allows users to store e–mail messages on the mail server. This is very useful when users need to access mail from several different computers, but it increases the need for disk space on the mail server.

# ## Configuring Sendmail

MTA configuration is critically important to most mail servers, because the MTA is usually the most important part of the server. The most common MTA today is sendmail. This MTA ships with Red Hat and many other Linux distributions. Fortunately, most Linux distributions use reasonable sendmail configurations by default, so if you’re lucky, you may not need to touch your system’s sendmail configuration. Unfortunately, sendmail can be a tricky package to configure, so if you do need to change your system’s configuration, you may need to spend some time learning about sendmail.

# ### Alternatives to Sendmail

Sendmail is the most popular MTA in use today, but it’s far from the only one available. Indeed, some Linux distributions don’t even use sendmail by default; they install other MTAs. Linux Mandrake favors Postfix (http://www.postfix.org/), and Debian and its derivatives use Exim (http://www.exim.org/). Another popular MTA is qmail (http://www.qmail.org/), although it’s not the default choice of any distribution in 2002.

When should you consider using an MTA other than sendmail? One good reason to use an alternative MTA is if your distribution ships with one. Replacing Postfix or Exim with sendmail is possible, but it takes some effort and may cause problems for MUAs or other utilities that make assumptions about the mail configuration on a computer. Another reason to use an alternative MTA is if you dislike sendmail’s configuration options. As described shortly, sendmail configuration is a bit tedious, and some people simply dislike it. Finally, sendmail is a fairly old program, loaded with inefficiencies. Alternative mail servers may be able to run more quickly or handle a heavier load than can sendmail—but handling e–mail doesn’t tax most servers, even when running sendmail.

If you want to try another MTA, which should you use? If your distribution of choice comes with a specific MTA, that one’s a good candidate. Postfix and qmail are both designed in a modular manner, which improves speed and (in theory) reduces the potential for security problems. Of these two, Postfix is more compatible with sendmail’s command options, and so is typically an easier replacement MTA for a system that ships with sendmail by default.

If you choose to use an alternative MTA, you’ll need to locate documentation other than the “Configuring Sendmail” section of this chapter, because other MTAs use different configuration files and procedures. Your best bet is to read the documentation for your MTA of choice on its Web page.

# ## Configuring Domains

Every computer on the Internet has a name, such as the fictitious pony.express.gov. If a computer runs an MTA, it’s possible to address mail to users of that system, such as susan@pony.express.gov. Frequently, a business or other organization prefers to use a shorter e–mail address. Rather than using pony.express.gov, the desire is to use express.gov. This shortened address is easier for individuals to remember, and it doesn’t tie the mail down to a