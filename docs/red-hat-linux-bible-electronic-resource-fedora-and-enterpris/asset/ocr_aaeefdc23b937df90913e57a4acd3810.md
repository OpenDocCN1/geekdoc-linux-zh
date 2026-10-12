# # Setting User Defaults

The useradd command and Red Hat User Manager window both determine the default values for new accounts by reading the /etc/login.defs file. You can modify those defaults by either editing that file manually with a standard text editor or by running the useradd command with the -D option. If you choose to edit the file manually, here is what you face:

```
# *REQUIRED*
# Directory where mailboxes reside, _or_ name of file, relative to the
# home directory. If you_do_ define both, MAIL_DIR takes precedence.
# QMAIL_DIR is for Qmail
#
#QMAIL_DIR Maildir
MAIL_DIR    /var/spool/mail
#MAIL_FILE    .mail

# Password aging controls:
#
# PASS_MAX_DAYS    Maximum number of days a password may be used.
# PASS_MIN_DAYS    Minimum number of days allowed between password changes.
# PASS_MIN_LEN    Minimum acceptable password length.
# PASS_WARN_AGE    Number of days warning given before a password
#    expires.
#
PASS_MAX_DAYS        99999
PASS_MIN_DAYS        0
PASS_MIN_LEN        5
PASS_WARN_AGE        7


#
# Min/max values for automatic uid selection in useradd
#
UID_MIN                    500
UID_MAX                   60000

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN                    500
GID_MAX                   60000


#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD    /usr/sbin/userdel_local
```