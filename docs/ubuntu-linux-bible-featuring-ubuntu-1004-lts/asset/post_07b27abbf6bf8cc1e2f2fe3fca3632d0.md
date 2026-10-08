
# Integrating MailScanner, SpamAssassin, and ClamAV with Postfix

MailScanner is a fast, powerful tool that scans incoming mail for spam and can optionally be configured to scan incoming mail for viruses. The Ubuntu MailScanner package requires that the SpamAssassin package (discussed in the section of Chapter 7 entitled "Automatically Checking for Junk Mail") be installed on your system so that it can invoke the SpamAssassin package after performing its own spam checks, to maximize the chances that it will catch and flag incoming spam.

# Note

The MailScanner package always claims that it is scanning for viruses even if it is not. This is because the configuration file contains a setting for the virus scanner you want to use, which by default is to none. Don't worry; I'll explain how to fix it.

I suggested that you install MailScanner and the ClamAV virus-scanning package in the section of this chapter entitled "Installing Postfix and Friends." If you didn't, please go back and see that section for information on how to install these packages.

Once installed, it is remarkably easy to add MailScanner to the Postfix food chain:

- Add the following line to the end of your Postfix main.cf configuration file (/etc/postfix/main.cf):

```
header_checks = regexp:/etc/postfix/header_checks
```

- Use your favorite text editor to create the file /etc/postfix/header_checks with the following contents:

```
^Received:/ / HOLD
```

This line tells Postfix to scan every incoming message for instances of the string "Received:" at the beginning of a line and to not deliver any matching messages (which are all of them) to a HOLD queue. The HOLD queue is a temporary staging area that you'll be scanning the incoming mail. Save this file and proceed to the next step.

- Using your favorite text editor, bring up the MailScanner configuration file (/etc/MailScanner/MailScanner.conf) so that you can configure MailScanner to work correctly with Postfix as installed on your Ubuntu system. (By default, the Ubuntu MailScanner package is configured as it would be on a Debian system and is therefore configured for use with the exim mail server.)

- Find the Run As User entries, remove the hash mark at the beginning of the line `Run As User = postfix`, and make sure there is a hash mark at the beginning of any other line that begins with Run As User. These entries should now look something like the following:

```
# Run As User = mail
Run As User = postfix
# Run As User = Debian-exim-
```

- Find the Run As Group entries, remove the hash mark at the beginning of the line that says `Run As Group = postfix`, and make sure that there is a hash mark at the beginning of any other line that begins with Run As Group. These entries should now look something like the following:

```
# Run As Group = mail
Run As Group = postfix
# Run As Group = Debian-exim
```

- Find the Incoming Queue Dir entry and change its value to /var/spool/postfix/hold. This entry should now look like the following:

```
Incoming Queue Dir = /var/spool/postfix/hold
```

- Find the Outgoing Queue Dir entry and change its value to /var/spool/postfix/incoming. This entry should now look like the following:

```
Outgoing Queue Dir = /var/spool/postfix/incoming
```

- Find the MTA entry and change its value to postfix. This entry should now look like the following:

```
MTA = postfix
```

- Find the Virus Scanners entry and set its value to clamav. This entry should now look like the following:

```
Virus Scanners = clamav
```

- Save the /etc/MailScanner/MailScanner.conf file, and proceed to the next step.

- Use the following commands to ensure that the Postfix user and group own MailScanner's working directory and the directory where it stores (quarantines) files that are suspected of containing viruses, so that the Postfix mail server can write to these directories:

```
sudo chown -R postfix:postfix /var/spool/MailScanner
```

# Part III: Ubuntu for System Administrators

12. Using your favorite text editor, modify the file /etc/default/mailscanner and remove the hash mark at the beginning of the line containing the `run_mailscanner` variable. This line should look like the following:

```
run_mailscanner=1
```

Enabling this variable will cause your system to automatically start MailScanner the next time you boot your system. Save the file, and exit from the text editor.

Now, start MailScanner for the first time using the following command:

```
sudo check_mailscanner
```

Now either restart the Postfix server (using sudo /etc/init.d/postfix restart) or use the postfix reload command to cause the active Postfix daemon to pick up your changes to the configuration file.

To test that MailScanner is correctly integrated with your mail server, send yourself a piece of mail through your mail server. If MailScanner is working correctly (and the mail was not spam and not contain a virus), you should see the following banner at the bottom of the message:

> This message has been scanned for viruses and dangerous content by MailScanner, and is believed to be clean.

Congratulations! You are now doing a decent amount of spam filtering and are also checking for viruses in any mail received by your mail server!

# Tip

As mentioned previously, SpamAssassin is a powerful tool that scans incoming mail for spam and can optionally be configured to scan incoming mail for viruses.
