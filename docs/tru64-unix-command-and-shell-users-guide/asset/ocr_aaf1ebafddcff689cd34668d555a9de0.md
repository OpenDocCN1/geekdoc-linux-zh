```
```shell
[5]  find / -type f -print > dir.paths &
% cp salary1 salary2
% fg
find / -type f -print > dir.paths
%
```
```

# 6.5 Displaying Information About Users and Their Processes

The operating system provides the following commands that can tell you who is using the system and what they are doing:

+   - `who` — Displays information about currently logged in users.
+   - `w` — Displays information about currently logged in users and what they are currently running on their workstations.
+   - `ps au` — Displays information about currently logged in users and the processes they are running.

The who command lets you determine who is logged into the system. It may be especially useful, for example, when you want to send a message and want to know whether the person is currently available.

In Example 6–2, information about all currently logged in users is displayed:

# Example 6–2. Output from the who Command

```
```text
$ who
juan    tty01   Jan 15 08:33
chang   tty05   Jan 15 08:45
larry   tty07   Jan 15 08:55
tony    tty09   Jan 15 07:53
lucy    pts/2   Jan 15 11:24   (boston)
$
```
```

The who command lists the user name of each user on the system, the workstation being used, and when the person logged in. In addition, if a user is logged in from a remote system, the name of the system is listed. For example, lucy logged in remotely from the system boston on Jan 15 at 11:24.

The actual display format of who varies according to your current locale. See Appendix C for more information about locales.

The who −u command gives all the information of the who command and also displays the PID of each user and the number of hours and minutes