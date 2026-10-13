The hostname, as well as the versions of RHEL 6 and the kernel, will vary. But that's irrelevant to actual logins; all you need to do is type in a username, press ENTER, and type in a password when prompted.

Logouts from the command line are even simpler; the exit, logout, and CTRL-D commands all perform logouts from the command line. Of course, once you've logged out from a system, the login prompt just shown will appear.

As discussed earlier in this chapter, there's a different way to switch user accounts. For example, to switch from the current account to user donna's account, run the following command:

```
$ su - donna
```

The same exit, logout, and CTRL-D commands can be used to exit from user donna's account.

Of course, users can log in to and log out of the GUI. While the steps vary a bit by desktop environment, they are as simple as the steps required to log in to and log out of any other operating system.

# CERTIFICATION OBJECTIVE 8.04

# Users and Network Authentication

By default, access to a Linux computer requires a valid username and password. One problem with a large network of Linux systems is that without some central database, each user would require an account on every Linux computer.

Several services are available that can be used as a central authentication database.

> exam watch
> 
> In the RHCSA objectives, the only requirement is to be able to connect a client to a LDAP server. You're not required to actually create an LDAP server. In addition, NIS is no longer part of the objectives.

One now-obsolete option for the Red Hat exams is the Network Information Service (NIS). In contrast, the Lightweight Directory Access Protocol (LDAP) is specifically listed in the RHCSA objectives. Other services are available, namely Samba, which can be configured to support access by Linux systems and users to networks governed by a Microsoft database. In any of these cases, one database of passwords and usernames exists for a network.