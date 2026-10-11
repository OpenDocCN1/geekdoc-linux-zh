The - option to the su command shown in the preceding output loads the root user's environment variables. Also, you can omit the root user's name in the preceding output; if a name is not specified as an argument to the su command, the root user is assumed by default.

If you only intend to run one command as the root user, you can instead choose to use the -c option to the su command; this returns you to your current shell automatically. The following demonstrates how to run the root command shown in the previous output using the -c option to the su command:

```
[user1@server1 user1]$ su -c "rm -f /etc/security" root
Password: *****
[user1@server1 user1]$
```

Still, some users, such as software developers, need to run certain commands as the root user in certain situations. Instead of giving them the root password, it is best to give them the ability to run certain commands as the root user via the **sudo command**. The sudo command checks the /etc/sudoers file to see if you have rights to run a certain command as a different user. The following /etc/sudoers file allows the software developers, mary and bob, the ability to run the kill and killall commands as the root user on the computers server1 and server2:

```
[root@server1 root]$ cat /etc/sudoers
User_Alias SD = mary, bob
Cmd_Alias KILL = /bin/kill, /usr/bin/killall
Host_Alias SERVERS = server1, server2

SD   SERVERS = (root) KILL
[root@server1 root]$
```

Now, if mary needs to kill the cron daemon on server1 (which was started as the root user) to test a program that she wrote, she needs to use the sudo command, as shown in the following output, and supply her own password:

```
[mary@server1 mary]$ ps -ef |grep crond
root    2281    1    0 21:20 ?    00:00:00 crond
[mary@server1 mary]$ kill -9 2281
-bash: kill: (2281) - Operation not permitted
[mary@server1 mary]$ sudo kill -9 2281
```

We trust that you have received the usual lecture from the local System Administrator. It usually boils down to these two things:

```
#1) Respect the privacy of others.
#2) Think before you type.
Password: *****
[mary@server1 mary]$
```