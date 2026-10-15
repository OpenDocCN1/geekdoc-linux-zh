# Table 7.5 User account options in /etc/security/user (AIX)

| Option | Type | Meaning |
|---|---|---|
| account_locked | Boolean | Prevents login if true |
| admin | Boolean | Gives admin privileges if true |
| auth1 | Method list | Primary authentication method |
| auth2 | Method list | Secondary authentication method |
| dictionary | Filenames | Dictionaries that must exclude passwords |
| expires | Date | Expiration date of the user account |
| histexpire | Weeks | Period when a user cannot reuse a pwd |
| histsize | Number | # of previous pwds that can't be reused |
| login | Boolean | Can log in? Good for logins like bin |
| loginretries | Number | # of login tries before account is locked |
| logintimes | Time range | Limits when the user can log in |
| maxexpired | Weeks | Grace period for expired pwds |
| maxrepeats | Number | # of times a character can appear in pwd |
| minage, maxage | Weeks | Minimum and maximum age of a pwd |
| minalpha | Number | Minimum # of alpha characters in pwd |
| mindiff | Chars | # of old pwd chars allowed in new pwd |
| minlen | Number | Minimum length of pwd (don't set to 0) |
| minother | Number | Minimum # of nonalpha character in pwd |
| pwdchecks | Filenames | Functions to call to check for safe pwds |
| pwdwarntime | Days | Grace period warning user to change pwd |
| rlogin | Boolean | Can user rlogin or telnet to this account? |
| su | Boolean | Can other users su to this account? |
| ttys | Device list | Terminals on which this user can log in |
| umask | Octal | Default permissions for user-created files |

Whew, what a list! Comments in the file often give the default values, which are fairly reasonable for a low-security installation. We recommend changing a few:

+   - Change umask from 022 to 077.
+   - Change loginretries from 0 (unlimited) to a small integer, say 5.
+   - Change minlen from 0 (no password OK) to at least 6 or 7.
+   - Change expires from 0 (never) to a year (only if you have a tool to refresh the expiration dates on valid users periodically).

> See page 908 for more information about PAM.

Unfortunately, that's just one of the configuration files that controls a new user's login. The file /etc/security/login.cfg contains parameters to control bad logins (the delay inserted before prompting for the login and password, the number of bad logins allowed before disabling the account, how long to disable the account, when to reinstate it, etc.), the times at which logins are allowed, the prompt to print when requesting the user's password, a list of valid shells, the maximum permissible number of simultaneous logins, the length of time to wait for a user password, the type of login authorization to use (here is where you would specify