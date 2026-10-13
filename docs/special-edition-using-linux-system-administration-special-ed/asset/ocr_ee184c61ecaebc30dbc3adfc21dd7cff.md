# The /etc/group File

The /etc/group file defines user groups on a Linux system. It contains a series of entries of the form:

```
<group name>:<password>:<GID>:<user list>
```

The fields in each entry have the following meanings:

+   - **Group Name:** The name by which humans identify the group. Group names should not contain spaces and they must start with a letter or number.
+   - **Password:** This field will contain an encoded version of the group’s password. Generally, groups do not require passwords.
+   - **GID:** Every group on the system must have a unique GID that is a numeric identifier used by the system and kernel to identify the group. You can define any scheme for assigning GIDs as discussed in the section “Selecting Groups and GIDs.”
+   - **User List:** A comma-separated list of usernames indicating the users who are members of the group.

You can edit the group file directly with your preferred text editor.

# Selecting Groups and GIDs

GIDs are numeric values in the range from 0-65534. Each group should have a unique GID in this range. You are free to segment this range in any way that makes sense for your site and it is not necessary to assign GIDs in consecutive order.

Current Linux distributions take one of two approaches to the assigning of groups. Some distributions, such as Red Hat Linux, create a separate group for each user to serve as the default group for that user. For instance, if user1 has a UID of 550, they will have as their default group 1 with the GID 550.

This provides for a strong security mechanism because no other users will belong to a user’s default group, which means that the group ownership permissions on their home directory don’t expose their data to access by other users.

However, this approach provides no flexibility in terms of using groups to assign permissions to broad ranges of users.

By contrast, other distributions create a single users group and make all new users members of that group. This makes it possible to easily grant permissions to access a file or directory to all users by making the users group the group owner of a file or directory. However, this approach does not offer fine-grained access control and, depending on permissions on a user’s home directory, can expose all of their data to viewing by all users on the system.

If you have a complex organizational structure or a large number of users, neither of these schemes is ideal. For instance, if you have a large user base, the scheme of creating a separate default group for each user means that you need to manage both a large user database in /etc/passwd as well as a large group database in /etc/group. By contrast, if you take the