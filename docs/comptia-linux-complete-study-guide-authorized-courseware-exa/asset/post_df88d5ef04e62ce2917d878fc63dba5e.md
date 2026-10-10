
Add users The `-M user[,...]` option works like `-A`, but it also adds the specified user(s) to the list of group members.

If entered without any parameters except a group name, `gpasswd` changes the password for the group. Group passwords enable you to control temporary membership in a group, as granted by `newgrp`. Ordinarily, members of a group may use `newgrp` to change their current group membership (affecting the group of files they create). If a password is set, even those who aren’t members of a group may become temporary group members; `newgrp` prompts for a password that, if entered correctly, gives the user temporary group membership. Unfortunately, some of these features aren’t implemented correctly in all distributions. In particular, password entry by non-group members sometimes does not give group membership—the system responds with an access denied error message. The `-R` option also sometimes doesn’t work correctly—group members whose primary group membership is with another group may still use `newgrp` to set their primary group membership.

## Directly Modifying Group Configuration Files

Group information is stored primarily in the `/etc/group` file. Like account configuration files, the `/etc/group` file is organized as a set of lines, one line per group. A typical line in this file resembles the following:

```
project1:x:501:sally,sam,ellen,george
```

Each field is separated from the others by a colon. The meanings of the four fields are as follows:

- **Group name**: The first field (`project1` in the preceding example) is the name of the group.
- **Password**: The second field (`x` in the preceding example) is the group password. Distributions that use shadow passwords typically place an `x` in this field; others place the encrypted password directly in this field.
- **GID**: The group ID number (in this example’s case, `501`) goes in this field.
- **User list**: The final field is a comma-separated list of group members.

Users may also be members of a group based on their own `/etc/passwd` file primary group specification. For instance, if user `george` has `project1` listed as his primary group, he need not be listed in the `project1` line in `/etc/group`. If user `george` uses `newgrp` to change to another group, though, he won’t be able to change back to `project1` unless he’s listed in the `project1` line in `/etc/group`.

Systems with shadow passwords also use another file, `/etc/gshadow`, to store shadow password information about groups. This file stores the shadow password and information for group administrators, as described earlier in “Using gpasswd.”

> If you configure Linux to use a network account database, the `/etc/group` file is present and may define groups important for the system’s basic operation. As with `/etc/passwd` and `/etc/gshadow`, though, important user groups are likely to be defined only on the network account server, not in `/etc/group`.

### Deleting Groups

Deleting groups is done via the `groupdel` command, which takes a single parameter: a group name. For instance, `groupdel project3` removes the `project3` group. You can also delete a group by editing the `/etc/group` file (and `/etc/gshadow`, if present) and removing the relevant line for the group. It's generally better to use `groupdel`, because `groupdel` checks to see if the group is any user's primary group. If it is, `groupdel` refuses to remove the group; you must change the user's primary group or delete the user account first.

As with deleting users, deleting groups can leave orphaned files on the computer. You can locate them with the `find` command, which is described in more detail in Chapter 4. For instance, if a deleted group used a GID of `503`, you can find all the files on the computer with that GID by using the following command:

```
# find / -gid 503
```

Once you've found any files with the deleted group's ownership, you must decide what to do with them. In some cases, leaving them alone won't cause any immediate problems; but if the GID is ever reused, it can lead to confusion and even security breaches. Therefore, it's usually best to delete the files or assign them other group ownership using the `chown` or `chgrp` command.

## Tuning User and System Environments

Text-mode user environments are controlled through shell configuration files. For bash, these files include `/etc/profile`, `/etc/bash.bashrc`, `~/.profile`, `~/.bashrc`, `~/.bash_profile`, and `~/.profile`. The files in `/etc` are global configuration files, which affect all users; those in users' home directories (which are usually copied from the skeleton directory at account creation, as described earlier) affect individual users' accounts and can be customized by individual users. These files control the various bash options, including environment variables—named variables that hold data for the benefit of many programs. For instance, you might set the `EDITOR` environment variable to the name of your favorite text editor. Some (but not all) programs that launch editors pay attention to this environment variable and launch the editor you specify.

As a system administrator, you can change the system-wide bash configuration files to add, remove, or change the environment variables that all users receive. Generally speaking, you should do so because the documentation for a specific program indicates that it uses particular environment variables. You can also see all your current environment variables by typing `env`. (The list is rather long, so you may want to pipe it through `less`, as in `env | less`.)

In addition to setting default environment variables and otherwise modifying users' text-mode login environment by adjusting their bash configuration files, you can adjust the default set of files created by `useradd`. As described earlier, in “Adding Users,” `useradd` copies files from the skeleton directory (`/etc/skel` by default) into a newly created home directory. Typically, `/etc/skel` contains a handful of user configuration files, such as `.bashrc`. You can add files (and even directories) to this directory, including user configuration files, a starting directory tree, a `README` file for new users, and anything else you like. Because these files are copied into users’ home directories and users are given ownership of the copies, the users can read, change, and even delete their copies of these files. Thus, you shouldn’t place any options in these files that are sensitive from a security point of view or that users should not be able to change. (In truth, entries you place in global bash configuration files can easily be overridden by individual users, as well.) Also, be aware that any changes you make to the global files won’t automatically be moved into existing users’ copies of these files; changes will affect only the files received by new users. This fact makes the global files (such as `/etc/profile`) preferable to `/etc/skel` for any changes to system defaults you want to implement system-wide, particularly if you expect you’ll ever want to modify your changes.

> Various programs set environment variables themselves, and some are maintained automatically by bash. For instance, bash maintains the *PWD* environment variable, so you shouldn’t try to set it in a configuration script. Also, be aware that adjusting the bash configuration files only affects bash. If a user’s default shell is something else, or if a user doesn’t use a text-mode shell (say, if the user logs into X and launches programs from a GUI menu), setting environment variables in the bash configuration files will do no good.

## Using System Log Files

Linux maintains log files that record various key details about system operation. You may be able to begin using log files immediately, but knowing how to change the log file configuration can also be important. You do this by configuring the *syslogd daemon* (a daemon is a program that runs continuously in the background waiting for an event to trigger it to perform some action). Some servers and other programs perform their own logging and so must be configured independently of *syslogd*. You may even want to configure one computer to send its log files to another system as a security measure. You should also be aware of issues surrounding log file rotation; if your computer doesn’t properly manage existing log files, they can grow to consume all your available disk space, at least on the partition on which they’re stored. In addition to configuring logging, you must be able to use the log files that the system generates.

### Understanding syslogd

Most Linux systems employ a special daemon to handle log maintenance in a unified way. The traditional Linux system logger is *syslogd*, which is often installed from a package called *sysklogd*. The *sysklogd* daemon handles messages from servers and other user-mode programs. It’s usually paired with a daemon called *klogd*, which is generally installed from the same *sysklogd* package as *syslogd*. The *klogd* daemon manages logging of kernel messages.
