
## More Information

- **Web**
    - **sendmail**: www.sendmail.org
    - exim4: www.exim.org, wiki.debian.org/Package:exim4
    - **procmail**: www.procmail.org
    - IMAP and POP3: www.dovecot.org, cyrusimap.org
    - SpamAssassin: spamassassin.apache.org, wiki.apache.org/spamassassin
    - Spam database: razor.sourceforge.net
    - Mailman: www.list.org
    - SquirrelMail: www.squirrelmail.org
    - Dovecot: www.dovecot.org
    - Postfix: www.postfix.org
    - Qmail: www.qmail.org

- **Local**
    - Dovecot: /usr/share/doc/dovecot*
    - man pages: **sendmail**, **aliases**, **makemail**, **spamassassin**, **spamc**, **spamd**
    - SpamAssassin: /usr/share/doc/spamassassin*. Give the following command:
      ```bash
      $ perl-doc Mail::SpamAssassin::Conf
      ```

# Setting Up a sendmail Mail Server

This section explains how to set up a **sendmail** mail server.

## Prerequisites

Install the following packages:

- **sendmail**
- **sendmail-cf** (required to configure **sendmail**)

Restart **sendmail**. As installed, **sendmail** is active and enabled so it will run when the system is booted. After changing its configuration files, give the following command to restart **sendmail**, causing it to reread its configuration files:

```bash
# systemctl restart sendmail.service
```

# NOTES

**Firewall** An SMTP server normally uses TCP port 25. If an SMTP server system that receives nonlocal mail is running a firewall, you need to open this port. Give the following commands to open the port each time the system boots (permanently) and on the running system; see page 906 for information on `firewall-cmd`.

```bash
$ su -c 'firewall-cmd --add-port=25/tcp'
$ su -c 'firewall-cmd --permanent --add-port=25/tcp'
```

**cyrus** This chapter covers the IMAP and POP3 servers included in the **dovecot** package. Fedora/RHEL also provides IMAP and POP3 servers in the **cyrus-imapd** package.

**FQDN** If the local system does not have an FQDN (page 1251), **sendmail** will start very slowly. As a consequence, the system might boot slowly. See /etc/hostname on page 507 for instructions on how to determine if the system has an FQDN and how to give the local system an FQDN.

# JUMPSTART I: CONFIGURING sendmail ON A CLIENT

> ### You might not need to configure sendmail to send email
>
> **tip**
> With **sendmail** running, give the command described under "Test" on page 744. As long as **sendmail** can connect to port 25 outbound, you should not need to set up **sendmail** to use an SMTP relay as described in this section. If you receive the mail sent by the test, you can skip this section.
> However, see “FQDN,” above.

This JumpStart configures an outbound **sendmail** server. This server

- Uses a remote SMTP server—typically an ISP—to relay outbound email to its destination (a smarthost or SMTP relay).
- Sends to the SMTP server email originating from the local system only. It does not forward email originating from other systems.
- Does not handle inbound email. As is frequently the case, you need to use POP or IMAP to receive email.

**Change sendmail.mc** To set up this server, you must edit /etc/mail/sendmail.mc and restart **sendmail** (page 742).

The dnl (page 749) at the start of the following line in **sendmail.mc** indicates that this line is a comment:

```text
dnl define(`SMART_HOST', `smtp.your.provider')dnl
```

You can ignore the dnl at the end of the line. To specify a remote SMTP server, you must open **sendmail.mc** in an editor and change the preceding line, deleting dnl from the beginning of the line and replacing **smtp.your.provider** with the FQDN of your ISP's SMTP server (obtain this name from your ISP). Be careful not to alter the back ticks (`) and the single quotation marks (') in this line. If your ISP's SMTP server is at smtp.mysip.com, you would change the line to:

```text
define(` SMART_HOST', `smtp.mysip.com')dnl
```

**Do not alter the back ticks (`) or the single quotation marks (')**

> **tip** Be careful not to alter the back ticks (`) or the single quotation marks (') in any line in **sendmail.mc**. These symbols control the way the **m4** preprocessor converts **sendmail.mc** to **sendmail.cf**. **sendmail** will not work properly if you do not preserve these symbols.

Restart **sendmail** so that it regenerates the **sendmail.cf** file from the **sendmail.mc** file you edited (page 742).

**Test** Test **sendmail** with the following command:

```bash
$ echo "my sendmail test" | /usr/sbin/sendmail user@remote.host
```

Replace *user@remote.host* with an email address on *another system* where you receive email. You need to send email to a remote system to make sure that **sendmail** is relaying your email.

# JUMPSTART II: CONFIGURING sendmail ON A SERVER

If you want to receive inbound email sent to a registered domain that you own, you need to set up **sendmail** as an incoming mail server. This JumpStart describes how to set up such a server. This server

- Accepts outbound email from the local system only.
- Delivers outbound email directly to the recipient's system, without using an SMTP relay (smarthost).
- Accepts inbound email from any system.

This server does not relay outbound email originating on other systems. Refer to "*access: Sets Up a Relay Host*" on page 752 if you want the local system to act as a relay. For this configuration to work, you must be able to make outbound connections from and receive inbound connections to port 25.

The line in **sendmail.mc** that limits **sendmail** to accepting inbound email from the local system only is:

```text
DAEMON_OPTIONS(` Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```

To allow **sendmail** to accept inbound email from other systems, remove the parameter *Addr=127.0.0.1*, from the preceding line:

```text
DAEMON_OPTIONS(` Port=smtp, Name=MTA')dnl
```

By default, **sendmail** does not use a remote SMTP server to relay email, so there is nothing to change to cause **sendmail** to send email directly to recipients' systems. [JumpStart I set up a SMART_HOST to relay email.]

Once you have restarted **sendmail** (page 742), it will accept mail addressed to the local system, as long as a DNS MX record (page 859) points at the local system. If you are not running a DNS server, you must ask your ISP to set up an MX record.

# WORKING WITH sendmail MESSAGES

When you send email, the MUA passes the email to **sendmail**, which creates in the /var/spool/mqueue (mail queue) directory two files that hold the message while **sendmail** processes it. To create a unique filename for a particular piece of email, **sendmail** generates a random string and uses that string in filenames pertaining to the email. The **sendmail** daemon stores the body of the message in a file named df (data file) followed by the generated string. It stores the headers and envelope information in a file named qf (queue file) followed by the generated string.

If a delivery error occurs, **sendmail** creates a temporary copy of the message that it stores in a file whose name starts with tf (temporary file) and logs errors in a file whose name starts with xf. Once an email has been sent successfully, **sendmail** removes all files pertaining to that email from the mqueue directory.

By default, **sendmail** delivers email addressed to the local system to users' files in the mail spool directory, /var/spool/mail/, in mbox format. Within this directory, each user has a mail file named with the user's username. Mail remains in these files until it is collected, typically by an MUA. Once an MUA collects the mail from the mail spool, the MUA stores the mail as directed by the user, usually in the user's home directory.

The scheme that **sendmail** uses to process email addressed to a nonlocal system depends on how it is configured: It can send the email to a smarthost, it can send the email to the system pointed to by the DNS MX record of the domain the email is addressed to, or it can refuse to send the email.

The mbox format holds all messages for a user in a single file. To prevent corruption, a process must lock this file while it is adding messages to or deleting messages from the file; thus the MUA cannot delete a message at the same time the MTA is adding messages. A competing format, maildir, holds each message in a separate file. This format does not use locks, allowing an MUA to delete messages from a user at the same time as mail is delivered to the same user. In addition, the maildir format is better able to handle larger mailboxes. The downside is that the maildir format adds overhead when you are using a protocol such as IMAP to check messages. The dovecot package supports both mbox and maildir formats. Qmail (page 742), an alternative to **sendmail**, supports the maildir format only.
