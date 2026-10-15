
+   f. Consider the pipe as a filter.
+   w. Wait for the filter or program to finish and check its exitcode (normally ignored); if the filter is unsuccessful, then the text will not have been filtered.

+   Make sure that you activate Procmail in /etc/postfix/main.cf:

```
mailbox_command = /usr/bin/procmail
```

+   Make sure that your smtpd definition in the file /etc/postfix/master.cf is set to default

```
smtp inet n - n - - smtpd
```

After this, start spamd by entering

rcspam start

Spam can be filtered from the mail client or in a further Procmail configuration (~/.procmailrc) by adding lines similar to this:

```
:0
* ^X-Spam-Status: Yes
$MAILDIR/Spam
```

## Test SpamAssassin

You can use telnet to test your configuration. You also can send a spam email directly using the sendmail command:

```
cat sample-spam.txt | /usr/sbin/sendmail geeko@digitalairlines.com
```

## Objective 3

## Use a Virus Scanner for Email

Communication via email is very important for companies and individuals today, but email can be infected by virus software.

Most of the viruses attack Windows clients, but the mail server of a company is often a Linux or UNIX machine. To avoid damage we recommend to search for viruses before the infected mail arrives at the user’s client.

SUSE Linux Enterprise Server 10 provides tools to detect viruses in email on your mail server.

In this objective, the following tools are introduced:

- AVMailGate
- AMaViSd-new

## AVMailGate

AVMailGate is the abbreviation for AntiVir MailGate, an antivirus mail filter from H+BEDV Datentechnik GmbH (http://www.hbedv.com).

AVMailGate updates the virus definition file and the engine itself.

This topic describes the following:

- AVMailGate Architecture
- Install AVMailGate
- Configure AVMailGate
- Understand the AVMailGate Configuration Files
- Update AVMailGate

### AVMailGate Architecture

### Figure 12-1

![](img/8279afe915b153902294b0e58311b75a_272_0.png)

AVMailGate is composed of three queues and two kinds of processes:

- **Queues** (located in `/var/spool/avmailgate/`)
  - **incoming/**. The input queue for all incoming email.
  - **rejected/**. The queue where possible infected email are stored.
  - **outgoing/**. The output queue for not infected email.
- **Processes**
  - **avgated**. The smtpd receiver that stores incoming email in the input queue. (daemon)
  - **avgatefwd**. Virus-scanning function and SMTP forwarder and sendmail invoker. (daemon)

Both processes can be configured by editing the file
`/etc/avmailgate.conf`.

This file includes comments that describe the possible settings.

For a description of all options, see /usr/share/packages/avmailgate/doc/MANUAL.

## Install AVMailGate

To install AVMailGate, select the package avmailgate.

A startscript is available in rcavgate to start and stop AVMailGate.

To start AVMailGate at the system’s start, enter insserv avgate.

## Configure AVMailGate

There are two possibilities to use AVMailGate with Postfix:

- AVMailGate Waits for Mails on Port 25 and Forwards Them to Postfix
- AVMailGate Is Used from Postfix as Content Filter

### AVMailGate Waits for Mails on Port 25 and Forwards Them to Postfix

To use AVMailGate as mail proxy that waits for mails on port 25 you simply have to avoid that Postfix listens on this port. Therefore mark the following line in /etc/postfix/master.cf: as command by adding a hash (“#”) in front

```
#smtp inet n - n - - smtpd
```

Then restart Postfix.

### AVMailGate Is Used from Postfix as Content Filter

The best way to use AVMailGate with Postfix is to use the Full Content Filter API (see FILTER_README in the Postfix package for details).

It waits for SMTP connections on port 10024 and sends scanned email messages or virus warnings out per SMTP on port 10025.

To integrate AVMailGate as a filter in Postfix, do the following:

1. Edit /etc/postfix/master.cf and uncomment –if applicable– or add the following line:

```
localhost:10025 inet n - y - - smtpd -o content_filter=
```

2. Edit /etc/postfix/main.cf and add the following line:

```
content_filter = smtp:127.0.0.1:10024
```

3. Since AVMailGate listens on port 10024, not port 25, edit /etc/avmailgate.conf and set

```
ListenAddress localhost port 10024
```

4. You have to tell AVMailGate it should send email back to Postfix via SMTP on host localhost via port 10025. Edit /etc/avmailgate.conf and set

```
ForwardTo SMTP: localhost port 10025
```

5. Since AVMailGate sends out notification messages as AVMailGate, set an alias in /etc/aliases:

```
vmailgate: root
```
