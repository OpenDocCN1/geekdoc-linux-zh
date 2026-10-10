**Listing 22.1:** Viewing a user account record with the `getent` command

```
$ sudo getent passwd $J$irk
$J$irk:x:1002:1002::/home/$J$irk:/bin/bash
$
$ sudo getent shadow $J$irk
$J$irk::!:$1$7806:$0:$99999:$7:::
$
```

Notice that in the password field for the $J$irk shadow record, there is an exclamation mark (!). This indicates a password was not created for the account.

![](bbox=[0.13, 0.33, 0.26, 0.39])

Make sure your system users know that usernames are case sensitive on Linux. Other operating systems, such as Windows, have usernames that are case insensitive, and this can cause confusion.

# ### Checking Account Accesses

Look at the last time the account was successfully accessed. The `lastlog` utility searches through the `/var/log/lastlog` file for users who have logged into the system, but it only maintains the most recent login. The `last` command searches the `/var/log/wtmp` file for users who have logged in/out and keeps records for the most recent logins and beyond. This file is typically rotated with earlier versions and given a numeric extension. Thus, the next oldest version of `wtmp` is `wtmp.1`. The `last` command’s `-f` option will help you search through the various files, as shown in Listing 22.2.

**Listing 22.2:** Viewing successful logins with the `last` command

```
$ sudo last -f /var/log/wtmp -f /var/log/wtmp.* | grep $J$Picard
$J$Picard    tty3            Wed Jan  4 13:14 - 13:14  (00:00)
$
$ sudo lastlog -u $J$Picard
Username   Port      From      Latest
$J$Picard    tty3          Wed Jan  4 13:14:11 -0500  2023
$
```

Notice the `last` command shows that the $J$Picard account was logged into on January 4 at the tty3 terminal, and this is confirmed via the `lastlog` command.

You can also employ the `lastb` command. This command allows you to search for unsuccessful login attempts, as shown in Listing 22.3. Notice that the $J$Picard account had two failed login attempts at the tty4 terminal.