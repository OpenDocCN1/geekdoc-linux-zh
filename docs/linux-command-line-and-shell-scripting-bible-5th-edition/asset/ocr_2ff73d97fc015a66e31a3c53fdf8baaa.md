# Part 1: The Linux Command Line

> **Note**
> Linux tracks dates using the old UNIX timestamp feature, which uses an integer value representing the day and time as the number of seconds since January 1, 1970. This comes in handy for doing “date math,” since UNIX timestamps are stored as integer values.

Using the shadow password system, the Linux system has much finer control over user passwords. It can control how often a user must change their password and when to disable the account if the password hasn’t been changed.

> **Tip**
> The shadow password file doesn’t store the password as plain text. Instead, it runs a hash algorithm against the password text and saves the result. The hash value isn’t technically an encryption, as the plain text password can’t be derived from the hash value. Instead, the system applies the same hash algorithm to the password value you enter at login and compares the result to the stored value.

# Adding a new user

The primary tool used to add new users to your Linux system is useradd. This command provides an easy way to create a new user account and set up the user’s $HOME directory structure all at once. The useradd command uses a combination of system default values and command-line parameters to define a user account. To see the system default values used on your Linux distribution, enter the useradd command with the -D parameter:

```
```
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELE=/etc/skel
CREATE_MAIL_SPOOL=yes
#
```
```

> **Note**
> The default values for the useradd command are set using the /etc/default/useradd file. Also, further security settings are defined in the /etc/login.defs file. You can tweak these files to change the default security behavior on your Linux system.