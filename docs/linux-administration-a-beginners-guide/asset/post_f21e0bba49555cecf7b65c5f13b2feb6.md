
## INSTALLING SENDMAIL

Make sure your configuration file is in the /etc/fcf directory, relative to the main Sendmail directory that was created when the source code was unpacked. For the sake of discussion, let’s call the file we are working with ourconfig.mc.

- Run the command:

```bash
[root@ford ~]# cd ../mc/Mcf -o ourconf.mc > ourconf.cf
```

And that’s it. The file ourconf.cf has been created and is ready to use.

We now have Sendmail compiled and its configuration files ready to go. All we need to do is actually install these creations into their place and start it up. BUT, like any service, you should be sure to make backups of all of your existing binaries and configuration files before performing the installation. In the worst case where nothing works, you should be able to revert back to the old configuration quickly so that your users will experience minimal amounts of down time. Ideally, you should be able to install the new version so fast that no one even notices the mail server was down.

When you have your backup of the Sendmail binaries and configuration files, go back to the directory where you ran ./Build the first time (/usr/local/src/sendmail-8.9.3/src) and type:

```bash
[root@ford src] # ./Build install
```

This will copy the Sendmail binary into /usr/sbin and install the man pages into the appropriate directories. With the binaries in place, you need to copy the configuration file into the /etc directory. Go back to the directory where you created the ourconf.cf file and type:

```bash
[root@ford ~]# cp ourconf.cf /etc/sendmail.cf
```

With the files in place, kill Sendmail and restart it. Suggested command-line parameters are -bd and -q1h. The -bd option tells Sendmail to go into daemon mode so that it quietly sits in the background processing e-mail, and the -q1h option tells it to go back and process outstanding e-mail once an hour. (The default configuration for Sendmail is to try to process the e-mail immediately, and if it cannot contact the destination host, it will queue it for future delivery.) Thus the command line to start Sendmail is:

```bash
[root@ford /root] # /usr/sbin/sendmail -bd -q1h
```

It is a good idea to create a startup script for Sendmail if one doesn’t exist for it already. (Most likely, one was already created for you when you installed Linux.) See Chapter 7 for more information on startup and shutdown scripts.

## BEYOND THE PRIMARY CONFIGURATION FILE

Reading through the features that Sendmail offers us, we saw that there are many features that enable and disable the usage of additional configuration files. Some of these files are very straightforward and are explained in a sentence or two in the previous section, but there are two files in particular that are nontrivial: the aliases file and the access database file. In this section, we examine their format and learn how to write our own.

### The Aliases File

Sendmail's mail aliases file is one of its most powerful features. It allows you to create mailing lists, give users alternative e-mail aliases, and even pipe e-mail directly to external applications. Most configurations place the aliases in either `/etc/aliases` or `/etc/mail/aliases`. It’s unlikely to be anywhere else.

The format of the aliases file is reasonably straightforward. All comment lines begin with a pound symbol (`#`) and the remainder of the line is free form. Lines may also be blank to help define logical blocks.

Each alias must begin with the alias’s name, followed immediately by a colon. The remainder of the line is what Sendmail will expand that address to be. The content of the line can be one of six things: another alias, a list of aliases, another user, a list of users, a file, or an external application. Aliases and user names can be intermixed. Any aliases referenced on the right side of the colon must be already defined.

Assume the domain domain.com has the users boson, yom, achan, julia, sangeet, hde, and sshah. Let's look at what some of these aliases can be set up to do.

**Example:** We want a simple alias for Sangeet. Since she is the CEO, we set up an alias as follows:

```text
ceo: sangeet
```

Now any mail sent to `ceo@domain.com` will transparently be sent to Sangeet.

**Example:** We want to create an alias for three of our departments, engineering, mis, and management. We can create the aliases:

```text
engineering: boson, yom
mis: achan, sshah
management: julia, hde, ceo
```

Any mail sent to `management@domain.com` will automatically be forwarded to the users julia and hde and ceo. The ceo address will get expanded to sangeet.

**Example:** We want to create the alias everybody so that any mail sent to it will automatically be forwarded to all of the departments. We can do that with the following alias:

```text
everybody: engineering, mis, management
```

E-mail sent to everybody@domain.com will be expanded to engineering, mis, and management. Each of these aliases will expand to their respective users, with the management alias having one more expansion to convert ceo to sangeet.

Following the trend here?

> **WARNING:** Depending on the database backend compiled with Sendmail, you may not be able to get more than about 1000 characters-worth of addresses per alias. From the standpoint of good administrative practices, try to keep each individual alias down to a manageable size so that it is easy to follow what each one expands to.

**Example:** If we want all of the mail sent to a particular address to be copied to a file, we simply start the right side of an alias with a forward slash character (/), indicating that the rest of the line is a filename. So if we want messages sent to log@domain.com to be placed into a file called /tmp/log, we would set an alias, like so:

```text
log: /tmp/log
```

**Example:** If we want to pipe all of the e-mail sent to a particular alias to an external program, we can do so through this file. Assume that the external program is /etc/smrsh/external_program.

```text
abuse: "| /etc/smrsh/external_program"
```

> **NOTE:** If you configured Sendmail to use smrsh, you will need to be sure to place your binaries in the correct directory so that smrsh knows they are there. If you are sticking with the Red Hat installation of Smsh, this directory is /etc/smrsh. If you are compiling yourself, the default directory is /usr/sbin.

Once you are done creating the aliases file, you will need to use the newaliases command to convert the file into a database format that Sendmail can quickly read. Simply type:

```bash
[root@ford /etc]# newaliases
```

### The "Access" Database (Spam-Control)

When configuring Sendmail, you have the option of enabling the access_db. This feature allows you to use the /etc/mail/access file to list special actions for particular domain names, host names, IP addresses, and users. This feature is specially interesting because it unifies all of the spam control mechanisms in Sendmail into a single configuration file. The format of the file is simple: lines that begin with a pound symbol (#) are comments, blank lines are allowed, and the rest of the lines contain the actual configuration information.

The default features that are enabled when using the access_db feature allow you to list either the host name, domain name, IP address, or e-mail address, and specify whether you want a specific action on e-mail originating from there. The actions are listed in Table 15-2.

| Action | Description |
| :--- | :--- |
| OK | Accepts the message even if there are other rules that would otherwise reject it. For example, if you enable the feature to deny messages from domain names that cannot be resolved to an IP address, you can specify a specific exception domain using the OK action. |
| RELAY | Unless explicitly turned on, the default Sendmail configuration does not relay messages for other domains. This action overrides that rule for a specific domain. |
| REJECT | Refuses all messages from this site / person. This will cause a brief message to be sent back to the sender informing him that the message was rejected. |
| DISCARD | Discards the message entirely. No message is sent back to the sender. For all other reasons, the message was accepted. |
| SMTP-code message | SMTP-code must be a valid SMTP code as specified in RFC 821. message can be any text you want returned along with SMTP-code. |

**Table 15-2. access_db Features**

**Example:** To reject all messages from annoying-web-site.com, your entry would be:

```text
annoying-web-site.com REJECT
```

**Example:** To discard all messages from badperson@badpeople.com, we would use:

```text
badperson@badpeople.com DISCARD
```

**Example:** To relay all messages from the 138.23.x.x network, we would use:

```text
138.23 RELAY
```

**Example:** To reject all messages from spamathon.com with the SMTP message "550 No Spam Here." we would use:

```text
spamathon.com 550 No Spam Here.
```

**Example:** We can put all of these examples together into a single file:
