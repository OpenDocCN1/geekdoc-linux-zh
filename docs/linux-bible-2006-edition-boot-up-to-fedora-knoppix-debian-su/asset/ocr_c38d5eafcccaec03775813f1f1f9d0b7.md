# 218 Part II ♦ Running the Show

the mailmailer's e-mail address or system name to the access file located in the /etc/mail directory.

Each line of the access file contains an e-mail address, host name, domain, or IP address followed by a tab and a keyword specifying what to take when that entity sends a message. Valid keywords are OK, RELAY, REJECT, DISCARD, and ERROR. The REJECT keyword will cause a sender's e-mail to be bounced back with an error message. The DISCARD keyword will cause the message to be silently dropped without an error back. You can even return a custom error message using the ERROR keyword.

Thus, an /etc/mail/access file may look similar to this:

```
# Check /usr/share/doc/sendmail/README.cf for a description
# of the format of this file. (search for access_db in that)
# The /usr/share/doc/sendmail/README.cf is part of the sendmail-doc
#
# package.
# by default allowing relay from localhost...
localhost.localdomain RELAY
localhost             RELAY
127.0.0.1            RELAY
#
# Senders we want to Block
emailer@yahoo.com     REJECT
stimpy.glaci.com      DISCARD
cyberpromo.com        ERROR:550 Die Spammer Scum!
192.170.16.99         ERROR:550 Email Refused
192.170.177
```

As with Linux configuration files, lines that begin with a pound (#) are comments. The list of blocked spammers is at the end of this example file. Note that the address to block can be a complete e-mail address, a full host name, a domain, an IP address, or a subnet.

To block a particular e-mail address or host from mailbombing, log into your system as root, edit the /etc/mail/access file, and add a line to DISCARD mail from the offending sender.

After saving the file and exiting the editor, you must convert the access file into a hash-indexed database called access.db. The database is updated automatically the next time sendmail starts. On Fedora and other Red Hat systems, you can convert the database immediately, as follows:

```
# cd /etc/mail
# make
```

Sendmail should now discard e-mail from the addresses you added.