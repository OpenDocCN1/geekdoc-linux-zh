
pass a single COMMAND to the shell with -c

-m, --preserve-environment
    do not reset environment variables

-1    a full login simulation for the substituted user,
      the same as specifying the dash alone

You can invoke the su command in different ways that yield diverse results. By using su alone, you can become root, but you keep your regular user environment. This can be verified by using the printenv command before and after the change. Note that the working directory (you can execute pwd as a command line to print the current working directory) has not changed. By executing the following, you become root and inherit root's environment:

```
$ su -
```

By executing the following, you become that user and inherit the super user's environment—a pretty handy tool. (Remember: Inheriting the environment comes from using the dash in the command; omit that, and you keep your “old” environment.) To become another user, specify a different user’s name on the command line:

```
$ su - other_user
```

When leaving an identity to return to your usual user identity, use the exit command. For example, while logged on as a regular user,

```
$ su - root
```

the system prompts for a password:

```
Password:
```

When the password is entered correctly, the root user's prompt appears:

```
#
```

To return to the regular user's identity, just type

```
# exit
```

This takes you to the regular user's prompt:

```
$
```

If you need to allow other users access to certain commands with root privileges, you must give them the root password so that they can use su—that definitely is not a secure solution. The next section describes a more flexible and secure method of allowing normal users to perform selected root tasks.

## Granting Root Privileges on Occasion—The sudo Command

It is often necessary to delegate some of the authority that root wields on a system. For a large system, this makes sense because no single individual will always be available to perform super user functions. The problem is that UNIX permissions come with an all-or-nothing authority. Enter sudo, an application that permits the assignment of one, several, or all of the root-only system commands.

### NOTE

As mentioned earlier, the sudo command is pervasive in Ubuntu, because it is used by default. If you want to get to a root shell, and thereby removing the need to type sudo for every command, just enter sudo -i to get the root prompt. To return to a normal user prompt, enter exit and press Return.

After it is configured, using sudo is simple. An authorized user merely precedes the super user authority-needed command with the sudo command, like so:

```
$ sudo command
```

After getting the user's password, sudo checks the /etc/sudoers file to see whether that user is authorized to execute that particular command; if so, sudo generates a "ticket" for a specific length of time that authorizes the use of that command. The user is then prompted for his password (to preserve accountability and provide some measure of security), and then the command is run as if root had issued it. During the life of the ticket, the command can be used again without a password prompt. If an unauthorized user attempts to execute a sudo command, a record of the unauthorized attempt is kept in the system log and a mail message is sent to the super user.

Three man pages are associated with sudo: sudo, sudoers, and visudo. The first covers the command itself, the second the format of the /etc/sudoers file, and the third the use of the special editor for /etc/sudoers. You should use the special editing command because it checks the file for parse errors and locks the file to prevent others from editing it at the same time. The visudo command uses the vi editor, so you might need a quick review of the vi editing commands found in Chapter 4, "Command Line Quickstart," in the section "Working with vi." You begin the editing by executing the visudo command with this:

```
$ sudo visudo
```

The default /etc/sudoers file looks like this:

```
# /etc/sudoers
#
# This file MUST be edited with the 'visudo' command as root.
```
