| Options | Description |
|---|---|
| -d dir | Sets the home directory of the new user. |
| -D | Displays defaults for all settings. Can also be used to reset default settings for the home directory (-b), group (-g), shell (-s), expiration date (-e), and password expirations (-f). |
| -e mm/dd/yy | Sets an expiration date for the account (none, by default). Specified as month/day/year. |
| -f days | Sets the number of days an account remains active after its password expires. |
| -g group | Sets a group. |
| -m | Creates user's home directory, if it does not exist. |
| -m -k skl-dir | Sets the skeleton directory that holds skeleton files, such as .profile files, which are copied to the user's home directory automatically when it is created; the default is /etc/skel. |
| -M | Does not create user's home directory. |
| -p password | Supplies an encrypted password (crypt or MD5). With no argument, the account is immediately disabled. |
| -r | A Red Hat-specific option that creates a system account (one whose user ID is lower than the minimum set in login.defs). No home directory is created unless specified by -m. |
| -s shell | Sets the login shell of the new user. This is /bin/bash by default, the BASH shell. |
| -u userid | Sets the user ID of the new user. The default is the increment of the highest number used so far. |
| TABLE 28-3 Options for useradd and usermod |

# usermod

The usermod command enables you to change the values for any of these features. You can change the home directory or the user ID. You can even change the username for the account. The usermod command takes the same options as useradd, listed in Table 28-3.

# userdel

When you want to remove a user from the system, you can use the userdel command to delete the user's login. With the -r option, the user's home directory will also be removed. In the next example, the user chris is removed from the system:

```
# userdel -r chris
```