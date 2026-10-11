Each line in the /etc/group file has four fields, each separated by a colon. If a field is blank, the colon is still required. Table 7.4 lists the fields and their contents.

**Table 7.4 The Fields Contained in Each Record in the /etc/group File and Their Contents**

| Field | Contents |
| :---- | :------- |
| Groupname | The group name must be unique and can be up to eight characters in length |
| Password | A password can be entered but usually it is either an asterisk or left blank |
| Group ID | The GID is used by the system and must be unique |
| Members | List of users who are members of a group separated by commas |


When a user attempts to access a file, the operating system first checks to see whether that user is the owner of the file. If she is not the owner, the OS checks to see whether the user is a member of the associated group.

If the user belongs to the appropriate group, she gets the access defined for the group. If she is not a member of this group, she gets whatever permissions have been assigned to all others. Access to resources is discussed in more detail in Chapter 9.

# # Identifying Your Group

Every user on your system must belong to at least one group. If only one group exists, make all your users members of that group. Users can belong to many groups; however, only one GID can be associated with a user at any point in time. The default group for each user is defined in the /etc/passwd file.

To find out what your present default group is, use the id command. It returns your UID, the GID, and the name of your default group. In addition, it lists all your group memberships. Its output might look like the following:

```
uid=503(hadden) gid=500(hadden) groups=500(hadden),520(wp)
```

You also can determine to which groups you belong by using the groups command. It outputs the groups to which you belong but does not indicate your present default group.

When a user creates a new file, his present group is associated with that file. You can change which group your default group is by using the command newgrp and specifying the desired group. For example, typing

```
newgrp wp
```

will make your present group the wp group. Now when you type id, you will see

```
uid=503(hadden) gid=520(wp) groups=500(hadden),520(wp)
```