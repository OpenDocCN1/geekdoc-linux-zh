
## **LISTING 9.2 Continued**

```
your account ''joe'' was created.
Have fun!

See also chpass(1), finger(1), passwd(1)

Add anything to default message (y/n) [n]:
Send message (y/n) [y]: Copy files from /usr/share/skel to /home/joe
Add another user? (y/n) [y]: n
Goodbye!
```

Pressing Enter after every prompt accepts the default value, which is shown in brackets. Many of the prompts give you a space-separated list of choices, such as the prompt for the shell. When these choices include *no*, that option can be used to disable or decline whatever the prompt is offering. For instance, entering *no* for the shell creates the user without a valid shell, meaning that the user cannot log in to the system.

> **NOTE**
> As of FreeBSD 4.0 and later, the "csh" built in to the base system is actually tcsh, an extended version of csh (the C shell). You can still specify tcsh as a shell, but it's the same thing as csh.

If you like, you can put a file at `/etc/adduser.message` that will be e-mailed to the new user at the new local account. The user is able to read it the first time he or she logs in to the system and runs a mail program (more on reading mail can be found in Chapter 24, "Configuring E-mail Services"). To make it easier, if you have elected to send the adduser.message file, the script prompts you for a second address to send it to (for instance, an address that the person is already using), so you can be sure the user receives it.

The "dotfiles" that the script mentions are the semi-hidden shell configuration files (they are only visible if you use the -a option on ls):

- `.cshrc`
- `.login_conf`
- `.mailrc`
- `.rhosts`
- `.login`
- `.mail_aliases`
- `.profile`
- `.shrc`

These files are explained in more detail in the section titled "Shell Initialization Files," in Chapter 11, "Customizing the Shell."

Each user and group has a numeric equivalent to its name, user ID (UID), and group ID (GID). This ID is listed in the ownership information of a file or directory and is used to control processes. If you remove a user from the system, that user's files become owned by the UID number that the user left behind.

Removing a user is a fairly simple matter. The command here is `rmuser`, which takes the username as an argument (adduser does not), as shown in Listing 9.3.

## LISTING 9.3 A Sample rmuser Session

```
# rmuser joe
Matching password entry:

joe:IR8pIrE/nkDQo::1008:1008::0:0:Joe user:/home/joe:/bin/csh

Is this the entry you wish to remove? y
Remove user's home directory (/home/joe)? y
Updating password file, updating databases. done.
Updating group file: (removing group joe -- personal group is empty) done.
Removing user's home directory (/home/joe): done.
Removing files belonging to joe from /tmp: done.
Removing files belonging to joe from /var/tmp: done.
Removing files belonging to joe from /var/tmp/vi.recover: done.
```

The line about the "matching password entry" describes the database in which all the user information is kept, which brings us to our next topic.

## The `/etc/passwd` and `/etc/master.passwd` Files

All Unix-flavored operating systems have an `/etc/passwd` file, but the file's specific role differs from platform to platform. For some systems, `/etc/passwd` is the sole repository of user information (including passwords). In these cases, adding a user requires only that you add a line to the file using a text editor (`vi`, `pico`, `ex`, `emacs`, and so on). More modern operating systems, though, use a "shadow passwords" structure—a way of storing the encrypted password strings not in `/etc/passwd`, but in a different file that is readable only by root. This file's name varies, depending on the platform. On some platforms, it's `/etc/shadow`; on others, it's `/etc/security/master.passwd`. On FreeBSD, it's `/etc/master.passwd`.

Both of these passwd files are simple text databases, containing a line for each user with fields delimited with colons (:). The files contain the username, the user ID, the group ID of the primary group, the home directory, the login shell, and the full name (which also has embedded comma-delimited fields such as Office Location, Office Phone, and Home Phone).

The permissions on `/etc/passwd` are `0644`; on `/etc/master.passwd`, they're `0600`. This security scheme means that any user can access the information in `/etc/passwd`, but root is the only one who can see into `/etc/master.passwd`, which differs from `/etc/passwd` only in that it contains the users' encrypted passwords in the second field. Passwords are encrypted in FreeBSD using a hash scheme based on the MD5 algorithm. Here are examples of each:

`/etc/passwd:`
```
joe:*:1008:1008:Joe User:/home/joe:/bin/csh
```

`/etc/master.passwd:`
```
joe:$1$32i2knXsSTnjUWjj9LzYgWfRZOnOu/10:1008:1008:Joe User:/home/joe:/bin/csh
```

These two files aren’t the only ones that store user information, though. Flat text databases are fine for a fairly small number of users, but as the user base grows, the need for a faster, hash table-based lookup database becomes more and more obvious. On a system with 25,000 users in a linear text database, looking up a user’s information can take a significant amount of time—while the user is waiting to log in!

So, FreeBSD also has `/etc/pwd.db` and `/etc/spwd.db`. These files are hash tables in db format, corresponding to the “insecure” `/etc/passwd` and the “secure” `/etc/master.passwd`, respectively. They also have the same permissions as their corresponding clear-text files. These files provide a fast lookup mechanism for large user databases, and they’re generated by the `pwd_mkdb` program automatically every time you alter a user’s information with the `chfn`, `passwd`, or `adduser`/`rmuser` command.

Speaking of which, the `chfn` (change full name) command is the tool you use to change a user’s information. Like the `edquota` command we examined in the last chapter, `chfn` operates by invoking the editor specified in your `EDITOR` environment variable (`vi`, by default). You can then modify any of the text fields. Upon saving and exiting, the `/etc/master.passwd` file is rewritten, and `pwd_mkdb -p` is automatically run to rebuild the other three files.

It is important to understand that `/etc/master.passwd` is truly the “master” user database file. If you want to rebuild a user list or port one from another FreeBSD machine, you can simply place the new master.passwd file into /etc (or anywhere within the / partition) and then issue the following command:

```
# pwd_mkdb -p /etc/master.passwd.new
```

This example assumes that your new master.passwd file is in /etc as master.passwd.new. The `/etc/master.passwd` file is replaced with your new file, and `/etc/pwd.db`, `/etc/spwd.db`, and `/etc/passwd` are rebuilt. The -p option tells `pwd_mkdb` to generate a new `/etc/passwd` file; if this is omitted, `/etc/passwd` is left unchanged. You will probably want to use -p at all times to keep the two files synchronized.

> **NOTE**
> In FreeBSD, the `/etc/passwd` file itself is never consulted; it only really exists for compatibility with third-party applications. Most modern utilities look up user information from `/etc/pwd.db`.

## The `/etc/group` File

Groups are handled in much the same way as users—with a text database in `/etc`. But because groups normally don't have passwords, there is no need for special security on the `/etc/group` file (the group equivalent of `/etc/passwd`), other than having it writable only by root.

The following is a sample line from `/etc/group`. Note that there are only four fields: the group name, a “dummy” field (in which passwords would go if they existed), the group ID, and then a comma-separated list of the users in the group:

```
wheel:*:10:root,bob,frank
```

There is no hash database for `/etc/group` because the file's information generally is referenced much less frequently than the information in `/etc/passwd` and because most systems have far fewer groups than users. FreeBSD's “unique groups” policy, however, makes that latter point moot. Future development may produce a hash file for groups.

## Managing Groups

Without passwords, user access, and a hash file to worry about, adding a group to the system is much easier than adding a user. You can simply open the `/etc/group` file in any text editor and create a new line in the format listed earlier (make sure to give the new group a group ID that has not yet been used).

New groups are added automatically by the `adduser` script when it creates unique per-user groups. The group IDs typically match the corresponding user IDs, but that is not a requirement. You will most likely only be interested in adding systemwide groups—for example, for tasks such as running a Web server or a database back end. These groups generally ought to have group IDs in the range of 100 to 1000. The numbers above 1000 are usually used for unique per-user groups, to match the corresponding user IDs. The numbers under 100 tend to be populated by system groups that are part of the core operating system.

To add a user to a group, type the user's name into the fourth field. If there are already usernames in the fourth field, separate them with commas, as shown previously. You can remove a user just as easily—simply delete the name.

![](img/48eec858cce7dfb89da36a4d40b7daf3_244_0.png)
