A sample /etc/login.defs file is depicted in the following example:

```
```
[root@server1 root]# cat /etc/login.defs
# "REQUIRED"
# Directory where mailboxes reside, or name of file, relative to the
# home directory. If you_do_ define both, MAIL_DIR takes precedence.
#       OMAIL_DIR is for Qmail
#
#OMAIL_DIR        Maildir
MAIL_DIR           /var/spool/mail
#MAIL_FILE        .mail


# Password aging controls:
#
#	PASS_MAX_DAYS	Maximum number of days a password may be used.
#	PASS_MIN_DAYS	Minimum number of days allowed between password
#				changes.
#	PASS_MIN_LEN	Minimum acceptable password length.
#	PASS_WARN_AGE	Number of days warning given before a password
#				expires.
#
PASS_MAX_DAYS		99999
PASS_MIN_DAYS		0
PASS_MIN_LEN		5
PASS_WARN_AGE		7


#
#	Min/max values for automatic uid selection in useradd
#
UID_MIN			500
UID_MAX			60000


#
#	Min/max values for automatic gid selection in groupadd
#
GID_MIN			500
GID_MAX			60000


#
#	If defined, this command is run when removing a user.
#	It should remove any at/cron/print jobs etc. owned by
#	the user to be removed (passed as the first argument).
#
#USERDEL_CMD		/usr/sbin/userdel_local
```
```