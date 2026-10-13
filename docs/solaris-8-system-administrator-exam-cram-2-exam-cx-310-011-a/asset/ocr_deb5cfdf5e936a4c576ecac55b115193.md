name as a command-line argument to limit the displayed information to a single user. The following example shows the results of the finger command:

```
```text
$ finger
Login       Name             TTY       Idle     When       Where
root        Super-User       console   36       Sun 01:47
 dla         Darrell          pts/7     1:35     Sat 20:37  winnt40
$
$ finger -l
Login name: root                         In real life: Super-User
Directory: /                              Shell: /sbin/sh
On since Mar 18 01:47:03 on console from :0
36 minutes Idle Time
No unread mail
No Plan.

Login name: dla                         In real life: Darrell
Directory: /export/home/dla              Shell: /bin/sh
On since Mar 31 20:37:53 on pts/7 from winnt40
1 hour 36 minutes Idle Time
Unread mail since Fri Feb 9 13:53:42 2001
No Plan.
$
$ finger dla
Login name: dla                         In real life: Darrell
Directory: /export/home/dla              Shell: /bin/sh
On since Mar 31 22:14:03 on pts/5 from winnt40
Unread mail since Fri Feb 9 13:53:42 2001
No Plan.

Login name: dla                         In real life: Darrell
Directory: /export/home/dla              Shell: /bin/sh
On since Mar 31 20:37:53 on pts/7 from winnt40
1 hour 43 minutes Idle Time
$
```
```

You can also use the finger command to display information about users logged in to a remote system by specifying a hostname preceded by the at (@) character. For example, to display information about users logged in to the system sparc20, use the following command:

```
```text
$ finger @sparc20
[sparc20]
Login       Name       TTY       Idle      When      Where
root        Super-User console   7d        Tue 21:25  :0
$
```
```

# The last Command

The last command displays login and logout activity. This command is useful because it can identify users currently on the system and those who have been on the system recently. The following example shows the results of the last command:

```
```text
$ last
root     console       :0       Sun Mar 18 01:47   still logged in
reboot   system boot             Sun Mar 18 01:45
```
```