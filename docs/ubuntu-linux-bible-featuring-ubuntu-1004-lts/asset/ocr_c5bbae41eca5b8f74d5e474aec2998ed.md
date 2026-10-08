# Integrating MailScanner, SpamAssassin, and
ClamAV with Postfix

MailScanner is a fast, powerful tool that scans incoming mail for spam and can optionally
configured to scan incoming mail for viruses. The Ubuntu MailScanner package requires
that the SpamAssassin package (discussed in the section of Chapter 7 entitled "Automatically
Checking for Junk Mail") be installed on your system so that it can invoke the SpamAssassin
package after performing its own spam checks, to maximize the chances that it will catch and
flag incoming spam.

# Note

The MailScanner package always claims that it is scanning for viruses even if it is not. This is because con-iguration file contains a setting for the virus scanner you want to use, which by default is to none.
Don't worry; I'll explain how to fix it.

I suggested that you install MailScanner and the ClamAV virus-scanning package in the section
of this chapter entitled "Installing Postfix and Friends." If you didn't, please go back and see that
section for information on how to install these packages.

Once installed, it is remarkably easy to add MailScanner to the Postfix food chain:

+   Add the following line to the end of your Postfix main.cf configuration file (/etc/
postfix/main.cf):

```
header_checks = regexp:/etc/postfix/header_checks
```

+   Use your favorite text editor to create the file /etc/postfix/header_checks with the
following contents:

```
^Received:/ / HOLD
```

This line tells Postfix to scan every incoming message for instances of the string
"Received:" at the beginning of a line and to not any matching messages (which
are all of them) to a HOLD queue. The HOLD queue is a temporary staging area that
you'll be scanning the incoming mail. Save this file and proceed to the next step.

+   Using your favorite text editor, bring up the MailScanner configuration file (/etc/
MailScanner/MailScanner.conf) so that you can configure MailScanner to work
correctly with Postfix as installed on your Ubuntu system. (By default, the Ubuntu
MailScanner package is configured as it would be on a Debian system and is therefore
configured for use with the exim mail server.)

+   Find the Run As User entries, remove the hash mark at the beginning of the line
s Run As User = postfix, and make sure there is a hash mark at the beginning