# **Using grouomod and usermod**

The `grouomod` command modifies an existing group’s settings. Its syntax is as follows:

```
grouomod [-g GID [-o]] [-n newgroupname] oldgroupname
```

The options to this command modify its operation. The `-g` and `-o` options work just like their counterparts in `groupadd`. The `-n` (or `--new-name`) option specifies a new group name, should you want to change it.

One of the most common group manipulations you’ll perform, however, is not handled through `grouomod`; it’s done with `usermod`. Specifically, `usermod` enables you to add a user to a group with its `--groups` (or `-G`) parameter. For instance, the following command sets `sally` to be a member of the `users`, `project1`, and `project4` groups, and it removes her from all other groups:

```
# usermod -G users,project1,project4 sally
```

> Be sure to list all the user’s current groups in addition to any groups to which you want to add the user. Omitting any of the user’s current groups will remove the user from those groups. You can discover the groups to which a user currently belongs with the `groups` command, as in **groups sally**. To avoid accidentally omitting a group, many system administrators prefer to modify the `/etc/group` file in a text editor or to use `gpasswd`. Both methods enable you to add users to groups without specifying a user’s existing group memberships.

# **Using gpasswd**

The `gpasswd` command is the group equivalent to `passwd`. The `gpasswd` command also enables you to modify other group features and to assign **group administrators**—users who may perform some group-related administrative functions for their groups. The basic syntax for this command is as follows:

```
gpasswd [-a user] [-d user] [-R] [-r] [-A user[,...]] [-M user[,...]] group
```

The options for this command modify its actions, as summarized in Table 5.8. If entered without any parameters except a group name, `gpasswd` changes the password for the group. Group passwords enable you to control temporary membership in a group, as granted by `newgrp`. Ordinarily, members of a group may use `newgrp` to change their current group membership (affecting the group of files they create). If a password is set, even those who aren’t members of a group may become temporary group members; `newgrp` prompts for a password that, if entered correctly, gives the user temporary group membership.