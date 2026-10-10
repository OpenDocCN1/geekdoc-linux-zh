# **38. passwd: Change user password.**

The `passwd` command in Linux is used to change a user's password. It allows users to update their own password or, if executed by a superuser, change the password for any user on the system.

**Examples:**

+   1. **Change your own password:**

```
passwd
```

You will be prompted to enter your current password and then the new password.

+   2. **Change another user's password (as root):**

```
sudo passwd username
```

Replace "username" with the actual username. This command will prompt you to enter the new password for the specified user.

+   3. **Lock a user account:**

```
sudo passwd -l username
```