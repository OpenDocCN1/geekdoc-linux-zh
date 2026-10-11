When changing a user’s ID, it must be unique unless you use the `-o` option. Be sure that the user is not logged in and verify that there are no processes running with that user’s old ID.

Any files located in the user’s home directory will have the UID associated with them changed; however, any files belonging to the user that are located elsewhere will have to be changed manually. Any crontab or at jobs also will need to be changed.

If you use the `-m` option when using the `-d` option to designate a new home directory, the files contained in the present home directory will be copied to the new location with the permissions intact.

# ## Deleting Users

When a user no longer requires access to your system, you should remove his account, files, and any crontab or at jobs he might have running. To manually remove a user, follow these steps:

+   1. Remove that user’s line from the `/etc/passwd` file.
+   2. Delete the user’s home directory.
+   3. Search for and delete files owned by that user located outside his home directory.
+   4. Delete the user’s mail and any mail aliases.
+   5. Delete any jobs he might have scheduled.

An easier way to perform this same task is to use the `userdel` command. Its syntax is

```
userdel [option] username
```

Using the `userdel` command without an option will delete the user from the `/etc/passwd` and other system files but will not delete his home directory. Use the `-r` option to also have his home directory deleted. You will still need to delete any files he owns that are located outside his home directory.

If you want to disable a user’s account rather than delete it, add an asterisk at the beginning of the password field in `/etc/passwd`. Do not change the encrypted password itself—this will prevent the user from logging in. When you want to reactivate the account, merely remove the asterisk and the user can log in.

# ## Special User Accounts

If you look at your `/etc/passwd` file or the example at the beginning of this chapter, you will see several user accounts that are system accounts. Each of these has a special purpose, some of which are listed in Table 7.3.