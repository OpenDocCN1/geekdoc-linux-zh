+   Password — The user's initial password. (Ask the user to change this password the first time he or she logs in to the new account, using the passwd command.)

+   Confirm Password — Type the same password again, to make sure that you entered it correctly.

+   Login Shell — The default shell (for entering typed commands) that the user sees when opening a Terminal window, virtual window, or other shell prompt.

+   Create home directory — By default this box is selected and the user's home directory (as indicated by the Home Directory field) is created automatically.

+   Home Directory — By default, the user is given a home directory of the user's name in the /home directory. (For example, the user sheree would be assigned /home/sheree as her home directory.) Change this field if you want to assign the user to a different home directory.

+   Create new group for this user — Check this box if you want a group by the same name as the user, created for this user. The name is added to the /etc/group file.

+   Specify user ID manually — Typically, you would not check this box, so that the UID for the new user would be assigned automatically. New UIDs for regular users start at 500. However, if you want to assign a particular UID for a user (for example, if you want to match the UID with the user's UID from another computer on your network), click this box and type the number you want to use in the UID box.

3. Click OK when you are done. The new user is added to the /etc/passwd and /etc/group files. The user account is now available for that user to login.

# Setting User Defaults

The useradd command and Red Hat User Manager window both determine the default values for new accounts by reading the /etc/login.defs file. You can modify those defaults by either editing that file manually with a standard text editor or by running the useradd command with the -D option. If you choose to edit the file manually, here is what you will face:

```
# *REQUIRED*
# Directory where mailboxes reside, _or_ name of file, relative
# to the home directory. If you _do_ define both, MAIL_DIR
# takes precedence.
# QMAIL_DIR is for Qmail
#
#QMAIL_DIR Maildir
MAIL_DIR /var/spool/mail
#MAIL_FILE .mail

# Password aging controls:
#
```