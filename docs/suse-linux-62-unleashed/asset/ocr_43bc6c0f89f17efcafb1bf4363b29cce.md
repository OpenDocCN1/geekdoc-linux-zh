# The v Operator: sendmail.cf Version Levels

As V.8 sendmaillevels, its author adds new features. The V operator tells V.8 sendmail which features it should expect to find in your configuration file. Older versions of sendmail don't understand this command. The SIOG explains the configuration file version levels in detail.

> The configuration file version level does not correspond to the sendmail version level. V.8 sendmail understands versions 1 through 5 of configuration files, and no such as one with 8 configuration files.

# The κ Operator: Key Files

sendmail has always used key databases—for example, the aliases databases. Given the key postmaster, sendmail looks up the data associated with that key and returns the names of the accounts to which the postmaster's mail should be delivered. V.8 sendmail extends this to arbitrary databases, including NIS maps (Sun's Network Information Service, formerly known as Yellow Pages or YP; see Chapter 17 for details). The κ operator tells sendmail the location of the database, its class, and how to access it. V.8 sendmail supports the following classes of user-defined databases: dbm, btree, hash, and NIS. The default used when compiling under Linux is one of the hash or btree formats. The SIOG for the lowdown on key files.

# The M Operator: Mailer Definitions

Mailers are either MTAs or delivery agents. Recall that the aliases file enables you to send mail to a login name (which might be aliased to a remote user), a program, or a file. A special mailer can be defined for each purpose, and even though the SMTP MTA is built in, it must have a mailer definition to tailor sendmail's SMTP operations.

Mailer definitions are important because all recipient addresses must resolve to a mailer in rules 0. Resolving to a mailer is just another name for sendmail's main function, mail routing. For example, resolving to the local router routes to the local user via the final delivery agent defined in that mailer (such as /bin/mail), and resolving to the SMTP router routes the letter to another host via sendmail's built-in SMTP transport, as defined in the SMTP mapper.

A concrete example of a mailer definition will make this information clearer. Because sendmail requires a local mailer definition, look at the following: