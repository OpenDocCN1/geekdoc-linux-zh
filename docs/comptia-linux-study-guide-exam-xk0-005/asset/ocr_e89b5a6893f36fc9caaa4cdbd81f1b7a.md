If the user attempts to log into a different text-based terminal and can’t, check to see if getty services are running. These services provide the login prompts for the text-based terminals. An example of checking for getty services on a systemd system is shown snipped in Listing 22.6.

# **Listing 22.6:** Checking for getty services with the `systemctl` command

```
```
$ sudo systemctl status getty.target
  getty.target - Login Prompts
  [...]
  Active: active since Wed 2023-01-04 09:38:13 EST; 6h ago
  [...]
```
```

The `getty.target` is active, so getty services are available. If a user still cannot log into the system, you’ll need to explore additional issues.

![](bbox=[0.13, 0.45, 0.2, 0.53])

Check the `/etc/security/access.conf` file. This file is scanned when a user attempts to log into the system. Its configuration accepts or blocks users/groups from accessing the system. It can also prohibit certain logins to the text-based terminals, as well as logins originating over the network.

# ## Checking Additional Local Issues

Determine if the account is locked. You can employ the `passwd -S` or the `getent` command to check this, as shown snipped in Listing 22.7.

# **Listing 22.7:** Checking if an account is locked with the `passwd` and `getent` commands

```
```
$ sudo passwd -S KJaneway
KJaneway L 01/02/2019 0 99999 7 -1
$
$ sudo getent shadow KJaneway
KJaneway:!!$6$[...]0:L7898:0:99999:7:::
```
```

The L after the user KJaneway account’s name indicates the account is locked. However, that code is also shown for accounts that have no password set. Thus, the `getent` command is also employed. The exclamation point (!) at the front of the account password’s field verifies that the account is indeed locked. To unlock the account, if desired, use super user privileges and the `usermod -U` or the `passwd -u` command.

![](bbox=[0.13, 0.94, 0.2, 0.00102])

Check the user’s keyboard. Sometimes incorrect keyboard mappings or corrupted hardware can cause wrong characters to be sent to authentication programs.