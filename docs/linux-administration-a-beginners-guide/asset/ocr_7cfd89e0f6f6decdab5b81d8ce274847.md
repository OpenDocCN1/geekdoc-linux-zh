# Linux Administration: A Beginner's Guide

**LOG COMMANDS** If you want to log each command entered by users connecting to your FTP service, you want to use log commands. Its usage is as follows:

```
log commands typelist
```

where *typelist* is the comma-separated list of the type of user whose commands you want to log, as described by the *class* command. Valid user types are anonymous, guest, and real. For example, if you want to log all the commands typed by anonymous users, you would type

```
log commands anonymous
```

**LOG TRANSFERS** If you want to log only the files transferred between users and your server instead of all commands typed, you would use this command:

```
log transfers typelist directions
```

where *typelist* is the type of user whose commands you want to log as described by the *class* command (that is, anonymous, guest, and real), and *directions* is a comma-separated list of which direction the transfer must take in order for it to be logged (that is, inbound and outbound). For example, to log all guest users' inbound and outbound connections, type

```
log transfers guest inbound,outbound
```

# Other Server Commands

Of course, there are always the commands that don't really fit into any particular category. Consider the following.

**ALIAS** It is often convenient to create shortcuts to frequently accessed directories. By using the *alias* command, you can do just that. The format of the command is

```
alias alias-name actual-directory
```

where *alias-name* is the alias itself, and *actual-directory* is the full directory that you want to set up a shortcut to. For example,

```
alias redhat /pub/linux/distributions/redhat
```

would allow a user to enter the command

```
cd redhat
```

and have the system automatically take him to the /pub/linux/distributions/redhat directory.