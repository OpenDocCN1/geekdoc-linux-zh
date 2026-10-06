# 484 Part III: Administering Fedora and RHEL

or if you want to lock out a customer whose account is temporarily disabled. The information isn't removed; it isn't just accessible).

![](bbox=[0.237, 0.153, 0.597, 0.381])

Figure 11-3: Choose Properties to modify an existing user account.

+   * **Password** — Select Password Expiration if you want to control expiration of the user’s password. By default, passwords don't expire. Here are your options: “Days before change allowed” (forces the user to keep the password for at least a set of days before it is changed); “Days before change required” (allows the user to keep the same password for at least the number of days); “Days before warning change” (sets how many days before the password expiration day that the user is warned to change the password); “Days before account inactive” (sets the number of days after which the account is deactivated).
• **Groups** — Select from the list of available groups to add the user to one or more of those groups.


4. Click OK to apply the changes to the user account.

# Deleting User Accounts

Occasionally, it is necessary to remove a user account from your Linux system. This can be done with either the `userdel` command or the User Manager window.

# Deleting user accounts with userdel

The `userdel` command takes a single argument, which is the login name of the account to delete. If you supply the optional -r option, it also deletes the user’s home directory and all the files in it. To delete the user account with login name mary, you would type this:

```
userdel mary
```