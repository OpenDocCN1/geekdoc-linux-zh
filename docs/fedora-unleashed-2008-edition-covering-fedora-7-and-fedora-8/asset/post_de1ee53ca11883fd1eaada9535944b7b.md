
## Configuring User Accounts

The third and final section of .fetchmailrc contains information about the user account on the server specified in the previous section. Here is an example:

```
user foobar
pass secretword
fetchall
flush
```

The first line, of course, is simply just the username that is used to log in to the email server, and the second line specifies the password for that user. Many security-conscious people cringe at the thought of putting clear-text passwords in a configuration file, and they should if it is group or world-readable. The only protection for this information is to make certain that the file is readable only by the owner; that is, with file permissions of 600.

The third line tells Fetchmail that it should fetch all messages from the server, even if they have already been read.

The fourth line tells Fetchmail that it should delete the messages from the mail server after it has completed downloading them. This is the default, so you do not really have to specify this option. If you want to leave the messages on the server after downloading them, use the option `no flush`.

The configuration options you just inserted configured the entire .fetchmailrc file to look like this:

```
set daemon 600
set postmaster foobar
set logfile ./.fetchmail.log

poll mail.sompenet.org
proto pop3
no dns

user foobar
pass secretword
fetchall
flush
```

What this file tells Fetchmail to do is:

- Check the POP3 server `mail.samplingnet.org` for new mail every 600 seconds.
- Log in using the username `foobar` and the password `secretword`.
- Download all messages off the server.
- Delete the messages from the server after Fetchmail has finished downloading them.
- Send any mail Fetchmail receives that cannot be delivered to a local user to the account `foobar`.

As mentioned earlier, many more options can be included in the `.fetchmailrc` file than are listed here. However, these options get you up and running with a basic configuration.

For additional flexibility, you can define multiple `.fetchmailrc` files to retrieve mail from different remote mail servers while using the same Linux user account. For example, you can define settings for your most often-used account and save them in the default `.fetchmailrc` file. Mail can then quickly be retrieved like so:

```
$ fetchmail -a
1 message for ahudson at mail.myserver.com (1108 octets).
reading message 1 of 1 (1108 octets). flushed
```

By using Fetchmail’s `-f` option, you can specify an alternative resource file and then easily retrieve mail from another server, as follows:

```
$ fetchmail -f .myothermailrc
2 messages for bball at othermail.otherverser.org (5407 octets).
reading message 1 of 2 (3440 octets). flushed
reading message 2 of 2 (1967 octets). flushed
You have new mail in /var/spool/mail/bball
```

By using the `-d` option, along with a time interval (in seconds), you can use Fetchmail in its daemon—or background—mode. The command launches as a background process and retrieves mail from a designated remote server at a specified interval. For more advanced options, see the Fetchmail man page, which is well written and documents all options in detail.

> **CAUTION**  
> Because the `.fetchmailrc` file contains your mail server password, it should be readable only by you. This means that it should be owned by you and should have permissions no greater than 600. Fetchmail complains and refuses to start if the `.fetchmailrc` file has permissions greater than this.

## Choosing a Mail Delivery Agent

Because of the modular nature of mail handling, it is possible to use multiple applications to process mail and accomplish more than simply delivering it. Getting mail from the storage area and displaying it to the user is the purpose of the mail delivery agent (MDA). MDA functionality can be found in some of the mail clients (MUAs), which can cause some confusion to those still unfamiliar with the concept of UNIX mail. As an example, the Procmail MDA provides filtering based on rulesets; KMail and Evolution, both MUAs, provide filtering, but the MUAs pine, mutt, and Balsa do not. Some MDAs perform simple sorting, and other MDAs are designed to eliminate unwanted emails, such as spam and viruses.

You would choose an MDA based on what you want to do with your mail. The following sections look at five MDAs that offer functions you might find useful in your particular situation. If you have simple needs (just organizing mail by rules), one of the MUAs that offers filtering might be better for your needs. Fedora provides the Evolution MUA as the default selection (and it contains some MDA functionality as previously noted), so try that first and see whether it meets your needs. If not, investigate one of the following MDAs provided by Fedora.

Unless otherwise noted, all the MDA software is provided with the Fedora discs. Chapter 34 details the general installation of any software.

### Procmail

As a tool for advanced users, the Procmail application acts as a filter for email as it is retrieved from a mail server. It uses rulesets (known as recipes) as it reads each email message. No default configuration is provided; you must manually create a `.procmailrc` file for each user, or each user can create her own.

There is no systemwide default configuration file. The creation of the rulesets is not trivial and requires an understanding of the use of regular expressions that is beyond the scope of this chapter. Fedora does provide three examples of the files in `/usr/share/doc/procmail/examples`, as well as a fully commented example in the `/usr/share/doc/procmail` directory, which also contains a Read Me and FAQ. Details for the rulesets can be found in the man page for Procmail, as well as the man pages for `procmailrc`, `procmailrc`, and `procmaillex`, which contain examples of Procmail recipes.

### Spamassassin

If you have used email for any length of time, you have likely been subjected to spam—unwanted email that is sent to thousands of people at the same time. Fedora provides an MDA named Spamassassin to assist you in reducing and eliminating unwanted emails. Easily integrated with Procmail and Sendmail, it can be configured for both systemwide and individual use. It employs a combination of rulesets and blacklists (Internet domains known to mail spam).

Enabling Spamassassin is simple. You must first have installed and configured Procmail. The *Read Me* file found in `/usr/share/doc/spamassassin` provides details on configuring the `.procmail` file to process mail through Spamassassin. It tags probable spam with a unique header; you can then have Procmail filter the mail in any manner you choose. One interesting use of Spamassassin is to use it to tag email received at special email accounts established solely for the purpose of attracting spam. This information is then shared with the Spamassassin site, where these “spam trap”-generated hits help the authors fine-tune the rulesets.

### Squirrelmail

Perhaps you do not want to read your mail in an MUA. If you use your web browser often, it might make sense to read and send your mail via a web interface, such as the one used by Hotmail or Yahoo! Mail. Fedora provides Squirrelmail for just that purpose. Squirrelmail is written in the PHP 4 language and supports IMAP and SMTP, with all pages rendering in HTML 4.0 without using Java. It supports MIME attachments, as well as an address book and folders for segregating email.

You must configure your web server to work with PHP 4. Detailed installation instructions can be found in `/usr/share/doc/squirrelmail/INSTALL`. After it is configured, point your web browser to `http://www.yourdomain.com/squirrelmail/` to read and send email.

### Virus Scanners

Although the currently held belief is that Linux is immune to email viruses targeted at Microsoft Outlook users, it certainly makes no sense for UNIX mail servers to permit infected email to be sent through them. Although Fedora does not provide a virus scanner, one of the more popular of many such scanners is MailScanner, available from `http://www.eng.scs.mot.com/mailscanner/`; a Fedora RPM package is available as well as the source code. It supports Sendmail and Exim, but not Postfix or Qmail. Searching on the terms “*virus*” and “*email*” at Freshmeat.net will turn up a surprising list of GPLed virus scanners that might serve your needs.

### Special Mail Delivery Agents

If you already use Hotmail or another web-based email account, the currently available MUAs are not useful to you: Formal POP3 access to a Hotmail account is not available free of charge. However, Microsoft Outlook Express can access Hotmail at no charge, using a special protocol called `HTTPMail`. How that is done is covered in RFC 2518 as “WebDAV extensions to HTTP/1.1.” No specific solution is provided by Fedora, but the basic tools it provides are adequate when supplemented by some clever Perl programming.

Hotwayd is available from `http://sourceforge.net/projects/hotwayd/` and implements this functionality, allowing you to use your favorite mail client to read mail from Hotmail.

A newer Hotmail access tool is Gotmail from `http://sourceforge.net/projects/gotmail/`. It is a Perl script that is easy to configure. There are brief tutorials on configuring it for use with KMail and Evolution at `http://www.madpenguin.org/cms/?m=show&id=437`.
