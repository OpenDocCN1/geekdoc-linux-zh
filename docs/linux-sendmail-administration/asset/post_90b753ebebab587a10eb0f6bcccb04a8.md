
# Chapter 6 Using Sendmail Databases

```
>>> RSET
250 2.0.0 Reset state... Saved message in /home/logan/dead.letter
/home/logan/dead.letter
Closing connection to wren.foobirds.org.
>>> QUIT
221 2.0.0 wren.foobirds.org closing connection
```

Other than deleting lines from the EHLO response Listing 6.3 appears exactly as it happened. Sendmail was invoked with -v and -t so that I could type the test in the keyboard and receive verbose responses. The first four lines, which are shown in bold, and what I typed. The remainder is the response from the remote email server. As to the line clearly shows, the mail was addressed to bill@robin.foobirds.org. The first line displayed by Sendmail says that it is connecting to wren.foobirds.org via the smtp mail. Mail addressed to wren.foobirds.org is being sent to wren, which means wren must be the preferred mail exchange for robin. Great, except that apparently told the administrator of wren! The 550 response line, in bold italics, is an error message saying that wren will not relay mail bear from robin. Well, we didn't want to relay mail, but we did want to accept mail for robin, but it clearly won't do. What is wrong is the name robin.foobirds.org is not a valid alias for wren.foobirds.org, so wren will not accept mail for robin.

To correct this, robin must be added to class w. There are two ways this can be done. One way is to add the value directly to class w in the Sendmail configuration using the LOCAL_DOMAIN macro command, in this example:

This works if there are only a few hosts to add. It is straightforward and everything is contained in the Sendmail configuration file.

The other way to add hostnames to class w is to put them in the local-host-names file. Putting the hostname aliases in the local-host-names file is better whenever there are several names to add or the list of names changes over. In the case of both the generic-linux.mc and redhat.mc configurations, using the local-host-names file is also simpler because the FEATURE(use_cw_file) command is already in the configuration. There is no need to add a LOCAL_DOMAIN command or to rebuild the sendmail.cf file. Listing 6.4 shows the local-host-names file with two entries for robin and it shows a SIGHUP signal sent to Sendmail to make sure Sendmail loads the new values.

# Listing 6.4 Entries in the local-host-names File

```
[root]# cat local-host-names
# local-host-names - include all aliases for your machine here.
#
robin.foobirds.org
robin
[root]# ps -ax | grep sendmail
542 ? S 0:00:: accepting connections
[root]# kill -HUP 542
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <reuses> <address>
$=w
robin.foobirds.org
wren.foobirds.org
[172.16.12.3]
wren
localhost
robin
>^D
```

Now wren will accept mail for robin, although it won't necessarily know what to do with it. If Jill will be downloading her mail from a mailbox on wren, you must create a valid user account for Jill to allow Sendmail to create the necessary spool directory to hold her mail and allow her to download the mail via POP or IMAP. If Jill's is supposed to be forwarded to another system, mail routing instructions must be given to Sendmail through the aliases database or another appropriate database. Clearly, adding hostnames to class w is essential, it is only a first step. A possible next step is to configure the aliases database.

# The aliases Database

Once mail is accepted by the Sendmail server for local delivery, Sendmail must decide how to deliver the mail. It must determine whether the user identified in the recipient address is a local user with a local mailbox, or a user alias whose must be forwarded to the real recipient. The primary database used to make this determination is the aliases database.

# Chapter 6 Using Sendmail Databases

Sendmail aliases perform important functions that are an essential part of creating a mail server. Mail aliases do the following:

- Specify nicknames for individual users. Nicknames can be used to direct mail addressed to special names, such as postmaster or root, to the real users who do those jobs. Aliases can simplify creation of a standard e-mail address structure for a domain because mail aliases have a more flexible structure than login usernames.

- Forward mail to other hosts. Sendmail aliases automatically forward mail to the host address included as part of the recipient address.

- Define mailing lists. An alias with multiple recipients is a mailing list.

Mail aliases are defined in the aliases file. The location of the aliases file is set by the ALIAS_FILE in the Sendmail configuration. The redhat.mc configuration file in Chapter 5 uses ALIAS_FILE to set the location of the aliases file to /etc/aliases. By default, Sendmail 8.11 locates the file in /etc/mail directory (/etc/aliases). Regardless of where it is, the basic format of entries in the aliases file is:

alias: recipient

The alias is the username from the e-mail address, and recipient is the name to which the mail should be delivered. The recipient field can contain a username, another alias, or a full e-mail address containing both a username and a hostname. Additionally, there can be multiple recipients for a single alias to create a mailing list. The aliases file delivered with a Red Hat system, with a few additions to illustrate the full range of uses for aliases, is shown in Listing 6.5.

# Listing 6.5 The Basic Red Hat aliases Database

```
#
# @(#)aliases          8.2 (Berkeley) 3/5/94
#
# Aliases in this file will NOT be expanded in the header for
# Mail, but WILL be visible over networks or /bin/mail.
#
# >>>>>>>>> The program 'newaliases' must be run after
# >> NOTE >>  this file is updated for any changes
# >>>>>>>>> show through sendmail.
```

Basic system aliases -- these MUST be present.
MAILER-DAEMON: postmaster
postmaster: root

# The aliases Database 151

```
# General redirections for pseudo accounts.
bin: root
daemon: root
games: root
ingres: root
nnbody: root
system: root
toor: root
uucp: root
```

```
# Well-known aliases.
manager: root
dumper: root
operator: root
webmaster: root
```

```
# trap decode to catch security alerts
decode: root
```

```
# Person who should get root’s mail
root: staff
```

```
# System administrator mailing list
staff: kathy, craig, david@parrot, sara@hawk, becky@parrot
owner-staff: staff-request
staff-request: craig
```

```
# User aliases
jill@egret.foobirds.org
norman.edwards: norm
edwardsn: norm
norm@hawk.foobirds.org
rebecca.hunt: becky@parrot
andy.wright: andy
sara.henson: sara
kathy.McCafferty: kathy
kathleen.McCafferty: kathy
```

The Red aliases file opens with several lines, which begin with a pound sign (#). Ignore the information about which mail programs display aliases in the headers of mail messages; it is not really significant. The comment that is significant is the one that tells you to run aliases every time you update this file. Sendmail does not read the (img/b082498451dba8cf2907c)

# Chapter 6 Using Sendmail Databases

aliases file. Instead, it reads a database produced from this file by the newaliases command—e.g., sendmail -bi.

> NOTE newaliases is not really a program; it is a link to Sendmail.

The 151 lines in Listing 6.5 define aliases for special names. The first two, MAILER-DAEMON and postfix, are aliases that people expect to find on any system running Sendmail. Most of the others are assigned to the daemon usernames as found in the /etc/passwd file. One can actually log using the daemon usernames, so any mail that might be directed to these accounts is forwarded to a real user account. Of course you don't want people logging into the root account to read mail, so the aliases file has an alias for root. In the example, I wrote the root entry to forward all mail to staff, which is another alias.

The staff alias is a mailing list. A mailing list is simply an alias with multiple recipients. In the example, five people are responsible for maintaining this mail server. Messages addressed to root are delivered to all of these people through the staff mailing list.

Two special aliases are associated with the mailing list. The owner-staff alias is a special alias used by Sendmail for error messages to the mailing list. The format for this alias is owner-list, where list is the name of the mailing list. The other special alias, staff-request, is not required by Sendmail but it is expected by remote users. By convention, manual mailing list maintenance requests, such as being added or deleted from a list, are sent to the list-request, where list is the name of the mailing list.

The last lines are user aliases I added to the file. These lines direct mail received at the mail server to users who read their mail. The first alias directs this mail server receives for Jill. (Refer to Listing 6.3.) Remember that when we classed class w, it pointed out that adding a hostname to class does not mean that the server will be able to handle the mail for a specific user on remote host. The user needs either an account on the server or an alias in the aliases database. This means that it is not necessary to create a user account for Jill on the mail server her mail is forwarded to egret. fobirds.org. It is egret's job to see that Jill gets her mail.
