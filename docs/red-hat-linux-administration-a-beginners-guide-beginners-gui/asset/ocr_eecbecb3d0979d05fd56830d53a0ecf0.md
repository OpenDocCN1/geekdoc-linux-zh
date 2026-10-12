```
news: *:9:13:news:/var/spool1/news:   uucp: *:9:10:uucp:/var/spool1/uucp:   operator:*:11:0:operator:/root:   games:*:12:100:games:/usr/games:   gopher:*:13:30:gopher:/usr/lib/gopher-data:   ftp:*:14:50:FTP User:/home/ftp:   pop:*:15:15:APop Admin:/tmp/bin/tcsh   nobody:*:99:99:Nobody/:   rwhite:Kas9Ere9blEjs:500:500:Russell White:/home/rwhite/bin/tcsh   mpawlawski:bFcCAblvZBltFM:501:501:Mike Pawlawski:/home/mpawlawski:/bin/bash   bwoodall:*:502:502:Brent Woodall:/home/bwoodall:/bin/bash   michael:aMa7sGOrnhfdoO8Vablg7M2:503:503:Michael Turner:/home/michael/:bin/zsh
```

# The /etc/shadow File

The speed of home computers began making dictionary attacks against password lists easier for hackers to accomplish. This led to the separation of the encrypted passwords from the **/etc/passwd** file. The **/etc/passwd** file would remain readable by all users, but the passwords kept in the **/etc/shadow** file would be readable only by those programs with root privileges, such as the login program. An x is typically placed in the password field of **/etc/passwd** to indicate that the encrypted password actually exists in the shadow file.

In addition to the encrypted password field, the **/etc/shadow** file contains information about password expiration and whether the account is disabled. The format of each line in the **/etc/shadow** file contains the following:

+   - Login name
+   - Encrypted password
+   - Days since Jan. 1, 1970, that the password has been changed
+   - Days before the password may be changed
+   - Days after which the password must be changed
+   - Days before the password is about to expire that the user is warned
+   - Days after the password is expired that the account is disabled
+   - Days since Jan. 1, 1970, that the account has been disabled
+   - Reserved field