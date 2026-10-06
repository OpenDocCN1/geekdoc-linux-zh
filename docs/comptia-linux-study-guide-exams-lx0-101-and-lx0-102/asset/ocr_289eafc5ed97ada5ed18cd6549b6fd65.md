# Deleting Groups

Deleting groups is done via the groupdel command, which takes a single parameter: a group name. For instance, groupdel project3 removes the project3 group. You can also delete a group by editing the /etc/group file (and /etc/gshadow, present) and removing the relevant line for the group. It's generally better to use groupdel, because groupdel checks whether the group is a user's primary group. If it is, groupdel refuses to remove the group; you must change the user's primary group or delete the user account first.

As with users, deleting groups can leave orphaned files on the computer. You can locate them with the find command, which is described in detail in Chapter 4. For instance, if a deleted group used a GID of 1003, you can find all the files on the computer with that GID by using the following command:

```
# find -gid 1003
```

Once you've found any files with the deleted group's ownership, you must decide what to do with them. In some cases, leaving them alone won't cause any immediate problems; but if the ID is ever reused, it can lead to confusion and security breaches. Therefore, it's usually best to delete the files or assign them other group ownership using the chown or chgrp command.

# Tuning User and System Environments

Mode-user environments are controlled through shell configuration files. For bash, these files include /etc/profile, /etc/bashrc, ~/.profile, ~/.bashrc, ~/.bash_profile, and ~/.profile. The files in /etc are global configuration files, which affect all users; those in users' home directories (which are usually copied from the skeleton directory at account creation, as described earlier) affect individual users' accounts and can be customized by users. These files control the bash options, including environment variables—named variables that hold data for the benefit of many programs. For instance, you might set the EDITOR variable to the name of your favorite text editor. Some (but not all) programs that launch pay attention to this environment variable and the editor you specify.

As a system administrator, you can change the system-wide bash configuration files to add, remove, or change the environment variables that all users receive. Generally speaking, you should do so because the documentation for a specific program indicates that it uses particular environment variables. You can also see all your current environment variables by typing env. The list is long, so you may want to pipe it through less, as in env | less.