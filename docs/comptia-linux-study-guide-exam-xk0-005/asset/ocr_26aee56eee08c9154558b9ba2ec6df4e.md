Just as with access issues, check your Linux kernel security module (SELinux or AppArmor) in situations where a user cannot create or delete files. Peruse the appropriate policy violation log files (/var/log/messages or /var/log/audit/audit.log) using the appropriate tools.

After you have found the policy violation concerning the file or directory in question, determine if the file/directory was mislabeled, the policy is incorrect, or possibly the wrong security context was used. Take appropriate actions to remedy the situation.

# Exploring Environment and Shell Issues

When dealing with user problems, a potential issue is the user account’s default shell. Check it using the getent command, as shown on an Ubuntu distribution in Listing 22.14.

```
**Listing 22.14:** Determining an account’s default shell with the getent command

```
$ getent passwd BSisko
BSisko:x:1007:1007::/home/BSisko:/bin/sh
$
$ readlink -f /bin/sh
/bin/dash
$ 
```

```

Notice that instead of the /bin/bash shell as the default shell, the /bin/sh shell is used. On this system, the /bin/sh file is linked to the /bin/dash shell. If this is not desired, you can change the user’s default shell via the usermod command (see Chapter 10).