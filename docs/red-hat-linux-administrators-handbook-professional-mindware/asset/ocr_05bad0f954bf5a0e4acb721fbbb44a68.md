This keyword denies FTP users the ability to retrieve named files. For example,

```
noretrieve /etc/passwd
```

denies anyone the ability to retrieve the /etc/passwd file. A message such as /etc/passwd is marked unretreivable is displayed. Note that if the filename does not include a fully qualified path name, all files with such names are marked unretreivable. For example,

```
noretrieve passwd core
```

prevents anyone from retrieving any file named passwd or core from any directory. Wildcards can’t be used in the filename.

# loginfails

Syntax: loginfails number

Default: loginfails 5

This keyword defines the number of times a user can attempt to log in before being disconnected. When a user fails to enter a valid username/password pair for a login for the specified number of times, an error message is logged and the user is disconnected.

# private

Syntax: private yes or no

Default: none

The wu-ftpd server provides an extended set of FTP commands that are nonstandard. One of these commands is called SITE, which is considered a security risk. Therefore, use of the private keyword is not recommended. In fact, the SITE command is disabled in the default version of wu-ftpd shipped with Red Hat. You have to compile wu-ftpd yourself to enable the SITE command, which is not recommended.