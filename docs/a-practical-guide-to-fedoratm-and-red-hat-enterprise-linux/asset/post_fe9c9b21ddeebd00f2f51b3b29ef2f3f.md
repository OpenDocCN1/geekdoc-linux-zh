
## MAIL LOGS

The **sendmail** daemon stores log messages in `/var/log/maillog`. Other mail servers, such as Dovecot, might also log information to this file. Following is a sample log entry:

```
# cat /var/log/maillog
...
Jun 18 11:55:46 guava sendmail[12159]: r5IItJ1L500127: to=ogs@osbello.com, ctagdr=es@anguava.example.com (1000/1400), delay=00:00:01, xdelay=00:00:01, mailer=esmtip, pri=120315, relay=esm1-smt1-in-1.google.com, [74.125.129.27], dsn=2.0.0, stat=Sent (OK 1371581746 04s18594494pac.163 - gsmsp)
```

Each log entry starts with a timestamp, the name of the system sending the email, the name of the mail server (**sendmail**), and a unique identification number. The address of the recipient follows the **to**= label and the address of the sender follows **from**=. Additional fields provide the name of the mailer and the time it took to send the message. If a message is sent correctly, the **stat**= label is followed by **Sent**.

A message is marked **Sent** when **sendmail** sends it; **Sent** does not indicate the message has been delivered. If a message is not delivered because an error occurred farther down the line, the sender usually receives an email saying that it was not delivered and giving a reason why.

See the **sendmail** documentation for more information on log files. If you send and receive a lot of email, the **maillog** file can grow quite large. The *logrotate* (page 618) syslog entry archives and rotates these files regularly.

## ALIASES AND FORWARDING

You can use the *aliases*, *~/.forward* (page 474), and *virtusertable* (page 753) files to forward email. Table 20-1 on page 753 compares the three files.

Most of the time when you send email, it goes to a specific person: the recipient, **user@system**, maps to a real user on the specified system. Sometimes, however, you might want email to go to a class of users and not to a specific recipient. Examples of classes of users include **postmaster**, **webmaster**, **root**, and **tech.support**. Different users might receive this email at different times or the email might go to a group of users. You can use the */etc/aliases* file to map local addresses and classes to local users, files, commands, and local as well as nonlocal addresses.

Each line in */etc/aliases* contains the name of a local (pseudo)user, followed by a colon, whitespace, and a comma-separated list of destinations. The default installation includes a number of aliases that redirect messages for certain pseudousers to **root**. These have the form

```
adm:	root
```

Sending messages to the *root* account is a good way to make them easy to review. However, because *root*'s email is rarely checked, you might want to send copies to a real user. You can set up an alias to forward email to more than one user. The following line forwards mail sent to *abuse* on the local system to *sam* and *max* in addition to *root*:

```
abuse:	root, sam, max
```

It is common to forward mail sent to many special accounts to **root**. If Zach is to read mail sent and forwarded to **root**, you could fix each alias individually. Alternatively, you can simply add the following line *to the end* of the **aliases** file (order does matter in this case). This line forwards to Zach all mail sent and forwarded to **root**:

```
root:          zach
```

You can create simple mailing lists with this type of alias. For example, the following alias sends copies of all email sent to **admin** on the local system to several users, including Zach, who is on a different system:

```
admin:        sam, helen, max, zach@example.com
```

You can direct email to a file by specifying an absolute pathname in place of a destination address. The following alias, which is quite popular among less conscientious system administrators, redirects email sent to **complaints** to /dev/null (page 503), where it disappears:

```
complaints:      /dev/null
```

You can also send email to standard input of a command by preceding the command with the pipeline character (|). This technique is commonly used by mailing list software such as Mailman (page 762). For each list it maintains, Mailman has entries, such as the following one for **painting_class**, in the aliases file:

```
painting_class:  "|/var/lib/mailman/mail/mailman post painting_class"
```

### newaliases

After you edit /etc/aliases, you must either run **newaliases** while you are working with **root** privileges or restart **sendmail** to re-create the /etc/aliases.db file that **sendmail** reads.

### praliases

You can use **praliases** to list aliases currently loaded by **sendmail**:

```
# praliases | head -5
@: @
abuse: root
adm: root
amanda: root
daemon: root
```

### ~/.forward

Systemwide aliases are useful in many cases, but **non-root** users cannot make or change them. Sometimes you might want to forward your own mail: Maybe you want mail from several systems to go to one address, or perhaps you want to forward your mail while you are working at another office. The ~/.forward file allows ordinary users to forward their email.

Lines in a .forward file are the same as the right column of the aliases file explained earlier in this section: Destinations are listed one per line and can be a local user, a remote email address, a filename, or a command preceded by the pipeline character (|). Mail that you forward does not go to your local mailbox. If you want to forward mail and keep a copy in your local mailbox, you must specify your local username preceded by a backslash to prevent an infinite loop. The following example sends Sam's email to himself on the local system and on the system at example.com:

```
$ cat ~/.forward
sams@example.com
\sam
```

## RELATED PROGRAMS

**sendmail** The sendmail packages include several programs. The primary program, **sendmail**, reads from standard input and sends an email to the recipient specified by its argument. You can use **sendmail** from the command line to check that the mail delivery system is working and to email the output of scripts. See page 744 for an example. The command **apropos sendmail** displays a list of **sendmail**-related files and utilities.

**mailq** The **mailq** utility displays the status of the outgoing mail queue. When there are no messages in the queue, it reports the queue is empty. Unless they are transient, messages in the queue usually indicate a problem with the local or remote MTA configuration or a network problem.

```
$ mailq
/var/spool/mqueue is empty
Total requests: 0
```

**mailstats** The **mailstats** utility reports on the number and sizes of messages **sendmail** has sent and received since the date it displays on the first line:

```
$ mailstats
Statistics from Fri Dec 27 16:02:34 2013
 M msgsfr bytes_from msgsto bytes_to msgsrej msgsdis msgsqur Mailer
 0 0 0K 17181 103904K 0 0 0 prog
 4 368386 4216614K 136456 1568314K 20616 0 0 esmtp
 9 226151 26101362K 479025 12776528K 4590 0 0 local
 T 594537 30317976K 632662 14448746K 25206 0 0
 C 694638 499700 146185
```

In the preceding output, each mailer is identified by the first column, which displays the mailer number, and by the last column, which displays the name of the mailer. The second through fifth columns display the number and total sizes of messages sent and received by the mailer. The sixth, seventh, and eighth columns display the number of messages rejected, discarded, and quarantined, respectively. The row that starts with T lists the column totals, and the row that starts with C lists the number of TCP connections.

## CONFIGURING sendmail

The sendmail configuration files reside in /etc/mail, where the primary configuration file is **sendmail.cf**. This directory contains other text configuration files, such as **access**, **mailertable**, and **virtusertable**. The **sendmail** daemon does not read these files but instead reads the corresponding *.db files in the same directory.
