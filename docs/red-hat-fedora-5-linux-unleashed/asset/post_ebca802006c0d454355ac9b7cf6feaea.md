
set daemon 600
set postmaster foobar
set logfile ../fetchmail.log

The first line in this example tells fetchmail that it should start in daemon mode and check the mail servers for new mail every 600 seconds, or 10 minutes. Daemon mode means that after fetchmail starts, it moves itself into the background and continues running. Without this line, fetchmail would check for mail once when it started and would then terminate and never check again.

The second option tells fetchmail to use the local account foobar as a last resort address. In other words, any email that it receives and cannot deliver to a specified account should be sent to foobar.

The third line tells fetchmail to log its activity to the file ../fetchmail.log. Alternatively, you can use the line `set syslog`, in which case, fetchmail logs through the syslog facility.

## Configuring Mail Server Options

The second section of the `.fetchmailrc` file contains information on each of the mail servers that should be checked for new mail. Here is an example of what the mail section might look like:

poll mail.samplet.org
proto pop3
no dns

The first line tells fetchmail that it should check the mail server `mail.samplet.org` at each poll interval that was set in the global options section (which was 600 seconds in our example). Alternatively, the first line can begin with `skip`. If a mail server line begins with `skip,` it is not polled at the poll interval, but is polled only when it is specifically specified on the fetchmail command line.

The second line specifies the protocol that should be used when contacting the mail server. In this case, we are using the POP3 protocol. Other legal options are IMAP, APOP, and KPOP. You can also use AUTO here—in which case, fetchmail attempts to automatically determine the correct protocol to use with the mail server.

The third line tells fetchmail that it should not attempt to do a DNS lookup. You probably want to include this option if you are running over a dial-up connection.

## Configuring User Accounts

The third and final section of `.fetchmailrc` contains information about the user account on the server specified in the previous section. Here is an example:

user foobar
pass secretword
fetchall
flush

The first line, of course, simply specifies the username that is used to log in to the email server, and the second line specifies the password for that user. Many security conscious people cringe at the thought of putting clear-text passwords in a configuration file, and they should if it is group or world-readable. The only protection for this information is to make certain that the file is readable only by the owner; that is, with file permissions of `600`.

The third line tells Fetchmail that it should fetch all messages from the server, even if they have already been read.

The fourth line tells Fetchmail that it should delete the messages from the mail server after it has completed downloading them. This is the default, so we would not really have to specify this option. If you wanted to leave the messages on the server after downloading them, use the option `no flush`.

The configuration options you just inserted configured the entire `.fetchmailrc` file to look like this:

set daemon 600
set postmaster foobar
set logfile ../fetchmail.log

poll mail.siplenel.org
proto pop3
no dns

user foobar
pass secretword
fetchall
flush

What this file tells Fetchmail to do is:

- Check the POP3 server `mail.siplenel.org` for new mail every 600 seconds
- Log in using the username `foobar` and the password `secretword`
- Download all messages off the server
- Delete the messages from the server after it has finished downloading them
- Send any mail it receives that cannot be delivered to a local user to the account `foobar`

As mentioned earlier, many more options can be included in the `.fetchmailrc` file than are listed here. However, these options get you up and running with a basic configuration.

For additional flexibility, you can define multiple `.fetchmailrc` files in order to retrieve mail from different remote mail servers while using the same Linux user account. For example, you can define settings for your most often used account and save them in the default `.fetchmailrc` file. Mail can then quickly be retrieved like so:

$ fetchmail -a
1 message for dball at mail.myserver.com (1108 octets).
reading message 1 of 1 (1108 octets). flushed

By using fetchmail's -f option, you can specify an alternative resource file and then easily retrieve mail from another server like this:

$ fetchmail -f .myothermailrc
2 messages for dball at othermail.othserver.org (5407 octets).
reading message 1 of 2 (3440 octets) ... flushed
reading message 2 of 2 (1967 octets) . flushed
You have new mail in /var/spool/mail/dball

By using the -d option, along with a time interval (in seconds), you can use fetchmail in its daemon, or background, mode. The command launches as a background process and retrieves mail from a designated remote server at a specified interval. For more advanced options, see the fetchmail man page, which is very well written and documents all options in detail.

![](img/2045828cf45e5632bf056f9ca99d6755_719_0.png)

## Choosing a Mail Delivery Agent

Because of the modular nature of mail handling, it is possible to use multiple applications to process mail and accomplish more than simply deliver it. Getting mail from the storage area and displaying it to the user is the purpose of the mail delivery agent (MDA). MDA functionality can be found in some of the mail clients (MUAs), which can cause some confusion to those still unfamiliar with the concept of UNIX mail. As an example, the Procmail MDA provides filtering based on rule sets; KMail and Evolution, both MUAs, provide filtering, but the MUAs pine, mutt, and Balsa do not. Some MDAs perform simple sorting, and other MDAs are designed to eliminate unwanted emails, such as spam and viruses.

You would choose an MDA based on what you want to do with your mail. We will look at five MDAs that offer functions you might find useful in your particular situation. If you have simple needs (just organizing mail by rules), one of the MUAs that offers filtering might be better for your needs. Fedora provides the Evolution MUA as the default selection (and it contains some MDA functionality as previously noted), so try that first and see whether it meets your needs. If not, investigate one of the following MDAs provided by Fedora.

Unless otherwise noted, all the MDA software is provided with the Fedora disc. Chapter 7 details the general installation of any software.

### Procmail

As a tool for advanced users, the Procmail application acts as a filter for email as it is retrieved from a mail server. It uses *rule sets* (known as *recipes*) as it reads each email message. No default configuration is provided; you must manually create a `~/.procmail` file for each user, or each user can create her own.

There is no systemwide default configuration file. The creation of the rule sets is not trivial and requires an understanding of the use of regular expressions that is beyond the scope of this chapter. Fedora does provide three examples of the files in `/usr/share/doc/procmail/examples`, as well as a fully commented example in the `/usr/share/doc/procmail` directory, which also contains a `README` and `FAQ`. Details for the rule sets can be found in the man page for Procmail as well as the man pages for `procmailrc` (corrected from OCR error `procmaile`), `procmailrc`, and `procmailex`, which contain examples of Procmail recipes.

### Spamassassin

If you have used email for any length of time, you have likely been subjected to *spam*—unwanted email that is sent to thousands of people at the same time. Fedora provides an MDA named Spamassassin to assist you in reducing and eliminating unwanted emails. Easily integrated with Procmail and Sendmail, it can be configured for both systemwide and individual use. It employs a combination of rule sets and *black lists* (Internet domains known to mail spam).

Enabling Spamassassin is simple. You must first have installed and configured Procmail. The `README` file found in `/usr/share/doc/spamassassin` provides details on configuring the `.procmail` file to process mail through Spamassassin. It tags probable spam with a unique header; you can then have Procmail filter the mail in any manner you choose. One interesting use of Spamassassin is to use it to tag email received at special email accounts established solely for the purpose of attracting spam. This information is then shared with the Spamassassin site where these “spam trap”-generated hits help the authors fine-tune the rule sets.

### Squirrelmail

Perhaps you do not want to read your mail in an MUA. If you use your web browser often, it might make sense to read and send your mail via a web interface, such as the one used by Hotmail or Yahoo! mail. Fedora provides Squirrelmail for just that purpose. Squirrelmail is written in the PHP 4 language and supports IMAP and SMTP with all pages rendering in HTML 4.0 without using Java. It supports MIME attachments, as well as an address book and folders for segregating email.
