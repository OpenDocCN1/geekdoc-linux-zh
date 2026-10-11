| -u, --unlock | Unlock the password for the user. |
|---|---|
| -e, --expire | The user will be forced to change the password in the next login attempt. |
| -n, --minimum DAYS | Minimum password lifetime, in days. |
| -x, --maximum DAYS | Maximum password lifetime. |
| -w, --warning DAYS | Days in advance, the user will receive warnings her password will expire. |
| -l, --inactive DAYS | Number of days that will pass before an expired password will be taken means that the account is inactive and should be disabled. |
| -S, --status | Output short information about the status of the password. |

*Table 4.10: Common options for the command passwd*

In *figure 4.11*, it is shown how to set the password for one user and how to lock the account (the command *passwd -S* is showing the letter *L* indicating is locked):

![](bbox=[0.13, 0.38, 0.86, 0.57])

*Figure 4.11: Output examples of the usage of the command passwd.*

# ## Command chage

This command is used to change the user password expiry information. The popular options are shown in *table 4.11*:

| Option | Description |
|---|---|
| -d, --lastday LAST_DAY | Set the date when the password was last changed. I |
| -E, --expiredate EXPIRE_DATE | Set the date when the user's account will no longer be accessible. |
| -I, --inactive INACTIVE | Set the number of days of inactivity after a password has expired before the account is locked. |
| -l, --list | Show account aging information. |
| -m, --mindays MIN_DAYS | Set the minimum number of days between password changes to MIN_DAYS. |
| -M, --maxdays MAX_DAYS | Set the maximum number of days during which a password is |