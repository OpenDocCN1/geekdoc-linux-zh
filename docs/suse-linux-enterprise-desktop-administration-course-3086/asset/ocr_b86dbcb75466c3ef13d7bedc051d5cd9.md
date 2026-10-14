The variable LANG specifies the language. In this example, the language is set to U.S. English.

The characters are encoded in UTF-8 (Unicode Transformation Format). Unicode has the advantage that it is possible to use all kind of letters, not just Latin letters.

SUSE Linux Enterprise Desktop uses UTF-8 encoding for all users, except the user root.

```
da10:~ # locale
LANG=POSIX
LC_CTYPE=en_US.UTF-8
LC_NUMERIC="POSIX"
LC_TIME="POSIX"
LC_COLLATE="POSIX"
LC_MONETARY="POSIX"
LC_MESSAGES="POSIX"
LC_PAPER="POSIX"
LC_NAME="POSIX"
LC_ADDRESS="POSIX"
LC_TELEPHONE="POSIX"
LC_MEASUREMENT="POSIX"
LC_IDENTIFICATION="POSIX"
LC_ALL=
da10:~ #
```

There the LANG variable is set to POSIX (Portable Operating System Interface), which means the characters are ASCII encoded.

The LANG variable is important for this section because the output of some commands depends on the type of encoding. The order of characters is different in POSIX and in UTF-8.

You can see the differences between UTF-8 and POSIX encoding, when you use the ls command. For user geeko, the content of the /usr/share/doc/packages/yast2-users/ directory looks like this:

```
geeko@da10:~> ls -l /usr/share/doc/packages/yast2-users/
total 65
drwxr-xr-x 2 root root 1352 2006-02-02 15:42 autoyast
-rw-r--r-- 1 root root 17992 2006-01-27 00:34 COPYING
-rw-r--r-- 1 root root 17992 2006-01-27 00:34 COPYRIGHT.english
-rw-r--r-- 1 root root 2013 2005-09-08 02:36 crack.html
-rw-r--r-- 1 root root 75 2006-01-27 00:34 README
-rw-r--r-- 1 root root 193 2005-09-08 02:36 TODO.txt
-rw-r--r-- 1 root root 9583 2005-09-08 02:36 users.html
geeko@da10:~>
```