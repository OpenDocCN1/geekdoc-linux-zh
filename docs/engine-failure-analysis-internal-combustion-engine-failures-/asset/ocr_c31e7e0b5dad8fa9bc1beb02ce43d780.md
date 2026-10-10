OPTIONS (CONT.)

| Use This Option | To Do This |
| --- | --- |
| -u | Unlock the account so that it is open for use by a user without root privileges. Requires root user status. |
| -d | Disable the password for an account by removing the password. Requires root user status. |
| -S | Display the account status. Requires root user status. |

# pwck

```
pwck [-r]
```

Examines all the passwords in the default password files (/etc/passwd and /etc/shadow) to make sure they do not contain errors. If errors are found, the user is prompted to correct them. Use the -r option to run the command in a test mode (no changes are made to the password files).

# pwgen

```
pwgen length [ count ]
```

Generates a high-quality password (one that combines uppercase and lowercase letters, as well as numbers) that may be pronounceable and, therefore, easy to remember. Specify the length by typing a number. You should create a password of at least six characters. Optionally, specify a count (a number) to generate more than one password. If pwgen is not installed on your system, you can obtain a copy from http://metalab.unc.edu/pub/Linux/system/security.

# quota

```
quota [ option ] name
```

Displays the current disk usage and limits for the specified user or group name. Root user status is required to view other user's quotas. To view quota information, quotas must be enabled (see edquota).

See also repquota, quotacheck, quotaoff, quotaon.