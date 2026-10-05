
## SETTING A MAIL SERVER (exim4)

- *Accepts email originating on local systems for delivery to local systems.
- *Accepts email originating on local systems for delivery to nonlocal systems, delivering it using an SMTP server (a smarthost)—typically an ISP—to relay email to its destination.
- Does not deliver email originating on nonlocal systems. As is frequently the case, you need to use POP or IMAP to receive email.
- Does not forward email originating on nonlocal systems to other nonlocal systems (does not relay email).

To set this up, you need to change the values of a few configuration variables in /etc/exim4/update-exim4.conf (page 724) and restart exim. The dpkg-reconfigure utility (page 726) you are editing in this file; this JumpStarts uses another editor. With root privileges, use a text editor to make the following changes to update-exim4.conf.

```
dc_eximconf_configtype='smarthost'
smarthost='mail.example.net'
```

Configuration type: Set the dc_eximconf_configtype to smarthost configuration variable to smarthost to cause exim4 to send bound for nonlocal systems to the system that the smarthost configuration variable specifies. This line should appear exactly as shown in the preceding example.

With dc_eximconf_configtype set to smarthost, smarthost to the FDN or IP address (preferred) of the remote SMTP server (a smarthost) that exim uses to relay email to nonlocal systems. Replace mail.example.net with this FDN or IP address. For Boolean variables in update-exim4.conf, exim4 interprets the null value (specified by '') as a value of false. With these changes, the file should look like this:

```
$ cat /etc/exim4/update-exim4.conf
...
dc_eximconf_configtype='smarthost'
dc_other_hostnames='example.com'
dc_local_interfaces='127.0.0.1 ; ::1'
dc_readhost=''
dc_relay_domains=''
dc_minimalhosts='false'
dc_relay_nets=''
dc_smarthost='mail.example.net'
FILEMODE='644'
dc_use_split_config='false'
dc_hide_mailname=''
dc_mailbox_in_oh='true'
dc_localdelivery='mail_spool'
```

The exim4 server does not use the value of the dc_local_interfaces variable in a smarthost configuration, so you can leave it blank. However in other configurations, the value of 127.0.0.1 ; ::1 prevents exim4 from accepting email from nonlocal systems. It is a good idea to configure exim4 this way and change this variable only when you are ready to accept mail from other systems.

To minimize network accesses for DNS lookups, which can be helpful if you are using a dial-up line, change the value of the dc_minimaldns variable to true.

/etc/mailname initially holds the name (uname -n) of the server. The string stored in /etc/mailname appears as the name of the sending system or the envelope-from and From lines that originate on the local system. If you want an email to come from a different system, change the contents of this file. You can modify this file using a text editor; the dpkg-reconfigure utility can also change it.

The following cases mail sent from the local system to appear to come from username@example.com, where username is the username of the user who is sending the email:

```
$ cat /etc/mailname
example.com
```

See page 724 for information on exim4 configuration variables. After making these changes, restart exim4 (page 716).

Test exim4 with the following command:

```
$ echo "my exim4 test" | exim4 user@remote.host
```

Replace user@remote.host with an email address on another system where you receive email. You need to send mail to a remote system to make sure exim4 is sending email to the SMTP server (the smarthost). If the mail is not delivered, check the email of the user who sent the email (on the local system) for errors. Also check the log file(s) in the /var/log/exim4 directory.

## JumpStart: CONFIGURING exim4 TO SEND AND RECEIVE MAIL

To receive email sent from a nonlocal system to a registered domain (that you control), you need to configure exim4 to accept email from nonlocal systems. JumpStart describes how to set up a server that:

- Accepts email from local and nonlocal systems.
- Delivers email that originates on local systems to a local system or directly to a nonlocal system, without using a relay.
- Delivers email that originates on nonlocal systems to a local system only.
- Does not forward email originating on nonlocal systems to other nonlocal systems (does not relay email).

This server does not relay email originating on nonlocal systems. (You must set the dc_relay_domains variable [page 726] for the local system to act as a relay.) For this configuration to work, you must be able to make outbound connections and receive inbound connections on port 25.

Working with root privileges, use a text editor to set the following in update-exim4.conf:

```
dc_eximconf_configtype='internet'
dc_other_hostnames='example.com'
```

Configuration type: Set the dc_eximconf_configtype to smarthost configuration variable to smarthost to cause exim4 to send bound for nonlocal systems to the system that the smarthost configuration variable specifies. This line should appear exactly as shown in the preceding example.

With dc_eximconf_configtype set to smarthost, smarthost to the FDN or IP address (preferred) of the remote SMTP server (a smarthost) that exim uses to relay email to nonlocal systems. Replace mail.example.net with this FDN or IP address. For Boolean variables in update-exim4.conf, exim4 interprets the null value (specified by '') as a value of false. With these changes, the file should look like this:

```
$ cat /etc/exim4/update-exim4.conf
...
dc_eximconf_configtype='smarthost'
dc_other_hostnames='example.com'
dc_local_interfaces='127.0.0.1 ; ::1'
dc_readhost=''
dc_relay_domains=''
dc_minimalhosts='false'
dc_relay_nets=''
dc_smarthost='mail.example.net'
FILEMODE='644'
dc_use_split_config='false'
dc_hide_mailname=''
dc_mailbox_in_oh='true'
dc_localdelivery='mail_spool'
```

The exim4 server does not use the value of the dc_local_interfaces variable in a smarthost configuration, so you can leave it blank. However in other configurations, the value of 127.0.0.1 ; ::1 prevents exim4 from accepting email from nonlocal systems. It is a good idea to configure exim4 this way and change this variable only when you are ready to accept mail from other systems.

## WORKING WITH exim4

exim4 receives email from both local and nonlocal systems, it creates files in /var/spool/exim4/input. To identify a particular message, exim4 generates a 16-character ID and stores the body of the message in a file named by ID followed by -D. It stores the headers in a file named by -H.

Frozen messages: exim4 cannot deliver a message, it marks the message as frozen and makes no attempt to deliver it. If it has successfully delivered an email, exim4 removes files pertaining to /var/spool/exim4/input.

Mail addressed to the local system: By default, exim4 delivers email to the local system to users' files in /var/mail, in mbox format. In this directory, each user has a mail file named with the user's name. Mail remains in these until it is collected, typically by an MUA. The MUA collects the mail as directed.

Mail addressed to nonlocal systems: The scheme exim4 uses to process email addressed to a nonlocal system depends on how it is configured: It can send the email to a smarth, or send the email to the system pointed to by the MX record of the domain it is addressed to, or it can refuse to send the email.

mbox versus maildir: The mbox format holds all messages for a user in a single file. To prevent corruption, a process must lock this file while it is adding messages to or deleting from; the MUA cannot delete a message at the same time the MTA is adding messages. A competing format, maildir, holds each message in a separate file. This format does not use locks, allowing an MUA to delete messages from a user at the same time as mail is delivered to the same user. In addition, the maildir format is better to handle large mailboxes. The downside is it uses a protocol such as IMAP to check messages. Qmail (page 715), an alternative to sendmail and exim4, uses maildir mailboxes.

## MAIL LOGS

By default, exim4 sends normal log messages to /var/log/exim4/mainlog, with other messages going to other files in the same directory. The lines in mainlog describe an email message sent directly to a remote system's SMTP server. The exim4 daemon writes one line each time it receives a message and one line each it attempts to deliver a message. The Completed line indicates that exim4 has completed its part in delivering the message.
