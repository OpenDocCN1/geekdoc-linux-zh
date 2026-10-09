```
# jexec mariadb adduser
Username: xistence
Full name: Bert JW Regeer
Uid (Leave empty for default):
Login group [bert]:
Login group is bert. Invite bert into other groups? []: wheel
--snip--
```

This jail now has an account for Bert, using his preferred username and everything. I've added it to the wheel group within the jail. Remember, root access within a jail doesn't equal root access on the host. That's the whole point of jails.
I can now run commands as that user in that jail.

```
# jexec -U xistence mariadb sh
$ 
```

I'm locked up in jail! Specifically, in Bert's jail cell.
This jailed process will behave a little oddly, though. A process retains its environment. In this case, while I'm running as the user xistence, I retain all the environment settings I had in my nonjailed process. This includes stuff like $SSH_AUTH_SOCK, my IRC server setting, and more. I don't want this stuff in my jailed environment. If I'm logged in as Bert, I want to be Bert.
To strip your environment before entering a jail, use jexec's -1 flag. This simulates a clean login.

```
# jexec -lU xistence mariadb sh
```

Should you always strip your environment before running a command in a jail? No, not always. It depends entirely on what you're doing.
Many commands include support for running them on the host but targeting a jail. Always check the man page for such an option. One good example is sysrc(8), which lets you specify a jail with -j. Here, I enable MariaDB on the jail mariadb. MariaDB has chosen to continue to use MySQL naming conventions, so it's enabled with the rc.conf option mysql_enable.