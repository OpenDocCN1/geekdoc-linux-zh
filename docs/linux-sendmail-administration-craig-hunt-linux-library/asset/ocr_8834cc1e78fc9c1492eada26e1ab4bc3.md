On the left-hand side of the window, select one of the items from the linuxconf Anti-Spam Filters menu. There are four possible selections:

+   Setting Rejected Senders The Setting Rejected Senders selection creates a spam filter. The selection opens the Mail Rejected From tab. Click Add to open the tab shown in Figure 11.1. The Rejected Message tab is the place you define the spam rule, including both the source of the e-mail and the error message that will be sent to that source. Figure 11.1 shows that mail from we11junk.com will be rejected with the error message "550 Junk is not accepted." This is the only linuxconf menu selection that blocks e-mail. The other three mail filtering selections are used to loosen the mail-relaying restrictions so that you can create a server.

+   Setting ‘Relay’ for IP Use this selection to define a host or network for which the server should relay mail. Identify the host or network by IP number. This enables mail relaying for the specified host

+   Setting ‘Relay’ for name Use this selection to define a host or domain for which the server should relay mail. Identify the host or network by name.

+   Setting Relay to Hosts This selection identifies remote hosts to which the server should relay mail. A possible use is to identify an external mail server that your system relays may through—for example, your corporate mail server.

The linuxconf tool will build the access database file for you when you click the Act/Changes button, which stands for activate changes. linuxconf creates both the text file and the actual database.

If, like me, you build your access list with a text editor, you must also manually build the database. Use the makeup command that comes with Sendmail to convert the text file into a database. You also need to let Sendmail know that you have an access database and that you want to use. Use the access_db feature to do that. See Chapter 6 for details on building the access database and configuring Sendmail to use it.

The fine level of control that the access database gives you over selecting addresses and the various actions you can choose from when you get an address match means that the access database is the right tool for most sites to block spammers. But if you need even more control over the process, you can define your own Sendmail rewrite rules to process the e-mail addresses.

# Using Anti-Spam Rewrite Rules

Most administrators think of Sendmail rewrite rules as a way to modify addresses on out-bound e-mail that originates on the local system in the user’s mailer. The anti-spam