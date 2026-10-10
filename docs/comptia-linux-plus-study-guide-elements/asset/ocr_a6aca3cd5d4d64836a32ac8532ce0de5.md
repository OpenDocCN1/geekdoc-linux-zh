/etc/shadow. The x in the example's password field is an indication that shadow passwords are in use. In a system that does not use shadow passwords, an encrypted password will appear here instead.

**UID** Following the password is the account's user ID (529 in this example).

**Primary GID** The default login group ID is next in the /etc/passwd line for an account. The example uses a primary GID of 100.

**Comment** The comment field may have different contents on different systems. In the preceding example, it's the user's full name. Some systems place additional information here, in a comma-separated list. Such information might include the user's telephone number, office number, title, and so on.

**Home directory** The user's home directory is next up in the list.

**Default shell** The default shell is the final item on each line in /etc/passwd. This is normally /bin/bash, /bin/tcsh, or some other common command shell. It's possible to use something unusual here, though. For instance, many systems include a shutdown account with /bin/shutdown as the shell. If you log into this account, the computer immediately shuts down. You can create user accounts with a shell of /bin/false, which prevents users from logging in as ordinary users but leaves other utilities intact. Users can still receive mail and retrieve it via a remote mail retrieval protocol like POP or IMAP, for instance. A variant on this scheme uses /bin/passwd so that users may change their passwords remotely but may not log in using a command shell.

You can directly modify any of these fields, although in a shadow password system, you probably do not want to modify the password field; you should make password-related changes via passwd so that they can be properly encrypted and stored in /etc/shadow. As with changes initiated via usermod, it's best to change /etc/passwd directly only when the user in question isn't logged in, to prevent an example from disrupting an ongoing session.

Like /etc/passwd, /etc/shadow may be edited directly. An example /etc/shadow line resembles the following:

```
sally:E/moFKeT5UnTq:14343:0:-1:-7:1:-1:-
```

Most of these fields correspond to options set with the chage utility, although some are set with passwd, useradd, or usermod. The meaning of each colon-delimited field of this line is as follows:

**Username** Each line begins with the username. Note that the UID is not used in /etc/shadow; the username links entries in this file to those in /etc/passwd.

**Password** The password is stored in encrypted form, so it bears no obvious resemblance to the actual password. An asterisk (*) or exclamation mark (!) denotes an account with no password (that is, the account doesn't accept logins—it's locked). This is common for accounts used by the system itself.