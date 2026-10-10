# The .forward File

One way for users to re-direct their own mail is through the use of the .forward file, which users can place in their own home directories (e.g., /home/jkpat/.forward). The format of a plaintext .forward file is a comma-separated list of mail recipients. Common uses of the .forward file include:

+   
+   - Piping mail to a program to filter the mailbox contents:
+   

```
$\quad$"| /usr/bin/procmail"
```

+   - Sending mail destined for one user (e.g., jkpat) to another (e.g., cht09, on a different machine in this case):

```
$\quad$cht09@other.mybox.com
```

+   - Delivering mail to the local user (jkpat again) and sending it to two others (cht09 and brannigan):

```
$\quad$\jkpat, cht09@other.mybox.com, \brannigan
```

> TIP: You are not allowed to have a .forward file in a directory that can be read by all users. If you leave permissions open on a .forward file, Sendmail will ignore that file and not forward mail as you want. To allow .forward files with open permissions to be used by Sendmail, you can remove the dn! from the confDO NOT_BLAME_SENDMAIL line in the sendmail.mc file.

# The Aliases File

A more flexible method of handling mail delivery (system-wide rather than being specific to one particular user) involves the /etc/aliases file, which is also a plaintext file. The aliases file contains a name followed by a colon, and then a username, another alias, a list of addresses, a file, or a program to which mail will be delivered. The name to the left of the colon (which can be a valid username or just an alias) can then be used as an e-mail recipient on the local machine or on a remote machine.

Some aliases are already set by default in /etc/aliases. For example, because there are a lot of administrative users defined in CentOS (bin, adm, lp, etc.), instead of having separate mailboxes for each one, messages for all of them are directed to the root user's mailbox as follows:

```
bin: root
daemon: root
adm: root
lp: root
```