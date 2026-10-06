# 812 Part IV: Fedora and RHEL Network and Server Setup

separate mailboxes for each one, messages for all of them are directed to the root user's mailbox as follows:

```
bin: root
daemon: root
adm: root
lp: root
```

Using the aliases file for mail-aliasing for several extensions to normal mail-handling behavior:

+   You can use the aliases file yourself to create mini-mailing lists. Here's an example:
- info-list: chris, tweaks, francois@spidermaker.com

In this example, any messages sent to info-list are distributed to chris, tweaks, and francois@spidermaker.com. Notice that the user list can be a combination of local users and outside mail addresses.

+   One account can receive mail under several different names:
- patterson: jkpat\This indicates that any mail addressed to patterson@mybox.com (just as an alias) will arrive in the mailbox of jkpat (an actual account).
- Mail can be received under a name that isn't a valid (or reasonable) user name:
- eric.foster-johnson@objectpartners.com:efjohnson

He may not want to type eric.foster-johnson as a user name, but that doesn't mean he cannot receive mail as such.
Messages intended for one user can be redirected to another account (or to several accounts):

```
oldemployee: bradford
consultant: bradford, jackson, patterson
users:include:/root/mail/lists/users
```

Here, any message for oldemployee@mybox.com will be delivered to the mailbox of user bradford. The users bradford, jackson, and patterson would receive any mail addressed to consultant. The third line indicates that the recipients of the “users” are specified in the file /root/mail/lists/users.

+   Mail can be sent directly to a file on the local machine:
- acsp-bugs:/dev/null
trouble-ticket:/var/spool/trouble/incoming

In the first line, the fictional ACSP program is no longer used on the machine, there's no need to track its errors, so the mail is effectively ignored. The second line stores incoming trouble tickets in the /var/spool/trouble/incoming file. Remember that if you enable this, anyone anywhere can send you a sufficiently