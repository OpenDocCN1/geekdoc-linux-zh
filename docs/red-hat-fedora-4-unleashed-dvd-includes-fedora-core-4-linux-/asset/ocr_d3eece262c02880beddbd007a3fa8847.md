for you and then you log in to pick it up once in awhile? (Most users who are not setting up servers will be in this situation.) In this case, you cannot easily receive email using SMTP, and you need to use a protocol, such as POP3 or IMAP, instead.

> Remember when we said that some mail clients can include some MTA functionality? MS Outlook and Outlook Express can be configured to use SMTP and, if you use a dial-up connection, will offer to start the connection and then use SMTP to send your mail, so a type of MTA functionality is included in those mail clients.

Unfortunately, many MUs do not know anything about POP3 or IMAP. To eliminate that problem, you can use a program called Fetchmail to contact mail servers using POP3 or IMAP, download mail off the servers, and then inject those messages into the local MTA just as if they had come from a standard SMTP server. The following sections explain how to install, configure, and use the Fetchmail program.

# ### Installing Fetchmail

Similar to other `.rpm files, Fetchmail can be installed with the `rpm` `-i` command. This command will install all files to their default locations. If, for whatever reason, you need to perform a custom installation, see Chapter 7, "Managing Software and System Resources," for more information on changing the default options for `rpm`.

You can get the latest version of Fetchmail at http://tuxedo.org/~esr/fetchmail. It is available in both source and RPM binary formats. The version of Fedora on the CDs and DVD accompanying this book provides a reasonably current version of Fetchmail and installs useful Fetchmail documentation in the `/usr/share/doc/fetchmail` directory. That directory includes an FAQ, features list, and Install documentation.

# ### Configuring Fetchmail

After you have installed Fetchmail, you must create the file `.fetchmailrc` in your home directory, which provides the configuration for the Fetchmail program.

There are two ways to create the `.fetchmailrc` file. The first is by simply creating and editing the file by hand with any text editor. The second is by using the graphical `fetchmailconf` program. The configuration file is straightforward and quite easy to create; the following sections explain the manual method for creating and editing the file. The information presented in the following sections does not discuss all the options available in the `.fetchmailrc` file, but covers the most common ones needed to get a basic Fetchmail installation up and running. You'll need to use a text editor to create the file to include entries like the ones shown as examples—modified for your personal information, of course. For advanced configuration, see the man page for Fetchmail. The man page is well written and documents all the configuration options in detail.