from changing to the group in question. A “x” refers to the separate pass-
word file /etc/gshadow.

**(<GID>)** The group’s numerical group identifier.

**(<Members>)** A comma-separated list of user names. This list contains all users who
have this group as a secondary group, i.e., who are members of this group
but have a different value in the GID field of their /etc/passwd entry. (Users
with this group as their primary group may also be listed here but that is
unnecessary.)

A /etc/group file could, for example, look like this:

```
root:x:0:root
bin:x:1:root,daemon
users:x:100:
project1:x:101:joe,sue
project2:x:102:bob
```

The entries for the root and bin groups are entries for administrative groups, similar to the system’s pseudo-user accounts. Many files are assigned to groups like this. The other groups contain user accounts. administrative groups

Like UIDs, GIDs are counted from a specific value, typically 100. For a valid entry, at least the first and third field (group name and GID) must be filled in. Such an entry assigns a GID (which might occur in a user’s primary GID field in /etc/passwd) a textual name. GID values

The password and/or membership fields must only be filled in for groups that are assigned to users as secondary groups. The users listed in the membership list are not asked for a password when they want to change GIDs using the newgrp command. If an encrypted password is given, users without an entry in the membership list can authenticate using the password to assume membership of the group. membership list
group password

In practice, group passwords are hardly if ever used, as the administrative overhead barely justifies the benefits to be derived from them. On the one hand it is more convenient to assign the group directly to the users in question (since, from version 2.6 of the Linux kernel on, there is no limit to the number of secondary groups a user can join), and on the other hand a *single* password that must be known by *all* group members does not exactly make for bullet-proof security.

If you want to be safe, ensure that there is an asterisk (“*”) in every group password slot.

# ### 13.2.4 The /etc/gshadow File

As for the user database, there is a shadow password extension for the group database. The group passwords, which would otherwise be encrypted but readable for anyone in /etc/group (similar to /etc/passwd), are stored in the separate file /etc/gshadow. This also contains additional information about the group, for example the names of the group administrators who are entitled to add or remove members from the group.

# ## Exercises

+   13.5 [1] Which value will you find in the second column of the /etc/passwd file? Why do you find that value there?

+   13.6 [2] Switch to a text console (using, e. g., [Alt]+[F1]) and try logging in but enter your user name in uppercase letters. What happens?