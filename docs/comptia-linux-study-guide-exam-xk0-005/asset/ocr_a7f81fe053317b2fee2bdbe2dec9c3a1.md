# Listing 22.3: Viewing unsuccessful login attempts with the `lastb` command

```
$ sudo lastb -f /var/log/btmp -f /var/log/btmp.* | grep JPicard
JPicard tty4                    Wed Jan  4 13:29 - 13:29  (00:00)
JPicard tty4                    Wed Jan  4 13:29 - 13:29  (00:00)
```

# Checking Privilege Elevation Issues

Most Linux distributions allow use of the sudo command to let users perform administrative tasks as the root user account, which is called privilege elevation. If there’s a user account that’s not allowed to use the sudo command, you need to check a few things.

First, take a look at the /etc/sudoers file to see what users and groups are allowed to elevate their privileges. If the user account isn’t specified directly in the /etc/sudoers file, there may be some groups that are specified. Those would have entries that look like this:

```
# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo ALL=(ALL:ALL) ALL
```

In this configuration from an Ubuntu system, users in the admin group are allowed to use the sudo command for root privilege elevation, and members of the sudo group can gain privileges to execute any command as any user account.

The next step is to see what groups the user account belongs to. The easiest way to do that is by using the id command:

```
$ id rich
uid=1000(rich) gid=1000(rich) groups=1000(rich),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),
120(lpadmin),131(lxd),132(sambashare)
$
```

The output from the id command shows all of the groups the user account belongs to. In this example, the rich user account does belong to the sudo group, so it should have access to use the sudo command for privilege elevation as any user account on the system.

# Checking GUI Issues

If you find that the account successfully logged into the system in the past and has no recent failed attempts, find out the user’s local access method. If using the GUI, have the user attempt to log into a text-based terminal, such as the tty2 terminal. If the user cannot successfully log into a terminal, then something else is amiss. The next few chapter sections after this one will help.

If the user can successfully log into a text-based terminal but not the GUI, you’ve narrowed down the problem. Determine what services are running. For older SysVinit systems, the runlevel command will show whether the graphical environment is current