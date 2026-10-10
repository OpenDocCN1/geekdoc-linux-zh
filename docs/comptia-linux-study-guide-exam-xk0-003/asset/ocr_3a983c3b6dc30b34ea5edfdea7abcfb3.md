# Configuring Groups

**TABLE 5.8** Options for *gpasswd*

| Option Name | Effect |
|---|---|
| -a *user* | This option adds the specified user to the specified group. |
| -d *user* | This option deletes the specified user from the specified group. |
| -R | This option configures the group to not allow anybody to become a member through *newgrp*. |
| -r | You can remove a password from a group using this option. |
| -A *user* [ , . . .] | The root user may use this parameter to specify group administrators. Group administrators may add and remove members from a group and change the group password. Using this parameter completely overwrites the list of administrators, so if you want to add an administrator to an existing set of group administrators, you must specify *all* of their usernames. |
| -M *user* [ , . . .] | This option works like -A, but it also adds the specified user(s) to the list of group members. |

Unfortunately, some of these features are not implemented correctly in all distributions. In particular, password entry by nongroup members sometimes does *not* give group membership—the system responds with an access *denied* error message. The -R option also sometimes doesn't work correctly—group members whose primary group membership is with another group may still use *newgrp* to set their primary group membership.

# Directly Modifying Group Configuration Files

Group information is stored primarily in the */etc/group* file. Like account configuration files, the */etc/group* file is organized as a set of lines, one line per group. A typical line in this file resembles the following:

```
`project1:x:501:sally,sam,ellen,george`
```

Each field is separated from the others by a colon. The meanings of the four fields are as follows:

+   - **Group name** The first field (project1 in the preceding example) is the name of the group.
+   - **Password** The second field (x in the preceding example) is the group password. Distributions that use shadow passwords typically place an x in this field; others place the encrypted password directly in this field.
+   - **GID** The group ID number (in this example's case, 501) goes in this field.
+   - **User list** The final field is a comma-separated list (with no spaces) of group members.