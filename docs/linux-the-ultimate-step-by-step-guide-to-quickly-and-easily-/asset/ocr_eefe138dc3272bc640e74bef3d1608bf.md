| -g groupname | Specifies a group account for this account. |
| -m | Creates the home directory if it doesn't exist. |
| -s shell | Specifies the default shell for this account. |
| -u userid | You can specify a user id for this account. |
| accountname | Actual account name to be created |

If you do not specify a parameter then system will use the default values. The `useradd` command modifies the /etc/passwd, /etc/shadow, and /etc/group files and creates a home directory. The following is an example which will create an account mcmohd setting its home directory to /home/mcmohd and group as developers. This user would have Korn Shell assigned to it.

```
`$ useradd -d /home/mcmohd -g developers -s /bin/ksh mcmohd`
```

Before issuing the above command, make sure you already have a developers group created using `groupadd` command. Once an account is created you can set its password using the passwd command as follows –

```
`$ passwd mcmohd20`
`Changing password for user mcmohd20.`
`New UNIX password:`
`Retype new UNIX password:`
`passwd: all authentication tokens updated successfully.`
```

When you type `passwd accountname`, it gives you option to change the password provided you are superuser otherwise you would be able to change just your password using the same command but without specifying your account name.

# Modify an Account

The `usermod` command enables you to make changes to an existing account