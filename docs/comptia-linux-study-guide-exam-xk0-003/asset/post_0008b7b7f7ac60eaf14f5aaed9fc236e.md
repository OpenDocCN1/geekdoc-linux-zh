
![](img/9903a4d3f7abd8dcbef1035fa04a3406_246_0.png)

/etc/shadow is normally stored with very restrictive permissions, such as rw-------, with ownership by root. This fact is critical to the shadow password system’s utility since it keeps non-root users from reading the file and obtaining the password list, even in an encrypted form. Therefore, if you manually modify /etc/shadow, be sure it has the correct permissions when you’re done.

## Real World Scenario

## Network Account Databases

Many networks employ network account databases. Such systems include the Network Information System (NIS), an update to this system called NIS+, the Lightweight Directory Access Protocol (LDAP), Kerberos realms, Windows NT 4.0 domains, and Active Directory (AD) domains. All of these systems move account database management onto a single centralized computer (often with one or more backup systems). The advantage of this approach to account maintenance is that users and administrators need not deal with maintaining accounts independently on multiple computers. A single account database can handle accounts on dozens (or even hundreds or thousands) of different computers, greatly simplifying day-to-day administrative tasks and simplifying users’ lives. Using such a system, though, means that most user accounts won’t appear in /etc/passwd and /etc/shadow, and groups may not appear in /etc/group. (These files will still hold information on local system accounts and groups, though.)

Linux can participate in these systems, naturally. Activating use of such network account databases after installing Linux is a complex topic. Chapter 12 covers a few basics for NIS and LDAP. My book *Linux in a Windows World* (O’Reilly, 2005) covers this topic for Windows NT 4.0 domains, LDAP, and Kerberos.

## Deleting Accounts

On the surface, deleting user accounts is easy. You may use the userdel command to do the job of removing a user’s entries from /etc/passwd and, if the system uses shadow passwords, /etc/shadow. The userdel command takes just three parameters: --remove (or -r) causes the system to remove all files from the user’s home directory, as well as the home directory itself; --help (or -h) displays help information; and --force (-f) forces account removal even if the user is currently logged in. Thus, removing a user account such as Sally is easily accomplished with the following command:

```
# userdel -r sally
```

You can omit the -r parameter if you want to preserve the user’s files. There is one potential complication, however: users might create files outside their home directories. For instance, many programs use the /tmp directory as “scratch space,” so user files often wind up there. These files will be deleted automatically after a certain period, but you may have other directories in which users might store files. To locate all such files, you can use the find command with its -uid parameter. For instance, if sally had been UID 529, you might use the following command to locate all her files:

```
# find / -uid 529
```

The result will be a list of files owned by UID 529 (formerly sally). You can then go through this list and decide what to do with the files—change their ownership to somebody else, delete them, back them up to a removable disk, or what have you. It’s wise to do something with these files, though, or else they may be assigned ownership to another user if Sally’s UID is reused. This could become awkward if the files exceed the new user’s disk quota or if they contain information that the new user should not have—such a person might mistakenly be accused of indiscretions or even crimes.

A few servers—most notably Samba—keep their own lists of users. If you run such a server, it’s best to remove the user’s listing from that server’s user list when you remove the user’s main account. In the case of Samba, this is normally done by manually editing the smbpasswd file (usually located in /etc/ or /etc/samba) and deleting the line corresponding to the user in question, or by using the smbpasswd command and its -x option, as in smbpasswd -x sally to delete the sally account from Samba’s database.

### Verifying Account Use

Once accounts are created, you may have cause to check who’s using the computer. This information can be useful for a variety of reasons—to see how many people might be inconvenienced if you shut down the computer for maintenance or to verify that an account is not in use if the user is away on vacation, for instance. Several tools are useful in this task, including who, w, and last. The whoami command is also potentially useful if you regularly use multiple accounts.

### Checking Who’s Logged In

The who and w commands are similar in purpose. Both display information on who is currently logged in. For instance, consider the following interactions:

```
$ who
paul :0 2009-04-08 17:26
paul pts/0 2009-04-08 17:26 (:0.0)
rhonda pts/5 2009-04-10 20:06 (tycho.luna.edu)
```

```
$ w
20:10:18 up 2 days, 2:45, 7 users, load average: 0.00, 0.00, 0.00
USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT
paul :0 - Wed17 ?xdm? 9:04 0.13s /usr/bin/gnome-session
paul pts/0 :0.0 Wed17 1:29m 0.35s 0.08s bash
rhonda pts/5 tycho.luna.edu 20:06 0.00s 0.02s 0.01s w
```

Both of these interactions reveal three current logins: two by paul and one by rhonda. The user paul appears to be logged in at the console, as revealed by the :0 and :0.0 fields in the TTY and FROM columns of the w output and by the similar data in who’s output. These identifiers refer to a local X server. The tycho.luna.edu field in rhonda’s data, on the other hand, suggests that she’s logged in over a network, from the named remote computer.

The default output for who is fairly basic, so it’s a good tool if you just want a summary of who’s logged on. Table 5.4 summarizes options to who that can increase or change the information it presents. Some of these options overlap with the function of other tools, such as runlevel and uptime.

**TABLE 5.4** Options for who

| Option Name | Option Abbreviation | Effect |
|---|---|---|
| --all | -a | Presents all the available information. |
| --boot | -b | Displays the system boot time instead of a list of logged-in users. |
| --dead | -d | Displays dead processes, which can be useful information when managing processes. |
| --heading | -H | Adds column headings, which are omitted by default. |
| --ips | None | Causes remote systems to be identified by IP address rather than hostname. Not all versions of who support this option. |
| --login | -l | Obtains a list of running system login processes instead of a list of logged-in users. |
| --lookup | None | Looks up remote systems’ IP addresses to obtain hostnames. |
| None | -m | Restricts the username list to the user who’s using standard input. |
| --process | -p | Lists processes spawned by init. |
| --count | -q | Obtains the number of users who are logged in. |
| --runlevel | -r | Displays the current runlevel (similar to the runlevel command). |
| --short | -s | Displays only the username, access method, and login time; it’s the default. |
| --time | -t | Finds when the system clock last changed. |
| --users | -u | Displays users who are logged in; it’s similar to the default, but it adds a few fields. |

The w command presents more information by default than does who. Like who, w has a number of options, which are summarized in Table 5.5. You can also pass a username to w, as in w paul, to obtain information about only that user’s logins.

**TABLE 5.5** Options for w

| Option Name | Effect |
|---|---|
| -h | Prints output without the header. |
| -u | Ignores the username when computing process and CPU times; has a subtle effect when using su, sudo, and similar tools. |
| -s | Use short format; omits several columns’ data from the output. |
| -f | Toggles printing the FROM field; this field might or might not be included by default, depending on compile-time options. |
| -o | Use old-style display format. (Display format has changed slightly recently.) |

Both who and w are useful tools when you need to check on the current status of a computer’s user loads—say to minimize the inconvenience caused by shutting down a system for maintenance. The w command also gives you some idea of what your users are doing. This last information is very limited, though; w was designed long before GUIs became common, so it can’t show you information on the many independent windows a user may have open. The ps command (described in Chapter 3) is more likely to be useful for finding such information.
