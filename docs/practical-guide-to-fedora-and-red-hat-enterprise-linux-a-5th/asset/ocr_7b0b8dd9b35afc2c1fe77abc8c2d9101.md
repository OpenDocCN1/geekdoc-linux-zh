Each log entry starts with a timestamp, the name of the system sending the email, the name of the mail server (sendmail), and a unique identification number. The address of the recipient follows the to= label and the address of the sender follows ctiaddr=. Additional fields provide the name of the mailer and the time it took to send the message. If a message is sent correctly, the stat= label is followed by Sent.

A message is marked Sent when sendmail sends it; Sent does not indicate that the message has been delivered. If a message is not delivered because an error occurred further down the line, the sender usually receives an email saying that it was not delivered and giving a reason why.

If you send and receive a lot of email, the maillog file can grow quite large. The rsyslog logrotate (page 579) entry is set up to archive and rotate the maillog files regularly.

# ALIASES AND FORWARDING

Three files can forward email: .forward (page 676), aliases (discussed next), and virtusertable (page 682). Table 20-1 on page 682 compares the three files.

+   et/aliases  Most of the time when you send email, it goes to a specific person; the recipient, user@system, maps to a specific, real user on the specified system. Sometimes you may want email to go to a class of users and not to a specific recipient. Examples of classes of users include postmaster, webmaster, root, and tech_support. Different users may receive this email at different times or the email may be answered by a group of users. You can use the /etc/aliases file to map inbound addresses to local users, files, commands, and remote addresses.

Each line in /etc/aliases contains the name of a local pseudouser, followed by a colon, whitespace, and a comma-separated list of destinations. The default installation includes a number of aliases that redirect messages for certain pseudousers to root. These have the form

```
system:		root
```

Sending messages to the root account is a good way of making them easy to review. However, because root's email is rarely checked, you may want to send copies to a real user. The following line forwards mail sent to abuse on the local system to root and alex:

```
abuse:		root, alex
```

You can create simple mailing lists with this type of alias. For example, the following alias sends copies of all email sent to admin on the local system to several users, including Zach, who is on a different system:

```
admin:		sam, helen, mark, zach@tcorp.com
```

You can direct email to a file by specifying an absolute pathname in place of a destination address. The following alias, which is quite popular among less conscientious system administrators, redirects email sent to complaints to /dev/null (page 469), where they disappear:

```
complaints:	/dev/null
```