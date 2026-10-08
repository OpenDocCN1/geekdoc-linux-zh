# group

![](bbox=[0.03, 0.11, 0.13, 0.18])

**group** - File that contains information about groups.

group(4)

group(4)

NAME
group, logingroup - group file, grp.h

DESCRIPTION

group contains for each group the following information:

+   - group name
- encrypted password
- numerical group ID
- comma-separated list of all users allowed in the group

This is an ASCII file. Fields are separated by colons, and each group is separated from the next by a new-line. No spaces should separate the fields or parts of fields on any line. If the password field is null, no password is associated with the group.

There are two files of this form in the system, /etc/group and /etc/logingroup. The file /etc/group exists to supply names for each group, and to support changing groups by means of the newgrp utility (see newgrp(1)). /etc/logingroup provides a default group access list for each user via login and initgroups() (see login(l) and initgroups(3C)).

The real and effective group ID set up by login for each user is defined in /etc/passwd (see passwd(4)). If /etc/logingroup is empty or non-existent, the default group access list is empty. If /etc/logingroup and /etc/group are links to the same file, the default access list includes the entire set of groups associated with the user. The group name and password fields in /etc/logingroup are never used; they are included only to give the two files a uniform format, allowing them to be linked together.

All group IDs used in /etc/logingroup or /etc/passwd should be defined in /etc/group. No user should be associated with more than NGROUPS (see setgroups(2)) groups in /etc/logingroup.

These files reside in directory /etc. Because of the encrypted passwords, these files can and do have general read permission and can be used, for example, to map numerical group IDs to names.

The group structure is defined in <grp.h> and includes the following members:

```
```
char *gr_name;    /* the name of the group */
char *gr_passwd;  /* the encrypted group password */
gid_t gr_gid;     /* the numerical group ID */
```
```