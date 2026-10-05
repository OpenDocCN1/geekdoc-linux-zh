# Chapter 7 Adding New Users

Table 7.5 User account options in /etc/security/user (AIX)

| Option | Type | Meaning |
|---|---|---|
| account_locked | Boolean | Prevents login if true |
| admin | Boolean | Gives admin privileges if true |
| auth1 | Method list | Primary authentication method |
| auth2 | Method list | Secondary authentication method |
| dictionlist | Filenames | Dictionaries that must exclude passwords |
| expires | Date | Expiration date of the user account |
| histexpire | Weeks | Period when a user cannot reset a pwd |
| histsize | Number | # of previos that can't be erased |
| login | Boolean | Can log in? Good for logins like bin |
| loginretries | Number | # of login tries before account is locked |
| logintimes | Time range | Limits when the user can log in |
| maxexpired | Weeks | Grace period for expired devs |
| maxrepeats | Number | # of times a character can appear in pw |
| minage, maxage | Weeks | Minimum and maximum age of a pwd |
| minpalha | Chars | # of alpha characters allowed in new pw |
| minlen | Number | Minimum length of pwd (not set to 0) |
| minother | Number | Minimum # nonalph character in pw |
| pwchecks | Filenames | Functions to check for safe pwds |
| pwdwartime | Days | Grace period warning to check pw |
| login | Boolean | Can user login or telnet to this? |
| su | Boolean | Can others su to this account? |
| tty | Device list | Terminals on which this user can log |
| umask | Octal | Default permissions for user-created files |

Whew, what a list! Comments in the file often give the default values, which are fairly reasonable for a low-security installation. We recommend changing a few:

+   * Change umask from 022 to 077.
* Change loginretries from 0 (unlimited) to a small integer, say 5.
* Change minlen from 0 (no password OK) to at least 6 or 7.
* Change expires from 0 (never) to a year (only if you have a tool to refresh the expiration dates on valid users periodically.)

Unfortunately, that's just one of the configurations that controls a new user's login. The file /etc/security/login.cfg contains parameters to control bad logins (the delay inserted between prompts for login and password, the number of bad logins before disabling the account, how long to allowed the account, when to reinstate it, etc.), the times at logins are allowed, the prompt to print when requesting the user's password, a list of valid shells, the maximum number of simultaneous logins, the length of time to wait for a user password, the type of login authorization to use (here is where you would specify