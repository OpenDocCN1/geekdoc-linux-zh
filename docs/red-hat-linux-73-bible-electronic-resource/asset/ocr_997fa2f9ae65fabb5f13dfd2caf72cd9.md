# The aliases file

A more flexible method of handling mail delivery (systemwide rather than being specific to one particular user) involves the /etc/aliases file, which is also a plain-text file. The aliases file (described earlier in the sendmail.cf section) contains a name followed by a colon, and then a user name, another alias, a list of addressees, a file, or a program to which mail will be delivered. The name on the left side of the colon (which can be a valid user name or just an alias) can then be used as an e-mail recipient on the local machine. Using the aliases file for mail aliasing allows for several extensions to normal mail-handling behavior:

+   - One account can receive mail under several different names:
+   `patterson: jkpat`
+   This indicates that any mail addressed to patterson@mybox.com (just an alias) will arrive in the mailbox of jkpat (an actual user account).

+   - Mail can be received under a name that isn’t a valid (or reasonable) user name:
+   `Charlie.Jackson.II@mybox.com: jackson`
+   He wouldn’t really want to type Charlie.Jackson.II as a user name, but that doesn’t mean he can’t receive mail as such.

+   - Messages intended for one user can be redirected to another account (or to several accounts):
+   ```
+   oldemployee: bradford
+   consultant: bradford, jackson, patterson
+   users: :include: /root/mail/lists/users
+   ```Here, any message for oldemployee@mybox.com would be delivered to the mailbox of user bradford. Also, the users bradford, jackson, and patterson would receive any mail addressed to consultant. The third line indicates that the recipients of the “users” alias are specified in the file /root/mail/lists/users.

+   - Mail can be sent directly to a file on the local machine:
+   ```
+   acsp-bugs: /dev/null
+   trouble-ticket: /var/spool/trouble/incoming
+   ```In the first line, because the fictional ACSP program is no longer used on the machine, there’s no need to track its errors, so the mail is effectively ignored. The second line stores incoming trouble tickets in the /var/spool/trouble/incoming file. Remember that if you enable this, anyone anywhere can send you a sufficiently large message to fill up the partition on which that directory resides. This is a security risk and should be carefully evaluated before being implemented.

+   - Incoming messages can be piped directly into an executable program:
+   `majordomo: "| /usr/lib/majordomo/wrapper majordomo"`