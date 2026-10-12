Here's what some of these sendmail files are supposed to contain (note that not all of these files have to be present in your /etc/mail directory, and even when present, some files may be empty):

+   - `/etc/mail/access` — Names and/or IP addresses of hosts allowed to send mail (useful in stopping spam — unwanted mail)
+   - `/etc/mail/access.db` — Access database generated from `/etc/mail/access` file
+   - `/etc/mail/helpfile` — Help information for SMTP commands
+   - `/etc/mail/local-host-names` — Names by which this host is known
+   - `/etc/mail/mailertable` — Mailer table used to override how mail is routed
+   - `/etc/mail/relay-domains` — Hosts that permit relaying
+   - `/etc/mail/trusted-users` — List of users allowed to send mail using other user's names without a warning
+   - `/etc/mail/userdb.db` — User database file containing information about each user's login name and real name
+   - `/etc/mail/virtusertable` — Database of users with virtual-domain addresses hosted on this system

# The .forward file

Users can redirect their own mail by placing a `.forward` file in their home directory. The `.forward` file is a plain-text file with a comma-separated list of mail addresses. Any mail sent to the user is then forwarded to these addresses. If the `.forward` file contains a single address, all e-mail for that user is redirected to that single e-mail address. For example, suppose a `.forward` file containing the following line is placed in the home directory of a user named `emily`:

```
ashley
```

This causes `sendmail` to automatically send all e-mail addressed to `emily` to the user name `ashley` on the same system. User `emily` does not receive mail at all.

You can also forward mail to a user name on another system by listing a complete e-mail address. For example, I have added a `.forward` file with the following line to send my messages (addressed to my username, `naba`) to the mail address `naba@comcast.net`:

```
naba@comcast.net
```