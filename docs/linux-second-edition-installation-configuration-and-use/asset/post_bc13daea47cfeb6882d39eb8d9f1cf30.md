
computer-internal mail delivery. (For example, in case of faults or problems, programs automatically send mail to root.)

> Online information can be obtained with sendmail. Depending on the distribution, additional information can be found in /usr/doc/packages/sendmail. Further sources of help are the Mail-HOWTO and Chapter 15 of the Linux Network Administration Guide.

# Configuration

sendmail is controlled via the configuration file /etc/sendmail.cf. All distributions include at least one ready-to-use configuration file. Some distributions, for Slack and SuSE, offer a choice of several configuration variations depending on the intended use: for local networks without Internet connection, UUCP, and so on. The most suitable variation for offline use is the one with Internet connection and server support (DNS).

Even if the preset configuration files already function well, you frequently need minor changes to adapt sendmail optimally to the peculiarities of PPP/SLIP. Fortunately, sendmail.cf is well provided with comments, so that the meaning of many settings quickly becomes evident.

Before modifying sendmail.cf, you should first stop and subsequently restart sendmail. In Red Hat Linux, you need to execute the following commands:

```
# /etc/rc.d/init/sendmail stop
# /etc/rc.d/init/sendmail start
```

In SuSE the paths are slightly different:

```
# /sbin/init.d/sendmail stop
# /sbin/init.d/sendmail start
```

# Host name problems

sendmail logs status and error messages in the /var/log/mail* file (the file name depends on the distribution, see /etc/syslog.conf). If you experience problems with sendmail, you should check this file.

A particularly frequent problem is the message 'unqualified host name (localhost) unknown'. Subsequently sendmail goes for one minute before it resumes work. The cause of this problem is usually that localhost is used as the computer name. In this case, /etc/hosts looks like this one of the distributions (for example in SuSE):

```
# /etc/hosts: sendmail complains about unqualified host name
127.0.0.1 localhost
127.0.0.2 localhostdomain localhost
```

Although most programs can actually cope with this, to choose a different computer name (myhost, if the Unix-conformant solution is better). From this, you generate the following file /etc/hosts which sendmail can agree with too. (Of course, /etc/HOSTNAME must now contain the name myhost.)

```
# /etc/hosts: this will work (SUSE)
127.0.0.1       localhost
127.0.0.2       myhost.localdomain      myhost
```

The alternative is to continue using localhost as the computer name and in exchange the full computer name for localhost in /etc/hosts. (However, this is in breach of the full rule according to which localhost is considered to be fully qualified (without extension.) RedHat Linux is usually configured in this way the network has only been set up loop-back.

```
# /etc/hosts: and this works too (RedHat)
127.0.0.1       localhost.localdomain   Localhost
```

# Setting the sender's address

When you send mail via PPP/SLIP with Elm, Mail, or sendmail automatically inserts loginname@domainname as the sender's address. This is undesirable – the address cannot reply to this address, but you must use your address at your Internet provider (in this chapter example: hofer@provider.de).

A small change in /etc/sendmail.cf ensures, instead of the host and domain main names, sendmail uses a different sender. In the masquerade line, which begins with the letters DM, you specify the required sender's domain name. This causes sendmail to assemble the sender out of the login name, the @ character and the masquerade text.

```
# alternative modification in /etc/sendmail.cf
# specify fixed computer name
DMprovider.de
```

Neither setting affects pine! builds the sender field for itself. How pine can be told to indicate the specified sender has been described on page 351. In Netscape and kmail the tool is directly inserted by the program.

In general sendmail only sends emails and not news articles. The sender of news articles must also be set separately – see pages 376 and 380 for programs and tin.

# Calling Internet providers as relays

In its standard setting, sendmail@hostname looks after forwarding your messages. Normally, you can leave this task to your Internet provider. For this, sendmail that it is to deliver your mail only to the system (and not any further). This has essential advantage: even if you send a message to another country and the Internet connections are jammed, you can deliver your mail to your provider without delay and save costs.

The necessary change in sendmail.cf is again limited to one line: you must specify the address of your Internet provider's mail server in the line that begins with DS and is normally empty:

```
# modification in /etc/sendmail.cf
# "Smart" relay (may be null)
Provider.de
```

# Changing timeout settings

sendmail.cf contains a separate section in which various timeout settings can be specified. These settings control the behavior of sendmail if an email message cannot be delivered for a given period. Often these times have to be increased otherwise you will receive irritating messages from sendmail which inform you about undeliverable. If you write a message in the morning, but decide to send it only in the evening via PPP (because during the day you have no access to your provider or are aware that this message is undeliverable and do not require warning).

```
# modification in /etc/sendmail.cf
# after one day, the sender of undeliverable
# email message receives warning; sendmail
# still attempts to deliver
# 0.queuewarn=1d
# after five days, an undeliverable
# email message is returned to the sender
# 0.queuereturn=5d
```

The frequency with which sendmail attempts delivery of email is controlled by the start of sendmail with the option -q (for example -q1h for hourly delivery). In RedHat, starting is carried out via /etc/rc.d/init.d; in SuSE via /sbin/init.d.

# Creating your own sendmail.cf

sendmail.cf is built in such way that the file is normally not edited but by recompiling macro files. The advantage of this procedure is that the source files are more understandable and therefore easier to adapt than sendmail. itself. A precondition for the creation of completely new configuration files is the installation of sendmail configuration files (which are not included in all distributions) and the macro processor m4, whose function is better compared to that of a C compiler. Furthermore you need a lot of fundamental sendmail knowledge. The 'official' documentation is the 800-page sendmail published by O'Reilly.

The source files for sendmail.cf are usually located in the /usr/share/sendmail or /usr/src/sendmail directory. The subdirectory contains several ready-made configuration files from which you can generate a new sendmail.cf file with a call to m4. In the following instructions, instead of linux.smtp.mc, you can obviously specify any of the many other sample files contained in the cf directory.

```
root cd /usr/src/sendmail/cf
root m4 linux.smtp.mc > sendmail.cf
root mv /etc/sendmail.cf /etc/sendmail.cf.backup
root cp sendmail.cf /etc
```

During execution of m4, various configuration files from the directories detail, osype, and so on, are read and processed. A detailed description of this process and the meaning of the various settings can be found in the file /usr/src/sendmail/README.

# mailq

mailq or the equivalent command sendmail -bp displays a list of all mail messages which have been sent by a mail program, but which could not be forwarded (for example, because no Internet connection was available). Thus, mailq is a simple method for determining whether there are any unsent mails lying around.

# Sending local mail

You can also try email on your computer if you have no Internet connection. As the address, you simply enter the name of the addressee (for example hofer or root). In some programs (pine, Netscape) you must append @localhost as the addressee's name, for example rootlocalhost. The reason: some email programs automatically supplement the abbreviation root with @hostname.domainname, which is in itself correct but may cause problems to the local delivery via sendmail.

# Fetching mail via POP (fetchmail)

Sendmail forwards the mail you have written to your Internet provider, the fetchmail program has exactly the opposite task: it fetches mail addressed to you from your Internet provider and appends the messages to the local mail file in /var/spool/mail (Automatic delivery of mail to your computer is not possible, because the POP/SLIP connection cannot be kept continuously).

Communication between the Internet provider and fetchmail is based on the Post Office Protocol (in short POP). There are two variations of POP, namely POP2 and POP3. Some email programs (Netscape, gmail) can also be configured in such a way that they fetch mail from the reader via POP. The use of fetchmail, however, allows better automation of the process.

Instead of fetchmail it is also possible to use the older program popclient. This program works in a similar way, but is less easy to configure and is no longer maintained, fetchmail is the successor of popclient.

> NOTE
