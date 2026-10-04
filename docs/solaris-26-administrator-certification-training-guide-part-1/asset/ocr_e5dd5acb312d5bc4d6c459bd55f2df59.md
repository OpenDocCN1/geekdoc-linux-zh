# Table 5-3 Add User Fields (continued)

| Item | Description |
|---|---|
| Min Change | (Optional) The minimum number of days allowed between password changes. This is intended to prevent a user from changing the password and then changing it back a few seconds later, which would defeat the concept of password aging. The default is 0. |
| Max Change | (Optional) The maximum number of days the password is valid before it must be changed; otherwise, the account is locked. Leaving the field blank means the password never has to be changed. |
| Max Inactive | (Optional) The maximum number of days an account may go without being accessed before it is automatically locked. A blank field means the account remains active no matter how long it goes unused. |
| Expiration Date | (Optional) The date when the user account expires. None means no expiration. |
| Warning | (Optional) The number of days to begin warning the user before the password expires. A blank means no warning is given. |
| Create Home Dir check box | Select this box to have the user's home directory automatically created. |
| Path | Use the Path field to point to an existing directory or to specify a new directory to create. |

> NOTE. Users can type the UNIX command passwd at the command prompt to change their passwords.

# Deleting a User Account with Admintool

Use the Admintool to delete an existing user account. The procedure to delete a user account is as follows:

+   1. Start Admintool, if it's not already running, and choose Browse, Users.
2. Select the user account entry you wish to remove from the Users window.
3. Choose Edit, Delete.
4. The message is displayed to confirm the removal of the user account (see Figure 5-3).

Figure 5-3
Confirmation that you want to delete the user account.

![](bbox=[0.35, 0.88, 0.6, 0.95])