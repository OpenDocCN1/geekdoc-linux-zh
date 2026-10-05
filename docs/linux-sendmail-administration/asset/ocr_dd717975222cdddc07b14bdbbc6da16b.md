# Listing 6.4 Entries in the local-host-names File

```
[root]# cat local-host-names
# local-host-names - include all aliases for your machine here.
#
robin.foobirds.org
robin
[root]# ps -ax | grep sendmail
542 ? S 0:00:: accepting connections
[root]# kill -HUP 542
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <reuses> <address>
$=w
robin.foobirds.org
wren.foobirds.org
[172.16.12.3]
wren
localhost
robin
>^D
```

Now wren will accept mail for robin, although it won't necessarily know what to do with it. If Jill will be downloading her mail from a mailbox on wren, you must create a valid user account for Jill to allow Sendmail to create the necessary spool directory to hold her mail and allow her to download the mail via POP or IMAP. If Jill's is supposed to be forwarded to another system, mail routing instructions must be given to Sendmail through the aliases database or another appropriate database. Clearly, adding hostnames to class w is essential, it is only a first step. A possible next step is to configure the aliases database.

# The aliases Database

Once mail is accepted by the Sendmail server for local delivery, Sendmail must decide how to deliver the mail. It must determine whether the user identified in the recipient address is a local user with a local mailbox, or a user alias whose must be forwarded to the real recipient. The primary database used to make this determination is the aliases database.