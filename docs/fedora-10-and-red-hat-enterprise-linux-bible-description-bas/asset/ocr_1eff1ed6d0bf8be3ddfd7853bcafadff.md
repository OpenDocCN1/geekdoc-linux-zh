# Chapter 11: Setting Up and Supporting Users 471

In this example, you create a user named projectx (with a group named projectx). Create a /usr/local/x directory and have it owned by root user and projectx group. Set the setgid bit on the group (2), open full read/write/execute permissions for user and group (77), and open read and execute permissions for else. Add each user to the group that you want to be able to write to the projectx directory (replace next with the user you want to add). After that, regardless of a user's primary group, any file created in the /usr/local/x directory by a user can be read or modified by anyone in the projectx group.

# Setting User Defaults

The useradd command and User Manager window both determine the default values for new accounts by reading the /etc/login.defs file. You can modify these defaults by either editing it manually with a standard text editor or by running the useradd command with the -d option. If you choose to edit the file manually, here is what you face:

```
# REQUIRED*
# Directory mailboxes reside, _or_ name of file, relative to the
# home directory. If you _do_ define both, MAIL_DIR takes precedence.
# QMAIL_DIR is for Qmail

#QMAIL_DIR Maildir
MA_DIR /var/spool/mail
#MAIL_FILE .mail

# Password aging controls:
#
# PASS_MAX_DAYS Maximum number of days a password may be used.
# PASS_MIN_DAYS Minimum number of days allowed password changes.
# PASS_MIN_LEN Minimum acceptable password length.
# PASS_WARN_AGE Number of days warning given before a password
# expires.

PASS_MAX_DAYS 99999
PASS_MIN_DAYS 0
PASS_MIN_LEN 5
PASS_WARN_AGE 7

# Min/max values for automatic uid selection in useradd
#
UID_MIN 500
UID_MAX 60000
```