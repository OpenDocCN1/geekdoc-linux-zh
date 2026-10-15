# 7.1 THE /ETC/PASSWD FILE

The /etc/passwd file is a list of users recognized by the system. It can be extended or replaced by a directory service, so it's complete and authoritative only on stand-alone systems.

The system consults /etc/passwd at login time to determine a user's UID and home directory, among other things. Each line in the file represents one user and contains seven fields separated by colons:

+   - Login name
+   - Encrypted password placeholder (see page 179)
+   - UID (user ID) number
+   - Default GID (group ID) number
+   - "GECOS" information: full name, office, extension, home phone
+   - Home directory
+   - Login shell

For example, the following lines are all valid /etc/passwd entries:

```
root:x:0:0:The System_x6096:/:/bin/sh
jl::100:0:Jim Lane,ECOT8-3,:/staff/jl:/bin/sh
dotty:x:101:20::/home/dotty:/bin/tcsh
```

Encrypted passwords used to live in the second field, but that is no longer safe; with fast hardware, they can be cracked (decrypted) in minutes. All versions of UNIX and Linux now hide the encrypted passwords by placing them in a separate file that is not world-readable. The passwd file contains an x in the encrypted password field on Linux, Solaris, and HP-UX and an ! or a * on AIX. (On AIX systems, * as a placeholder disables the account.)

The actual encrypted passwords are stored in /etc/shadow on Linux, Solaris, and HP-UX and in /etc/security/passwd on AIX. The formats vary.

If user accounts are shared through a directory service such as NIS or LDAP, you might see special entries in the passwd file that begin with + or -. These entries tell the system how to integrate the directory service's data with the contents of /etc/passwd. This integration can also be set up in the /etc/nsswitch.conf file (/etc/nscontrol.conf on AIX).

The following sections discuss the /etc/passwd fields in more detail.

# Login name

Login names (also known as usernames) must be unique and, depending on the operating system, may have length and character set restrictions. Table 7.1 shows the rules for our example systems. Login names can never contain colons or new-lines because these characters are used as field separators and entry separators,