PC-BSD, the sudoers file is found in /usr/local/etc. At this point, you should use the more command to examine the contents of the sudoers file on your system.

The sudoers file recognizes seven types of user specification lists. They are usernames, group names (such as wheel on PC-BSD), aliases defined within the sudoers file itself, UID numbers, GID numbers, netgroups, and non-UNIX groups. See the following examples for applications of some of these seven specification lists.

The sudoers file is composed of two types of entries: aliases (basically variables) and user specifications that specify who may run what. When multiple entries match a user, they are applied in order. Where there are multiple matches, the last match is used (which is not necessarily the most specific match). A user specification determines which commands a user may run (and as what user) on specified hosts. By default, commands are run as root, but this can be changed on a per-command basis.

The user specifications in the sudoers file contain policy rules, one rule per line. Every rule uses the general format as follows:

```
who where = (as_whom) what
```

where:
who is the user that this rule applies to. who can also be a user specification list—for example, a group name that has been defined as shown for Solaris in Section 23.3.3.7, "Adding Group Accounts," and for PC-BSD in Section 23.3.2, "Adding/Deleting and Maintaining Users and Groups in a GUI-Based Interface on PC-BSD."
where is the hostname of the system this rule applies to.
= separates the where from (as_whom) and what.
(as_whom) designates the user specification list sudo will run the what.
what lists the full path to each command this policy rule applies to.
You must specify full pathnames to command.

Some sudoers file examples follow:
In the following rule, bob can run any command:

```
bob ALL = ALL
```

The following rule from a Solaris sudoers file allows user sarwar to run the visudo program:

```
sarwar ALL = /usr/sbin/visudo
```

The following command run on a Solaris system, uses the -l option to sudo to allow you to list the permissions currently defined as policy in the sudoers file. We see that user sarwar can run all commands as root, all commands as the user admin, and visudo as root.

```
$ sudo -l
```