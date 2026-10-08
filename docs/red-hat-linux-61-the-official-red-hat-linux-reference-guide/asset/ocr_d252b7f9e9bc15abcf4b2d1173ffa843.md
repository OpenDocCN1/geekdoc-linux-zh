# Chapter 6. Users and Groups

| Group | GID | Members |
| --- | --- | --- |
| ldap | 55 | |
| netdump | 34 | |
| pecap | 77 | |
| ident | 98 | |
| privoxy | 101 | |
| radvd | 75 | |
| fax | 78 | |
| slocate | 21 | |
| wnn | 49 | |

Table 6-2. Standard Groups

# 6.4. User Private Groups

Red Hat Linux uses a user private group (UPG) scheme, which makes UNIX groups easier to manage.
A UPG is created whenever a new user is added to the system. A UPG has the same name as the user for which it was created and that user is the only member of the UPG.

UPGs makes it safe to set default permissions for a newly created file or directory which allow both the user and that user's group to make modifications to the file or directory.
The setting determining what permissions are applied to a newly created file or directory is called a umask and is configured in the /etc/bashrc file. Traditionally, on UNIX systems the umask is set to 022, which allows only the user who created the file or directory to make modifications. Under this scheme, all users, including members of the creator's group are not allowed to make any modifications. However, under the UPG scheme, this "group protection" is not necessary since every user has their own private group.

# 6.4.1. Group Directories

Many IT organizations create a group for each major project and then assign people to the group if they need to access that project's files. Using this traditional scheme, managing files has been difficult when someone creates a file, it is associated with the primary group to which they belong. Using the UPG scheme, groups are automatically assigned to files created within a directory with the setgid bit set, which makes managing group projects that share a common directory very simple.

Lets say, for example, that a group of people work on files in the /usr/lib/emacs/site-lisp/; some are trusted to modify the directory but certain not everyone. First create an emacs group, as in the following command:

```
/usr/sbin/groupadd emacs
```

In order to associate the contents of the directory with the emacs group, type:

```
chown -R root.emacs /usr/lib/emacs/site-lisp
```

Now, it is possible to add the proper users to the group with the gpasswd command: