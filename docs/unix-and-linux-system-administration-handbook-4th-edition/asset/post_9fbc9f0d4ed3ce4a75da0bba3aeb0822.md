
useradd -D displays the defaults that useradd will use for new logins. Those defaults are set in the file /etc/default/useradd. On Red Hat, new users are placed in their own individual groups. The passwd file entry uses "x" as a password placeholder, and the shadow file uses "!", a code that disables the login and requires a sysadmin to set a password for the new user. MD5 encryption is the default. A new user's home directory is populated with startup files from /etc/skel.

## useradd on Solaris

On Solaris, some of the default parameters related to logins and passwords are stored in /etc/default/login and /etc/default/passwd; others are built into the useradd command itself. useradd -D shows the default values for several parameters. With additional flags, it can be used to reset some of those defaults.

The format of the default/login and default/passwd files is similar to that of Linux's login.defs file in that blank lines and lines beginning with # are ignored, and each noncomment line assigns a value to a variable. However, the syntax is

```
NAME=value
```

rather than

```
NAME <white-space> value
```

The /etc/default/passwd file controls the following:

- Minimum password length
- Password aging
- Required password complexity
- Checking for crackable passwords

/etc/default/login controls issues such as these:

- The time zone
- Limits on the size of files a user can create
- Whether root can log in only on the console
- Whether a password is required for each user
- Handling of failed login attempts
- Users' initial search path
- Users' default umask (defaults to 022)
- Whether to log root and failed logins through syslog

The files /etc/security/policy.conf and /etc/security/crypt.conf determine the encryption algorithms that can be used for passwords.

## useradd on HP-UX

By default, HP-UX's useradd command does not create home directories or put the user in an individual group. However, with the -m option, useradd does create home directories and populate them with startup files from /etc/skel.

Configuration parameters for **useradd** are set in the files **/etc/default/useradd** and **/etc/default/security**, with the **useradd** file adopting the Linux-style format of **NAME <white-space> value** and the **security** using the Solaris **NAME=value** style. Geez, HP, make up your mind! The syntax should be clear from other entries in each file, but if you use the wrong form, the variable you tried to set will be silently ignored. No syntax error message is generated.

The **/etc/default/useradd** file controls options such as:

- Default group and shell
- Root of the home directory tree
- Account expiration
- Whether to create home directories
- Whether to allow duplicate UIDs

The file **/etc/default/security** contains additional configuration parameters, some of which relate to user management:

- Whether to allow logins with a missing home directory
- Whether to allow null passwords
- Minimum password length
- Handling of failed login attempts
- Handling of inactive accounts
- Default umask for new users (default 027)

The variable names in this file are long and well-chosen to explain exactly what each variable controls.

## useradd on AIX

AIX's **useradd** is really just a **ksh** wrapper for its native AIX equivalent, **mkuser**. Likewise, **usermod** invokes **chuser**, and **userdel** calls **rmuser**. Man pages exist for these commands under both their original names and their rest-of-the-world-compliant names.

Configuration files control numerous aspects of logins and passwords and are kept in the **/etc/security** directory. There are three relevant files: **login.cfg**, **user**, and **mkuser.default**. The first two use the * as a comment character; the third has no comments. These files are organized in stanzas of the following form:

```
label:
    attribute = value
    next-attribute = value

next-label:
    attribute = value
```

For example, in the **/etc/security/user** file, the labels are usernames (or the word default); the possible attributes are shown in Table 7.5 on the next page.
