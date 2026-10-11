| Option | Description |
|---|---|
| -a, --append | Add the user to the secondary group(s). Use only with the -G option |
| -c, --comment COMMENT | Usually used to specify user's full name. |
| -d, --home HOME_DIR | The user's new login directory. |
| -g, --gid GROUP | The new main group name or group id for the user. |
| -G, --groups GROUP1,GRP2 | A list, command separated, of secondary groups for the user. |
| -l, --lock | Lock a user's password. |
| -m, --move-home | Move the content of the user's home directory to the new location. |
| -s, --shell SHELL | The path of the user's new login shell. |
| -U, --unlock | Unlock a user's password. |

*Table 4.7: Common options for the command usermod*

In *figure 4.5*, a secondary group named **syslog** is added to the user **testuser2** created previously:

```
```
root@ubuntu:~# usermod -G syslog testuser2
root@ubuntu:~# id testuser2
uid=1002(testuser2) gid=1002(testuser2) groups=1002(testuser2),113(syslog)
```
```

*Figure 4.5: Example adding a secondary group to user testuser2 using usermod*

# ## Command Islogins

The command **lslogins** is a modern command to display information about available users in the system. Not specifying any argument or options will list all the users and information about the last login and the number of processes running by the user if the password is locked. This can be shown in *figure 4.6*:

```
```
root@ubuntu:~# lslogins

  UID USER          PROC PWD-LOCK PWD-DENY LAST-LOGIN GECOS
   0 root          108   0        0        root
   1 daemon        0     0        1        daemon
   2 bin           0     0        1        bin
 112 usbmux        0     0        1        usbmux daemon,,,
1000 agonzalez     5     0        0  12:21 agonzalez,12,1234,12345
678
1001 testuser      0     0        1        Test User
1002 testuser2     0     0        0        Test User2,,,
```
```

*Figure 4.6: Output example (truncated) of command Islogins*

Specifying one of the existing users as argument, detailed information about the account is shown, as illustrated in *figure 4.7*: