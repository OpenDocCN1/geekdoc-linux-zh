cal systems. It is a good idea to configure **exim4** this way and change this variable only when you are ready to accept mail from other systems.
To minimize network accesses for DNS lookups, which can be helpful if you are using a dial-up line, change the value of the `dc_minimaldns` configuration variable to `true`.

`/etc/mailname`
The `/etc/mailname` file initially holds the node name (**uname -n**) of the server. The string stored in `/etc/mailname` appears as the name of the sending system on the envelope-from and From lines of email that originates on the local system. If you want email to appear to come from a different system, change the contents of this file. You can modify this file using a text editor; the `dpkg-reconfigure` utility can also change it.
The following file causes mail sent from the local system to appear to come from **username@example.com**, where **username** is the username of the user who is sending the email:

$ cat /etc/mailname

example.com

See page 724 for more information on **exim4** configuration variables. After making these changes, restart **exim4** (page 716).
Test Test **exim4** with the following command:

$ echo "my exim4 test" | exim4 user@remote.host

Replace **user@remote.host** with an email address on another system where you receive email. You need to send email to a remote system to make sure that **exim4** is sending email to the remote SMTP server (the smarthost). If the mail is not delivered, check the email of the user who sent the email (on the local system) for errors. Also check the log file(s) in the `/var/log/exim4` directory.

# **JUMPSTART II: CONFIGURING EXIM4 TO SEND AND RECEIVE MAIL**

To receive email sent from a nonlocal system to a registered domain (that you control), you need to configure **exim4** to accept email from nonlocal systems. This JumpStart describes how to set up a server that

+   - Accepts email from local and nonlocal systems.
+   - Delivers email that originates on local systems to a local system or directly to a nonlocal system, without using a relay.
+   - Delivers email that originates on nonlocal systems to a local system only.
+   - Does not forward email originating on nonlocal systems to other nonlocal systems (does not relay email).

This server does not relay email originating on nonlocal systems. (You must set the `dc_relay_domains` variable [page 726] for the local system to act as a relay.) For this