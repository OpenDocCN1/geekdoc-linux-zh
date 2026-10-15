
## CAUTION

Reading email as root is a security hazard: a malicious email message can exploit an email client and cause it to execute arbitrary code as the user running the client. To avoid this danger, you can forward all of root's mail to another account and read it from there. You can choose one of two ways for doing this.

You can add an entry to the /etc/aliases file that sends root's mail to a different account. For example, root: foobar would forward all mail intended for root to the account foobar.

The other way is to create a file named .forward in root's home directory that contains the address that the mail should forward to.

Anytime you make a change to the /etc/aliases file, you will need to rebuild the aliases database before that change will take effect. This is done with the following:

```
$ sudo newaliases
```

## Using Fetchmail to Retrieve Mail

SMTP is designed to work with systems that have a full-time connection to the Internet. What if you are on a dial-up account? What if you have another system store your email for you and then you log in to pick it up once in awhile? (Most users who are not setting up servers will be in this situation.) In this case, you cannot easily receive email using SMTP, and you need to use a protocol, such as POP3 or IMAP, instead.

## NOTE

Remember when we said that some mail clients can include some MTA functionality? Microsoft Outlook and Outlook Express can be configured to use SMTP and, if you use a dial-up connection, will offer to start the connection and then use SMTP to send your mail, so a type of MTA functionality is included in those mail clients.

Unfortunately, many MUAs do not know anything about POP3 or IMAP. To eliminate that problem, you can use a program called Fetchmail to contact mail servers using POP3 or IMAP, download mail off the servers, and then inject those messages into the local MTA just as if they had come from a standard SMTP server. The following sections explain how to install, configure, and use the Fetchmail program.

## Installing Fetchmail

Similar to other packages, Fetchmail can be installed using either synaptic or apt-get.

You can get the latest version of Fetchmail at http://www.catb.org/~esr/fetchmail.

## Configuring Fetchmail

After you have installed Fetchmail, you must create the file .fetchmailrc in your home directory, which provides the configuration for the Fetchmail program.

You can create and subsequently edit the .fetchmailrc file by using any text editor. The configuration file is straightforward and quite easy to create; the following sections explain the manual method for creating and editing the file. The information presented in the following sections does not discuss all the options available in the .fetchmailrc file, but covers the most common ones needed to get a basic Fetchmail installation up and running. You must use a text editor to create the file to include entries like the ones shown as examples—modified for your personal information, of course. For advanced configuration, see the man page for Fetchmail. The man page is well written and documents all the configuration options in detail.

## CAUTION

The .fetchmailrc file is divided into three different sections: global options, mail server options, and user options. It is important that these sections appear in the order listed. Do not add options to the wrong section. Putting options in the wrong place is one of the most common problems that new users make with Fetchmail configuration files.

## Configuring Global Options

The first section of .fetchmailrc contains the global options. These options affect all the mail servers and user accounts that you list later in the configuration file. Some of these global options can be overridden with local configuration options, as you learn later in this section. Here is an example of the options that might appear in the global section of the .fetchmailrc file:

```
set daemon 600
set postmaster foobar
set logfile ./fetchmail.log
```

The first line in this example tells Fetchmail that it should start in daemon mode and check the mail servers for new mail every 600 seconds, or 10 minutes. Daemon mode means that after Fetchmail starts, it will move itself into the background and continue running. Without this line, Fetchmail would check for mail once when it started and would then terminate and never check again.

The second option tells Fetchmail to use the local account foobar as a last-resort address. In other words, any email that it receives and cannot deliver to a specified account should be sent to foobar.
