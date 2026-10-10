You can change passwords *en masse* by redirecting a list of name and password pairs to the command. An appropriate shell script can be constructed with the information gleaned from this chapter.

However, Fedora also provides the `newusers` command to add users in a batch from a text file. This command also allows a user to be added to a group, and a new directory can be added for the user, too.

# # Granting System Administrator Privileges to Regular Users

It may be necessary for regular users to run a command as if they were the root user. They usually do not need these powers, but they might on occasion—for example, to temporarily access certain devices or run a command for testing purposes.

There are two ways to run commands with root privileges: The first is useful if you are the super user and the user; the second if you are not the regular user (as on a large, multiuser network).

# ## Temporarily Changing User Identity with the `su` Command

What if you are also root, but are logged on as a regular user because you are performing nonadministrative tasks and you need to do something that only the super user can do? The `su` command is available for this purpose.

> **NOTE**
> 
> A popular misconception is that the `su` command is short for *super user*; it just means *substitute user*. An important but often overlooked distinction is that between `su` and `su -`. In the former instance, you become that user but keep your own environmental variables (such as `PATH`). In the latter, you inherit the environment of that user. This is most noticeable when you use `su` to become the super user, root. Without appending the `-`, you do not inherit the path variable that includes `/bin` or `/sbin`, so you must always enter the full path to those commands when you just `su` to root.

Because almost all Linux file system security revolves around file permissions, it can be useful to occasionally become a different user with permission to access files belonging to other users or groups or to access special files (such as the communications port `/dev/ttyS0` when using a modem, or the sound device `/dev/audio` when playing a game). You can use the `su` command to temporarily switch to another user identity, and then switch back.