-L Places an exclamation mark in front of the user's password in the /etc/passwd file, which disables the user's ability to log in.

-U Removes the exclamation mark from the user's entry in the /etc/passwd file, re-enabling the user's password.

login The user's login name.

# Disabling User Accounts

If you need to deactivate an account but believe that the account will be needed again in the future, you'll want to disable it instead of deleting it. A deleted account and a disabled account look exactly the same to a user attempting to log in that account, but a disabled account does not remove the user's home directory or any files owned by that.

# Manual Disabling

The simplest way to disable an account is to make sure that the user's password has expired. To do this, you can modify the user's entry in /etc/shadow. As discussed earlier, dates in this file are represented as the number of days since January 1, 1970. The third field in an entry is the date the password was last modified, and the eighth field is the date the account will expire. So you first want to change the user's password; the third field in the entry will reflect today's date. Subtract one from that number, insert the new number immediately before the last colon, and save the file.

```
docker1d:HXc52b8ocpmY:11088:0:9999:7:0::
```

Subtracting 11088 yields 11087, so you'd change the entry to this:

```
docker1d:HXc52b8ocpmY:11088:0:9999:7:0:11087:
```

# Disabling Account with Linuxconf

To disable a user's account, follow these steps:

+   1. Start Linuxconf as previously described.

+   2. Open Config > Users Accounts > Normal > User Accounts.

+   3. Select the account that you'd like to disable. You'll be presented with the Information screen, which resembles Figure 6.2.

+   4. Uncheck the Account Is Enabled box.

+   5. Click Accept to accept the modified user information.

+   6. Click Quit on the User Accounts screen that follows.

+   7. Click Act/Changes from the main Linuxconf screen.

+   8. Click Activate the Changes from the Status of the System screen.

+   9. Click Quit from the main Linuxconf screen.