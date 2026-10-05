# Understanding Accounts

the account. Certain tools and procedures make it easy for users to access their home directories; for instance, the tilde (~) refers to a user's home directory when used at the start of a filename.

Default Shell A default shell is associated with every account. In Linux, this is normally Bash (/bin/bash), but individual users can change this if they like. Most non-root system accounts use the default shell to /usr/sbin/nologin or (/sbin/nologin) as an added security measure—this program displays a message stating that the account is not available. Using /bin/false also works in a similar way, although without the explanatory message.

You might guess its name from /etc/passwd password information. This isnt not normally the case today, although it was many years ago. For historical reasons, /etc/passwd must be readable by all users, so storing passwords, even as a salted and hashed password, is risky. Passwords are stored in another file, /etc/shadow, where only root can read it. This file contains a salted and hashed password, as well as other information, which can disclose an account after a period of time or if the user doesn't change the password within a given period of time. A typical /etc/shadow entry looks like this:

```
root:$1eF$mFeKTUnT3kq2U0AAFl1pOUic:16860:5:30:14:-1:
```

The meaning of each colon-delimited field on this line is as follows:

Username Each line begins with the username. Note that the UID is not used in /etc/shadow, the username links entries in this file to /etc/passwd.

Password The password is stored as a salted hash, so it bears no resemblance to the account. An asterisk (*) or exclamation mark (!) denotes an account with no password (that is, the account doesn't login—it's locked). This is common for accounts used by the system itself.

Last Change The next field (16866 in this example) is the last password change. This date is stored as the number of days since January 1, 1970.

Days Until a Change Is Allowed The next field (5 in this example) is the number of days before a password change is allowed. This is used to prevent users from changing their passwords as required and then changing them back to the original password.

Days Before a Change Is Required The next field (30 in this example) is the number of days before another password change is required (since the last-word change).

![](bbox=[0.775, 0.275, 0.938, 0.33])

Certification Objective

Passwords are stored using a salted hash, a one-way mathematical process with additional input (salt), that produces looks like nonsense to humans. When a user types a password, it's salted and hashed, and if the hashes match, access is granted.

January 1970 is also called Unix time, POSIX time, or epoch (inception), and it is the amount of time elapsed since Midnight UTC on that date. It is used for time systems and could cause problems in the year 2038 on older 32-bit processors, because the computer will run out of storage to track time properly in this way.

![](bbox=[0.775, 0.735, 0.938, 0.765])

![](bbox=[0.775, 0.845, 0.938, 0.875])