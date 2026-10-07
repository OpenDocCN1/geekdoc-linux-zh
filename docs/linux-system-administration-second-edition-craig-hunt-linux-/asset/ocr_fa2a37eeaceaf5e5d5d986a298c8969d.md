with similar packages.

**Note:**Just as sendmail isn’t the only SMTP server, the POP and IMAP servers included in the imap-2001a-10 package aren’t the only POP and IMAP servers. You’ll most likely need to look for an alternative package if you use qmail as your MTA, because qmail stores e-mail in different locations than do most other MTAs, which confuses most POP and IMAP servers. The qmail Web site includes links to alternative POP and IMAP servers that work with qmail. Exim and Postfix are compatible with the standard imap package, however.

The POP and IMAP daemons are normally run from a *super server*, as described in Chapter 12. Red Hat 7.3 and Mandrake 8.2 use the xinetd super server, but most other distributions in 2002 use inetd. The configuration of these programs differs.

If your distribution uses xinetd, the /etc/xinetd.d directory probably contains files named for the POP and IMAP servers, such as imap,ipop2, and ipop3. (These files are installed with the imap package, so you won’t see them until you install imap.) Secure variants use files whose names end in s. Chapter 12 includes a discussion of the format of files in /etc/xinetd.d. By default, these files include lines like the following:

```
```
disable = yes
```
```

This line deactivates the server in question. If you want to run a POP or IMAP server, you must do two things to activate it if you’re using xinetd:

+   1. Change the disable = yes line to read disable = no, or delete the line entirely, and save the changes. You can do this for just one server (POP-3, for instance), or for several.
2. Restart xinetd by typing **/etc/rc.d/init.d/xinetd restart**.

If your distribution uses inetd rather than xinetd, the procedure is somewhat different. You must edit the /etc/inetd.conf file to enable POP or IMAP servers run from inetd. To do so, follow these steps:

+   1. Open the /etc/inetd.conf file in a text editor and locate the line corresponding to the protocol you want to enable. It probably begins with a pound sign and the protocol name, as follows:
   # pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
2. Remove the pound sign and save the result. You can do this for multiple protocols, if you wish.
3. Restart inetd by typing **/etc/rc.d/init.d/inet restart**.

Once you’ve done this, your system should be configured as a server for whichever pull mail protocols you selected. You can test the server by using an appropriate MUA on another computer or by using a Telnet program to test the server manually, as shown in Listings 14.2 and 14.3.

# ## Setting Up Mail-Only Accounts

Ordinarily, Linux accepts mail only for recipients who have an account on the server. For example, if mail is addressed to nemo@pony.express.gov, and if pony.express.gov has no user called nemo, the server bounces the mail—the sender receives back a message that includes an error message stating that nemo isn’t a valid recipient. Therefore, you must normally create user accounts for all e-mail recipients, even if the computer is used *only* as a mail server.