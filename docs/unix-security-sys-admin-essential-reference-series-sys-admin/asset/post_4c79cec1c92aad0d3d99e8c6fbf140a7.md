
## Configuration Files

The login process references the files /etc/passwd, /etc/security/passwd, /etc/security/login.cfg, and /etc/security/user. /etc/passwd is the standard UNIX password file, owned by root and world readable. The layout and weakness of the original UNIX password file were explained in Chapter 8 [1, 2, 3, 4]. As a remedy, AIX uses the shadow password file /etc/security/passwd (Figure 9.1), which is owned by root and has read and write permissions for root only.

As shown in Figure 9.1, the second field in /etc/passwd either contains an exclamation mark or is empty, in which case the user has no password. The user ID is used as a key to search for attributes in /etc/security/passwd. The password attribute refers to the encoded password, while lastupdate is the time in epoch (seconds since midnight, 1 January 1970) when the password was last changed. flags contains additional information on password changing and checking [5].

The file /etc/security/login.cfg changed considerably from AIX v3. It is divided into three parts: port configuration, password verification rules, and user definition. The default stanza applies to all ports. Each port can be defined separately and can overwrite the values in the default stanza entry.

Figure 9.2 shows an example of the v4 /etc/security/login.cfg. The first section of login.cfg specifies the default attributes for port definitions. Since most of the attributes are new with this version, I will list each and identify its function.

- herald Message printed when port is opened by getty.
- logindelay Delay in seconds between unsuccessful logins.
- logindisable Number of unsuccessful login attempts before port is closed.

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_99_0.png)

logininterval Number of seconds in which login disable-specified unsuccessful login attempts have to occur before port is closed.

loginreenable Minutes to pass before a locked port is reopened.

logintimes Date and time logins on this port are allowed or denied. The format is

[ "!" ] : time "-" time

or

[ "!" ] day [ "-" day ] [ ":" time "-" time ]

or

[ "!" ] date [ "-" date ] [ ":" time "-" time ]

## Figure 9.2 A sample AIX v4 /etc/security/login.cfg file.

```
* First section, port definitions
default:

  logintimes = 1:5:0700-1900,6:0800-1400,10
  login delay = 30
  login disable = 5
  login interval = 360
  login reenable = 60

/dev/console:

  herald = "Welcome to AIX Version 4.1.2\r\nlogin: "

* Second section, alternate login program.
mylogin:
  program = /usr/local2/adm/mylogin
* Third section, user definitions

u sw:
  shells = /usr/bin/bash,/usr/bin/csh,/usr/bin/ksh, maxlogins = 2
  login timeout = 15
```

day is a digit between 0 and 6 representing the day of the week, starting with 0 (Sunday). date and time are both four-digit numbers of the form mmdd and hhmm, with mandatory leading 0s. month ranges from 0 for January to 11 for December. For example, 0001-0231 indicates 1 January until 31 March. dd may be 00, indicating the first or last day of the month, depending on whether it appears in a start or end context. For example, 0700-1000 indicates the first day of August to the last day of November.

time is a 24-hour clock always preceded by a colon. Entries without a leading exclamation mark allow access during that time; a leading exclamation mark denies access. Several values may be specified, delimited by commas. The sample entry in Figure 9.2 allows login on Monday to Friday from 7a.m. till 7p.m., on Saturdays from 8a.m. till 2p.m., and no login on Sundays.

login timeout Timeout in seconds for user to enter the password.

maxlogins Number of simultaneous logins per user. This includes su and telnet sessions.

shells List of valid command shells.

The second section of login.cfg (Figure 9.2) is used if you call an alternate login program. The third section has only one stanza, which applies to all users and must be named usw. The file /etc/security/user (Figure 9.3) contains an entry for each user, and the default stanza applies to all users. Password rules, login times, password dictionaries, and password extension rules can be specified on a per-user basis. There are many more options, such as setting a user's initial umask and remote login permission [6].

The attributes displayed in Figure 9.3 are listed in the following text.

ttys List of valid terminals to login.

auth1 Primary authorization method. Values are SYSTEM for default password verification, NONE for no checking, and token;name for an alternate login program, where token is the key when searching in the second part of /etc/security/login.cfg and name is the userid to authenticate.

auth2 Secondary authorization method. Values are the same as for auth1.

SYSTEM Describes the login requirements, which may consist of multiple or alternate methods. Values are NONE for no password checking, files for local authentication only, and compat for local and Network Information System (NIS) authentication.
