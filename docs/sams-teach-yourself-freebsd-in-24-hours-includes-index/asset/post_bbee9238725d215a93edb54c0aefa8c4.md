
features and options that override the defaults in the standard config file—much in the same fashion that /etc/rc.conf overrides /etc/defaults/rc.conf. To make your changes to the Sendmail configuration, you will want to make them in this file, using the otherwise mostly unknown m4 macro language, and then compile a new sendmail.cf file from it.

The contents of freebsd.mc look like this (the dnl that marks the commented-out lines stands for delete through newline):

```
dnl Uncomment the first line to change the location of the default
dnl /etc/mail/local-host-names and comment out the second line.
dnl define(`confCW_FILE',`o /etc/mail/sendmail.cw')
define(`confCW_FILE',`o /etc/mail/local-host-names')
```

As you can see, the contents of these lines are designed to be read by a program, but not so much by a human. Believe it or not, the sendmail.cf file that is generated from this is even less readable.

There's a Makefile in /etc/mail, which allows you to create a new .cf file from the freebsd.mc file simply by typing make cf from inside that directory. Then, install this output file (freebsd.cf) into sendmail.cf using make install.

```
# make cf
/usr/bin/m4 -D CF_DIR=/usr/share/sendmail/cf/
/usr/share/sendmail/cf/m4/cf.m4 freebsd.mc > freebsd.cf
# make install
install -c -m 444 freebsd.cf /etc/mail/sendmail.cf
```

The /etc/mail/Makefile has a number of other uses, as you'll see in a moment.

## Creating Mail Aliases

A mailbox exists in /var/mail for every user on the system; however, someone isn't required to have an account in order to have an email address on your machine. You can always set up aliases to map incoming email addresses to any other address, whether it's another account on your machine, an address somewhere else on the Internet, or even a pipe to a file or program. The default /etc/mail/aliases contains examples of all these. An alias line contains the alias name, a colon, a space or tab, and the target address or pipe:

| Example | Description |
|---|---|
| tiger: bob@stripes.com | Redirects to bob@stripes.com |
| fsmth: frank | Goes into frank's mailbox instead of fsmth's |
| pager: "|/usr/local/bin/pageme" | Sends the message as input into /usr/local/bin/pageme |
| dump: "|>/home/frank/dump2me" | Appends the message to the dump2me file |
| mylist:include:/home/frank/list.txt | Expands to include all the addresses in list.txt |

After you make any change to /etc/mail/aliases, you have to rebuild the aliases.db file, which is a faster hash table version of the aliases file. You can use the traditional newaliases command to do this; or for consistency's sake with the rest of the maintenance tasks, use make aliases:

```
# make aliases
/usr/sbin/sendmail -bi
/etc/mail/aliases: 22 aliases, longest 10 bytes, 213 bytes total
```

![](img/ba0161b65b37e94cffc801ecbacaba5e_393_0.png)

> Global aliases aren't the only way to redirect mail from one local address to another or to an external address. For instance, if a user wants all his incoming mail to be forwarded automatically to some external address, you could use /etc/mail/aliases to do the trick, but this involves root access; there's a better way if the user has a full account on the system.
> 
> All a user has to do to forward mail to another address is to create a .forward file in his home directory, containing the forwarding email address. This can be done with any text editor, or even simply with echo:
> 
> # echo "frank@somewhereelse.com" > .forward
> 
> Removing this file will cause mail forwarding to stop.

## Blocking and Allowing Specific Senders

The access database, /etc/mail/access, provides a way to apply certain rules to single hosts, subnets, or whole groups of addresses—an excellent anti-spam provision. Applicable rules include OK, REJECT, RELAY, DISCARD, or 550 <message>. The contents of the default /etc/mail/access file show examples of how the address/hostname field can be formatted:

```
cyberspammer.com      550 We don't accept mail from spammers
FREE.STEALTH.MAILER@  550 We don't accept mail from spammers
another.source.of.spam REJECT
okay.cyberspammer.com OK
128.32                RELAY
```

- OK accepts messages from the specified host, regardless of whether that host might fail other checks in the system (such as the anti-relaying provisions that we will discuss shortly).
- REJECT refuses connections initiated by the specified host.
- DISCARD silently drops messages after accepting them, making the sender think that the message has been successfully delivered.
- RELAY enables relaying for the specified host, overriding other checks (as with OK).
- 550 <message> specifies a "rejection" message that is displayed to a sender, matching the host specification. This message will appear during the SMTP session, and will be included in an error email message that is sent back to the sender.

After you've made changes to /etc/mail/access, the access.db file must be regenerated. This is done with the make maps target, which regenerates any of the feature map files that have been changed since the last time make maps has been run. Follow this command with make restart to restart the Sendmail master process with the new access.db file:

```
# make maps
/usr/sbin/makemap hash access.db < access
# make restart
/bin/kill -HUP `head -1 /var/run/sendmail.pid`
```

## Other Configuration Files

There are more files in /etc/mail that control Sendmail's operation: /etc/mail/virtusertable and /etc/mail/local-host-names are both important for advanced Sendmail configuration, such as an installation in which your server hosts email services for multiple domains. The virtusertable file allows you to set up mappings of user-names at other hosted domains to go to other local users' mailboxes at your normal domain; think of it as an aliases file on steroids. The local-host-names file allows you to specify which domains you're hosting mail for.

The complete documentation for how to use the virtual-hosting database and other configuration files can be found at http://www.sendmail.org, the Sendmail Consortium's Web site.

## Controlling Sendmail

Sendmail operates by keeping a single master process running and listening on port 25 for incoming connections—as well as additional processes for handling queue runs, sending messages to remote recipients, and other tasks. The master process is started at boot time from /etc/rc. Starting and stopping the Sendmail master process is made easy by Makefile and the integrated nature of the resource configuration files in /etc. To start the Sendmail server, simply go into /etc/mail and enter make start:

```
# make start
( ./etc/defaults/rc.conf; source_rc_confs; if [
'${sendmail_enable}' = 'YES' -a -r /etc/mail/sendmail.cf ];
then /usr/sbin/sendmail ${sendmail_flags}; fi )
```

Because this command echoes its actions, you can see that it pulls in relevant configuration details from the systemwide resource configuration files—in which flags such as -q30m (do a queue run every thirty minutes) and -bd (run as a background daemon) are centrally specified. It will even refuse to start the process if the sendmail_enable variable in the rc.conf files is set to NO.

Restarting or stopping the master process is equally simple:

```
# make restart
/bin/kill -HUP `head -1 /var/run/sendmail.pid`
# make stop
/bin/kill -TERM `head -1 /var/run/sendmail.pid`
```

You can see what state each Sendmail process is in by using ps in wide mode in conjunction with grep; each process reports its position in the queue as an argument against its name in the process table. The following example shows the master process (51248) and a process in the middle of a queue run (54150):

```
51248 ?? Ss 0:00.17 sendmail: accepting connections (sendmail)
54150 ?? I 0:00.02 sendmail: /f4Q6KWV16827
@mail.backstreetboys.com.: user open (sendmail)
```

## The Message Queue

Messages waiting to be sent by Sendmail sit in /var/spool/mqueue. In Sendmail's default configuration, a new sendmail -q process is started every 30 minutes, stepping through each queued message and attempting to deliver it to its destination. This continues for five days: At the end of which, an undeliverable message is returned to the sender with the relevant error headers attached.

If you have some messages in your queue, which you almost certainly will if you've been using the system for any length of time, you can browse through them at will. Unlike opaque systems such as Microsoft Exchange in which queue files are kept in a database without an easy way to tweak or even see the files waiting to be sent, Sendmail provides both. Queued messages are just plain-text files, capable of being read and edited by regular text editors. This gives the administrator great control over how the mail system operates; however, it also provides an opportunity for the administrator to abuse his
