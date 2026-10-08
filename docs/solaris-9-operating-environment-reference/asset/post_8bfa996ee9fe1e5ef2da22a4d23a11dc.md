
# 922

# newform

castle% kookaburra-1

- 1. Kookaburra sits in the old gum tree
2. Merry merry king of the bush is he.
3. Laugh, kookaburra, laugh, kookaburra
4. Gay your life must be.

- 5. Kookaburra sits in the old gum tree
6. Eating all the gumdrops he can see.
7. Stop, kookaburra, stop, kookaburra
8. Leave some there for me.

- 9 castle% newform -s kookaburra-1

Kookaburra sits in the old gum tree.
Merry merry king of the bush is he. 2.
Laugh, kookaburra, laugh, kookaburra. 3.
Gay your life must be. 4.

- 5. Kookaburra sits in the old gum tree. 6.
Eating all the gumdrops he can see. 7.
Stop, kookaburra, stop, kookaburra. 8.
Leave some there for me. 9.

castle%

# Exit Status

- 0 Successful operation.
1 Operation failed.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNMesu |

# See Also

```
csplit(1), tabs(1), fspec(4), attributes(5)
```

# Diagnostics

All diagnostics are fatal.

```
usage:...
```

```
newform was called with a bad option.
```

```
"not -s format"
```

```
There was no Tab on one line.
```

```
"can't open file"
```

```
Self-explanatory.
```

# newgrp 923

"internal line exceeds too long"

A line 512 characters after being expanded in the internal work buffer.

"tabspec in error"

A Tab specification is incorrectly formatted, or specified Tab stops are not ascending.

"tabspec redirection illegal"

A tabspec read from a file (or standard input) may not contain a tabspec referencing another file (or standard input).

# newgrp — Log In to a New Group

# Synopsis

/usr/bin/newgrp [- | -1] [group]

sh

newgrp [argument]

ksh

*

newgrp [argument...]

# Description

Use the newgrp command to log in to a new group by changing your real and effective group ID. You remain logged in and the current directory is unchanged. The execution of newgrp always replaces the current shell with a new shell if the command terminates with an error (unknown group).

Any variable that is not exported is reset to null or its default value. Exported variables retain their values. System variables (such as PS1, PS2, PATH, and HOME) are reset to default values unless they are exported by the system or the user. For example, when you have a primary prompt string (PS1) other than $ (default) and have not exported PS1, your PS1 is set to the default prompt $, if newgrp terminates with an error.

> Note — The shell command export (sh(1) and set(1)) is the method to export variables so that they retain their assigned value when invoking new shells.

With no operands and options, newgrp changes your group IDs (real and effective) back to the group specified in your password file entry. This way, you can exit the effect of an earlier newgrp command.

A password is demanded if the group has a password and you are not listed in /etc/group as being a member of that group.

> Note — The only way to create a password for a group is to use passwd(1), then cut and paste the encrypted password from /etc/shadow to /etc/group. passwords are antiquated and not often used.

# Bourne Shell

Equivalent to exec newgrp argument, where argument represents the options or operand of the newgrp command.

# K Shell

Equivalent to exec /bin/newgrp argument where argument represents the options or operand of the newgrp command.

For the newgrp command, ksh(1) commands that are preceded by one or two asterisks (*) are treated specially in the following ways:

- * Variable assignment lists preceding the command remain in effect when the command completes.
- * I/O redirections are processed after variable assignments.
- * Errors cause a script that contains them to abort.
- * Words that follow a command by ** and are in the format of a variable assignment are expanded with the same rules as a variable assignment. This means that tilde substitution is performed after the sign =, and word splitting and file-name generation are not performed.

# Options

-1 | Change the environment to what would be expected if the user actually logged in again as a member of the new group.

# Operands

group A name from the group database or a nonnegative numeric group ID. Specify the group ID used to set the real and effective group IDs. If group is a nonnegative numeric string and exists in the group database as a group name (see getgrp(3C)), use the numeric group ID associated with that group name as the group ID.

argument sh and ksh only. Options and/or operand of the newgrp command.

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of newgrp: LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status

newgrp succeeds in creating a new shell environment, whether or not the group identification was changed successfully, the exit status is the exit status of the shell. Otherwise, the following exit value is returned.

```
>0
An error occurred.
```

# Files

/etc/group System file.
/etc/passwd password file.
/news

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwcs |

# See Also

ksh(1), login(1), set(1), sh(1), getgrnam(3), group(4), passwd(4), attributes(5), environ(5)

# news — Print News Items

# Synopsis

/usr/bin/news [-a] [-n] [-s] [items]

# Description

Use news to keep informed of current events. The news command consults var/news directory for information about current events. By convention, these events are described by files in the directory /news. When invoked without arguments, news prints the contents of all files in news, most recent first, each preceded by an appropriate header. news stores the currency time as the modification date of a file named .news_time in the home directory (the identity of this directory is determined by the environment variable HOME); only files more recent than this time are considered.

# Options

-a Print all items, regardless of currency. In this case, the stored item is not changed.
-n Report the names of the current items without printing their contents and changing the stored item.
-s Report how many current items exist, without printing their names or contents without changing the stored item. It is useful to include such an invocation of news in your .profile file or in the system /etc/profile. All other arguments are assumed to be specific items to be printed. If you press the Delete key during the printing of news item, printing stops and the next item is started. Another delete within one second of the first terminates the program.

# Examples

The following example displays one item.

```
example@ news (root) Thu Mar 18 14:46:34 1999
```

You can display all items using the -a option, as shown in the following example.

```
example@ news -a
(root) Thu Mar 18 14:46:34 1999
Today the U.S. Market broke the 10,000 barrier.
```

You can display individual items by name by typing the name of the article as an argument to news, as shown in the following example.

```
example@ news stocknews
(root) Thu Mar 18 14:46:34 1999
Today the U.S. Market broke the 10,000 barrier.
```

# newsp — Front Ends to the Text Pretty Print Filter

# Synopsis

/bin/newsp [options] filename...

# Description

See mail(1).

# newtask — Create New Task

# Synopsis

newtask [-Fl] [-p project] [command...]

# Description

The newtask command, new in the Solaris 8 Operating Environment, is a part of the project management capability that you can administer with the Solaris Management Console (SMC) and Projects tool, which is new in the Solaris 9 release. The project management tools enable you to track and manage system resource with the /etc/projects database in the environment or the project tables in an NIS or LDAP environment. Use the newtask command to execute the user's default shell or a specified command executing the executed command in a new task owned by the specified project. The user's default shell is the one specified in passwd database and is determined by getpwnam(). When extended accounting is active, the newtask command may additionally create a task accounting record marking the completion of the preceding system task.

# Options

-F Create a finalized task within which further newtask or settaskid(2) invocations fail. Finalized tasks are useful at some sites for simplifying the attribution of resource consumption.
-l Change the environment to what would be expected if the user actually logged in as a member of the new project.
-p Change the project ID of the new task to that associated with the given project name. The invoking user must be a valid member of the requested project for the command to execute. If you specify no project name, start the new task in the invoking user's current project.
-v Display the system task ID as the new system task is begun.

# Operands

- project The project that is charged the resource usage by the created task. The requested project must be defined in the project databases defined in switch.conf(4).
- command The command to be executed as the new task. If you specify no command, the user's login shell is invoked. (If the login is not available, /bin/sh is invoked).

# Examples

The following example creates a new shell in the canada project, displaying the task ID.

```
example$ id -p uid=565(gh) gid=10(staff) projid=10(default)
example$ newtask -v canada
38
```

```
example$ id -p
uid=565(gh) gid=10(staff) projid=82(canada)
example$
```

The following example runs the date command in the russia command.

```
example$ newtask -p russia canada
Tue Aug 31 11:12:10 PDT 1999
example$
```

# Exit Status

- 0 Successful execution.
