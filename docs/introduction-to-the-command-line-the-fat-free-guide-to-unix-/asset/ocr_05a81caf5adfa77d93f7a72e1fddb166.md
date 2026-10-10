# useradd / userdel

Purpose: Create/delete user accounts.

Usage syntax: useradd [OPTIONS] [USER]

```
# useradd -m steve
# passwd steve
Enter new UNIX password: ******
Retype new UNIX password: ******
passwd: password updated successfully
Adding a user account to the system (and setting their password)
```

The useradd command creates new user accounts. In the above example, executing useradd -m steve creates a basic login account for a user. The -m option is used to automatically create a home directory for the specified user (recommended). The password is then set for the new user using the previously discussed passwd command.

> Note You must set the password for the new user using the passwd command before they can login.

The userdel command deletes user accounts from the system. The next example demonstrates using userdel to remove an account. The optional -r option is used to have the system automatically delete the specified user's home directory after removing their account.

Usage syntax: userdel [OPTIONS] [USER]

```
# userdel -r steve
Removing a user account
```

> Note The ruser command may be used on some Unix and BSD systems in place of userdel.

Common usage examples:

|  |  |
|---|---|
| useradd [USER] | Create the specified user account |
| useradd -m [USER] | Automatically create a home directory for the user |
| userdel [USER] | Delete the specified user account |
| userdel -r [USER] | Delete a user's account and their home directory |