Changing the default values is a snap:

```
```
# useradd -D -s /bin/tsch
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/tsch
SHELL=/etc/skel
CREATE_MAIL_SPOOL=yes
#
```
```

Now, the *useradd* command will use the *tsch* shell as the default login shell for all new user accounts you create.

# Removing a user

If you want to remove a user from the system, the *userdel* command is what you need. By default, the *userdel* command removes only the user information from the */etc/passwd* and */etc/shadow* files. It doesn’t remove any files the account owns on the system.

If you use the *-r* parameter, *userdel* will remove the user’s $HOME directory, along with the user’s mail directory. However, there may still be other files owned by the deleted user account on the system. This can be a problem in some environments.

Here’s an example of using the *userdel* command to remove an existing user account:

```
```
# userdel -r test
# ls -al /home/test
ls: cannot access /home/test: No such file or directory
#
```
```

After using the *-r* parameter, the user’s old */home/test* directory no longer exists.



# TABLE 7.2 The useradd Change Default Values Parameters

| Parameter | Description |
| :--- | :--- |
| -b default_home | Change the location where users’ home directories are created. |
| -e expiration_date | Change the expiration date on new accounts. |
| -f inactive | Change the number of days after a password has expired before the account is disabled. |
| -g group | Change the default group name or GID used. |
| -s shell | Change the default login shell. |