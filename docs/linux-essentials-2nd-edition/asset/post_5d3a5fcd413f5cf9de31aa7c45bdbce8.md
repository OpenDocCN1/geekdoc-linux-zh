
## Identifying Accounts

One way to identify user accounts is to use a GUI tool for account management. Such tools vary from one distribution to another. One example is the Users account tool in the Settings control panel on a Fedora system, which can be quickly reached by clicking Activities in the main window and typing users in the search box, as shown in Figure 12.1.

![](img/77662199428609b7662c8dc9c0e45c10_252_0.png)

FIGURE 12.1 Locating the Users account tool in Fedora

Alternatively, if you're searching for a specific account, you can use grep to find it in /etc/passwd, as in grep /etc/passwd to find information on any account that is tied to a user with the username rich. (This specific example assumes that the string appears in the password file, of course.)

An alternative to similar searching /etc/passwd is to type passwd. This command retrieves entries from certain administrative databases, including the /etc/passwd file. In most cases, typing passwd produces results that are identical to typing cat /etc/passwd; however, sometimes the passwords are typically displayed as dots or asterisks as a security feature.

You can pull out individual records by using the getent command. Just add the username to the command—for instance, getent passwd rich.

## Chapter 12 Understanding Basic Security

aren't identical. The /etc/passwd file defines only local user accounts. It's possible to configure Linux to use a network account database to define some or all of its accounts. If you use such a configuration, typing passwd returns both local accounts and accounts defined on the network server.

![](img/77662199428609b7662c8dc9c0e45c10_253_0.png)

FIGURE 12.2 The Users account tool provides minimal account information.

## NETWORK ACCOUNT DATABASES

Many networks employ network account databases. Such systems include the Network Information System (NIS), an update to this system called NIS+, the Lightweight Directory Access Protocol (LDAP), Kerberos realms, and Active Directory (AD) domains. All of these systems move account database management onto a single centralized computer (often with one or more backup systems). The advantage of this approach to account maintenance is that users and administrators need not deal with maintaining accounts independently on multiple computers. A single-account database can handle accounts on dozens (or even hundreds or thousands) of different computers, greatly simplifying day-to-day administrative tasks and also simplifying users' lives. Using such a system, means that most user accounts won't appear in /etc/passwd and /etc/shadow, and groups may not appear in /etc/group (described

## Understanding Accounts

## NETWORK ACCOUNT DATABASES

Linux can participate in these systems. In fact, some distributions provide options to enable such support at OS installation time. Typically, you must know the name or IP address of the server that hosts the network account database, and you must know what protocol system uses. You may also need a password or some other protocol-specific information, and the server may need to be configured to accept accounts from the Linux system that you're configuring. Activating use of such network account databases after installing Linux is a complex topic that is not subtle to alter the behavior of tools such as password and usermod (described in Chapter 13) in subtle or not-so-subtle ways. If you need to use a system, you'll have to consult documentation specific to the service that you intend to use.

## Understanding Groups

As noted earlier, groups are collections of accounts that are defined in the /etc/group file. Like /etc/passwd, the /etc/group file contains colon-delimited lines (records), each defining a single group. An example looks like this:

```
users:x100:games,sally
```

The fields in /etc/group are as follows:

**Group Name** The first field, users in the preceding example, is the name of the group. You use it with most commands that access or manipulate group data.

**Password** Groups, like users, can have passwords. A value of x means the password is defined elsewhere (but may be disabled), and an empty password field means the group has no password.

**GID** Linux uses GID values, like UID values, internally. Translation to and from group names is done for the benefit of users and administrators.

**User List** You can specify users who belong to the group in a comma-delimited list at the end of the /etc/group record.

It's important to recognize that users can be identified as members of a group in either of two ways:

Certification Objective

The use and management of group passwords is a topic that is beyond the scope of this book.

## Chapter 12 Understanding Basic Security

**By Specifying the Group's GID in Users' Individual /etc/passwd Entries** Because /etc/passwd has room for only one GID value, only one group can be defined in this way. This is the user's primary (or default) group.

**By Specifying Usernames in the User List in the /etc/group File** A single user can appear multiple times in /etc/group, and a single group can have multiple users associated with it in this way. If a user is associated with a group in this way but not via the user's /etc/passwd entry, this group association is secondary.

When you create new files, those files will be associated with your current group. When you log in, your current group is set to your primary group. If you want to create files associated with another group, you can use newgrp command, as:

```
$ newgrp project1
```

Group ownership of files is important, which is described more detail in Chapter 13.

## Using Tools

A few commands can help you learn about users and groups. Most notably, whoami and id utilities can tell you about your identity.

## Discovering Your Own Identity

If you maintain multiple accounts for yourself and you don't recall which one used to log in, you might become confused about your current status. In such a case, the whoami command can come in handy. It displays your user ID:

```
$ whoami
christine
```

This example reveals that the current account is christine. If you need more information, you can use the id utility:

```
$ id
uid=1002(christine) gid=100(users) groups=100(users)
```

This example shows information on both users and groups:

- Your user ID and username: uid=1002(christine) in this example
- Your current group: gid=100(users) in this example
- All your group memberships: groups=100(users) in this example

The id command displays both the numeric UID or GID values and the associated names. The current group is the one that's active, by default or because you used the newgrp command.

You can limit id's output by specifying various options, as summarized in Table 12.1. In addition, you can specify a username, as in id sally, to obtain information on that user rather than yourself.

## TABLE 12.1 Options for id

| Long option | Short option | Effect |
| --- | --- | --- |
| --group | g | Displays only the effective group ID |
| --groups | -G | Displays all of the groups to which you belong |
| --user | -u | Displays only the user data |
| --name | -n | Used in conjunction with -g, -G, or -u; displays only the name, not the UID or GID |
| --real | -r | Used in conjunction with -g, -G, or -u; displays only the UID or GID, not the name |

## Learning Who's Online

Linux permits multiple users to access the computer simultaneously. Most often, this is done by means of remote access servers such as the Secure Shell (SSH); however, you can use Linux's virtual terminal (VT) feature to log in multiple times with a single keyboard and monitor. Sometimes, you might want to know who is using the computer. You might do this before shutting down the computer, for instance, to ensure that you don't inconvenience another user.
