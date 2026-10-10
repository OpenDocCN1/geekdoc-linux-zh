# The `/etc/group` File

Groups are handled in much the same way as users—with a text database in `/etc`. But because groups normally don't have passwords, there is no need for special security on the `/etc/group` file (the group equivalent of `/etc/passwd`), other than having it writable only by root.

The following is a sample line from `/etc/group`. Note that there are only four fields: the group name, a “dummy” field (in which passwords would go if they existed), the group ID, and then a comma-separated list of the users in the group:

```
wheel:*:10:root,bob,frank
```

There is no hash database for `/etc/group` because the file's information generally is referenced much less frequently than the information in `/etc/passwd` and because most systems have far fewer groups than users. FreeBSD's “unique groups” policy, however, makes that latter point moot. Future development may produce a hash file for groups.

# Managing Groups

Without passwords, user access, and a hash file to worry about, adding a group to the system is much easier than adding a user. You can simply open the `/etc/group` file in any text editor and create a new line in the format listed earlier (make sure to give the new group a group ID that has not yet been used).

New groups are added automatically by the `adduser` script when it creates unique per-user groups. The group IDs typically match the corresponding user IDs, but that is not a requirement. You will most likely only be interested in adding systemwide groups—for example, for tasks such as running a Web server or a database back end. These groups generally ought to have group IDs in the range of 100 to 1000. The numbers above 1000 are usually used for unique per-user groups, to match the corresponding user IDs. The numbers under 100 tend to be populated by system groups that are part of the core operating system.

To add a user to a group, type the user's name into the fourth field. If there are already usernames in the fourth field, separate them with commas, as shown previously. You can remove a user just as easily—simply delete the name.

![](bbox=[0.927, 0.705, 0.965, 0.776])