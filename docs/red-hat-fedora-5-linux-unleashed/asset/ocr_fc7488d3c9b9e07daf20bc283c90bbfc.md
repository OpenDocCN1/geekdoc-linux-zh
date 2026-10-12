see whether it meets your needs. If not, investigate one of the following MDAs provided by Fedora.

Unless otherwise noted, all the MDA software is provided with the Fedora disc. Chapter 7 details the general installation of any software.

# Procmail

As a tool for advanced users, the Procmail application acts as a filter for email as it is retrieved from a mail server. It uses *rule sets* (known as *recipes*) as it reads each email message. No default configuration is provided; you must manually create a `~/.procmail` file for each user, or each user can create her own.

There is no systemwide default configuration file. The creation of the rule sets is not trivial and requires an understanding of the use of regular expressions that is beyond the scope of this chapter. Fedora does provide three examples of the files in `/usr/share/doc/procmail/examples`, as well as a fully commented example in the `/usr/share/doc/procmail` directory, which also contains a `README` and `FAQ`. Details for the rule sets can be found in the man page for Procmail as well as the man pages for `procmaile`, `procmailrc`, and `procmailex`, which contain examples of Procmail recipes.

# Spamassassin

If you have used email for any length of time, you have likely been subjected to *spam*—unwanted email that is sent to thousands of people at the same time. Fedora provides an MDA named Spamassassin to assist you in reducing and eliminating unwanted emails. Easily integrated with Procmail and Sendmail, it can be configured for both systemwide and individual use. It employs a combination of rule sets and *black lists* (Internet domains known to mail spam).

Enabling Spamassassin is simple. You must first have installed and configured Procmail. The `README` file found in `/usr/share/doc/spamassassin` provides details on configuring the `.procmail` file to process mail through Spamassassin. It tags probable spam with a unique header; you can then have Procmail filter the mail in any manner you choose. One interesting use of Spamassassin is to use it to tag email received at special email accounts established solely for the purpose of attracting spam. This information is then shared with the Spamassassin site where these “spam trap”-generated hits help the authors fine-tune the rule sets.

# Squirrelmail

Perhaps you do not want to read your mail in an MUA. If you use your web browser often, it might make sense to read and send your mail via a web interface, such as the one used by Hotmail or Yahoo! mail. Fedora provides Squirrelmail for just that purpose. Squirrelmail is written in the PHP 4 language and supports IMAP and SMTP with all pages rendering in HTML 4.0 without using Java. It supports MIME attachments, as well as an address book and folders for segregating email.