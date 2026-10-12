For example, the following renames the existing novices group to experts:

```
groupmod -n experts novices
```

To change the GID, use the -g new GID option. For example, the following changes the current GID of the troublemakers group to 666:

```
groupmod -g 666 troublemakers
```

# # groups

Syntax: groups [username]

The groups command displays the list of group(s) the named user currently belongs to. If no username is specified, the current user's groups are displayed.

# # last

Syntax: last [-number] [username] [reboot]

The last command displays a list of users who have logged in since /var/log/wtmp was created. For example, the following command shows the number of times user julie has logged in since the last time /var/log/wtmp was created:

```
last julie
```

The following command shows only the last ten logins by julie:

```
last -10 julie
```

This command displays the number of times the system was rebooted since /var/log/wtmp file was created:

```
last reboot
```