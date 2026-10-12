group is easy. For example, suppose I want to add the username `naba` to the group called `wheel`. I simply type the following command in a terminal window:

```
usermod -G wheel naba
```

To remove a user account, click the username in the list on the Users tab that displays all user accounts (refer to Figure 2-1). Then click the **Delete** button on the toolbar.

# Using commands to manage user accounts

If you’re working from a text console, you can create a new user account by using the `useradd` command. Follow these steps to add an account for a new user:

+   1. **Log in as root.**
+   
+   If you’re not already logged in as `root`, type `su -` to become `root`.
+   
+   2. **Type the following `useradd` command with the `-c` option to create the account:**
+   
+   `/usr/sbin/useradd -c “Ashley Barkakati” ashley`
+   
+   3. **Set the password by using the `passwd` command, as follows:**
+   
+   `passwd ashley`
+   
+   You’re prompted for the password twice. If you type a password that someone can easily guess, the `passwd` program rejects it.

The `useradd` command consults the following configuration files to obtain default information about various parameters for the new user account:

+   - `/etc/default/useradd`: Specifies the default shell (`/bin/bash`) and the default home directory location (`/home`).
+   - `/etc/login.defs`: Provides system-wide defaults for automatic group and user IDs, as well as password-expiration parameters.

Examine these files with the `cat` or more commands to see what they contain.

You can delete a user account by using the `userdel` command. Simply type `/usr/sbin/userdel username` at the command prompt to delete a user’s account. To wipe out that user’s home directory as well, type `/usr/sbin/userdel -r username`.