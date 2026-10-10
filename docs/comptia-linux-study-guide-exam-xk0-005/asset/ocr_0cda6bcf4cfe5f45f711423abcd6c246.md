# TABLE 10.5 The useradd command's commonly used options

| Short | Long | Description |
|---|---|---|
| -c | --comment | Comment field contents. Traditionally it contains the user's full name. Optional. |
| -d | --home or --home-dir | User's home directory specification. Default action is set by the HOME and CREATE_HOME directives. |
| -D | --defaults | Display /etc/default/useradd directives. |
| -e | --expiredate | Date of account's expiration in YYYY-MM-DD format. Default action is set by the EXPIRE directive. |
| -f | --inactive | Number of days after a password has expired and has not been changed until the account will be deactivated. A -1 indicates that the account will never be deactivated. Default action is set by the INACTIVE directive. |
| -g | --gid | Account's group membership, which is active when user logs into system (default group). |
| -G | --groups | Account's additional group memberships. |
| -m | --create-home | If it does not exist, create the user account's home directory. Default action is set by the CREATE_HOME directive. |
| -M | N/A or --no-create-home | Do not create the user account's home directory. Default action is set by the CREATE_HOME directive. |
| -s | --shell | Account's shell. Default action is set by the SHELL directive. |
| -u | --uid | Account's User Identification (UID) number. |
| -r | --system | Create a system account instead of a user account. |

We need to employ a few of the options in Table 10.5 to create a user account on the Ubuntu Desktop distribution. An example is shown in Listing 10.10.

# Listing 10.10: Creating a user account on Ubuntu Desktop

```
$ sudo useradd -md /home/JKirk -s /bin/bash JKirk
[sudo] password for Christine:
$
$ grep ^JKirk /etc/passwd
```