
## Verifying Your Identity

As a system administrator, you may occasionally need to use `su` to run programs using other users' identities in order to debug problems or to acquire root privileges. You might also have multiple login accounts, either on one system or on many. In any of these cases, you may forget what account you're using. When this happens, `whoami` can come to the rescue:

```
$ whoami
c.farrell
```

Few options to `whoami` exist; just `--help` and `--version`, which are common ones on many programs.

## Configuring Groups

Linux provides group configuration tools that parallel those for user accounts in many ways. Groups are not accounts, however, so many features of these tools differ. Likewise, you can create or modify groups by directly editing the configuration files in question. Their layout is similar to that for account control files, but the details differ.

### Adding Groups

Linux provides the `groupadd` command to add a new group. This utility is similar to `useradd` but has fewer options. The `groupadd` syntax is as follows:

```
groupadd [-g GID [-o]] [-r] [-f] groupname
```

The parameters to this command enable you to adjust its operation, as summarized in Table 5.7.

**TABLE 5.7 Options for groupadd**

| Option Name | Option Abbreviation | Effect |
| :--- | :--- | :--- |
| `--gid GID` | `-g` | You can provide a specific GID with this parameter. If you omit it, groupadd uses the next available GID. |
| `--non-unique` | `-o` | Normally, the GID you specify must be unused by other groups, but the `-o` parameter overrides this behavior, enabling you to create multiple groups that share one GID. |
| `--system` | `-r` | This parameter instructs groupadd to create a group with a GID of less than 500. Not all distributions support this option; it was added by Red Hat, and has been used on some related distributions, because Red Hat uses GIDs of 500 and greater for user private groups (as described shortly, in the section "Using User Private Groups"). |
| `--force` | `-f` | Normally, if you try to create a group that already exists, groupadd returns an error message. This parameter suppresses that error message. Not all versions of groupadd support this parameter. |

In most cases, you’ll create groups without specifying any parameters except for the group name itself, thus:

```
# groupadd project3
```

This command creates the project3 group, giving it whatever GID the system finds convenient—usually the highest existing GID plus 1. Once you’ve done this, you can add users to the group, as described in the next section. When you add new users, you can add them directly to the new group with the `-g` and `-G` parameters to `useradd`, described earlier.

### Modifying Group Information

You can modify group information, such as user account information, either by using utility programs or by directly editing the underlying configuration file, `/etc/group`. As with creation, there are fewer options for modifying groups than for modifying accounts, and the utilities and configuration files are similar. In fact, `usermod` is one of the tools that’s used to modify groups.

### Using `groupmod` and `usermod`

The `groupmod` command modifies an existing group's settings. Its syntax is as follows:

```
groupmod [-g GID [-o]] [-n newgroupname] oldgroupname
```

The options to this command modify its operation. The `-g` and `-o` options work just like their counterparts in `groupadd`. The `-n` (or `--new-name`) option specifies a new group name, should you want to change it.

One of the most common group manipulations you'll perform, however, is not handled through `groupmod`; it's done with `usermod`. Specifically, `usermod` enables you to add a user to a group with its `--groups` (or `-G`) parameter. For instance, the following command sets sally to be a member of the `users`, `project1`, and `project4` groups, and it removes her from all other groups:

```
# usermod -G users,project1,project4 sally
```

> **WARNING** Be sure to list all the user's current groups in addition to any groups to which you want to add the user. Omitting any of the user's current groups will remove the user from those groups. You can discover the groups to which a user currently belongs with the `groups` command, as in `groups sally`. To avoid accidentally omitting a group, many system administrators prefer to modify the `/etc/group` file in a text editor or to use `gpasswd`. Both methods enable you to add users to groups without specifying a user's existing group memberships.

### Using `gpasswd`

The `gpasswd` command is the group equivalent to `passwd`. The `gpasswd` command also enables you to modify other group features and to assign group *administrators*—users who may perform some group-related administrative functions for their groups. The basic syntax for this command is as follows:

```
gpasswd [-a user] [-d user] [-R] [-r] [-A user[,...]] [-M user[,...]] group
```

The options for this command modify its actions, as summarized in Table 5.8. If entered without any parameters except a group name, `gpasswd` changes the password for the group. Group passwords enable you to control temporary membership in a group, as granted by `newgrp`. Ordinarily, members of a group may use `newgrp` to change their current group membership (affecting the group of files they create). If a password is set, even those who aren't members of a group may become temporary group members; `newgrp` prompts for a password that, if entered correctly, gives the user temporary group membership.

**TABLE 5.8 Options for gpasswd**

| Option Name | Effect |
| :--- | :--- |
| `-a user` | This option adds the specified user to the specified group. |
| `-d user` | This option deletes the specified user from the specified group. |
| `-R` | This option configures the group to not allow anybody to become a member through `newgrp`. |
| `-r` | You can remove a password from a group using this option. |
| `-A user[...]` | The root user may use this parameter to specify group administrators. Group administrators may add and remove members from a group and change the group password. Using this parameter completely overwrites the list of administrators, so if you want to add an administrator to an existing set of group administrators, you must specify all of their usernames. |
| `-M user[...]` | This option works like `-A`, but it also adds the specified user(s) to the list of group members. |

Unfortunately, some of these features are not implemented correctly in all distributions. In particular, password entry by nongroup members sometimes does not give group membership—the system responds with an access denied error message. The `-R` option also sometimes doesn't work correctly—group members whose primary group membership is with another group may still use `newgrp` to set their primary group membership.

## Directly Modifying Group Configuration Files

Group information is stored primarily in the `/etc/group` file. Like account configuration files, the `/etc/group` file is organized as a set of lines, one line per group. A typical line in this file resembles the following:

```
project1:x:501:sally,sam,ellen,george
```

Each field is separated from the others by a colon. The meanings of the four fields are as follows:

- **Group name**: The first field (`project1` in the preceding example) is the name of the group.
- **Password**: The second field (`x` in the preceding example) is the group password. Distributions that use shadow passwords typically place an `x` in this field; others place the encrypted password directly in this field.
- **GID**: The group ID number (in this example's case, `501`) goes in this field.
- **User list**: The final field is a comma-separated list (with no spaces) of group members.
