You can see that the sendmail daemon is running and responding to port number 25. Try typing **HELO**. When you are done, type **QUIT** to exit.

> **NOTE:** For more information on troubleshooting your mail server, refer to the *Linux Troubleshooting Bible*, from Wiley Publishing.

# Redirecting mail

At times, your e-mail users may want to redirect mail to some place other than their own mailboxes on the local server. Each user can redirect his or her mail using the `.forward` file. System-wide, you as the administrator can set aliases to redirect mail in the `/etc/aliases` file.

# The .forward file

One way for users to redirect their own mail is through the use of the `.forward` file, which users can place in their own home directories (for example, `/home/jkpat/.forward`). The format of a plain-text `.forward` file is a comma-separated list of mail recipients. Common uses of the `.forward` file include:

+   - Piping mail to a program to filter the mailbox contents:
+     - `* |/usr/bin/procmail*`

+   - Sending mail destined for one user (for example, jkpat) to another (for example, cht09, on a different machine in this case):

```
cht09@other.mybox.com
```

+   - Delivering mail to the local user (jkpat again) *and* sending it to two others (cht09 and brammigan):

```
jkpat, cht09@other.mybox.com, brammigan
```

> **TIP:** You are not allowed to have a `.forward` file in a directory that can be read by all users. If you leave permissions open on a `.forward` file, sendmail will ignore that file and not forward mail as you want. To allow `.forward` files with open permissions to be used by sendmail, you can remove the `dn1` from the confDONT_BLAME_SENDMAIL line in the `sendmail.mc` file.

# The aliases file

A more flexible method of handling mail delivery (system-wide rather than being specific to one particular user) involves the `/etc/aliases` file, which is also a plain-text file. The aliases file contains a name followed by a colon, and then a name, another alias, a list of addresses, a file, or a program to which mail will be delivered. The name on the left side of the colon (which can be a valid user name or just an alias) can then be used as an e-mail recipient on the local machine or on a remote machine.