# **LPI sudoers: Configuring sudo**

As installed, **sudo** is not as secure and robust as it can be if you configure it carefully. The **sudo** configuration file is */etc/sudoers*. You can edit this file to give specific users the ability to run only certain commands with **root** privileges as opposed to any com- mands. You can also limit these users to running commands only with certain options or arguments. Or you can set up **sudo** so a specific user cannot use a specific option or argument when running a command with **root** privileges.

The best way to edit *sudoers* is to use **visudo** by giving the command: `su -c visudo` or `sudo visudo`. The **visudo** utility locks, edits, and checks the grammar of the *sudoers* file. By default, **visudo** calls the *vi* editor. You can set the **VISUAL** or **EDITOR** env- ironment variable to cause **visudo** to call a different editor. The following command causes **visudo** to use the **nano** editor (page 270):

```
$ export EDITOR=$(which nano)
```

Replace **nano** with the textual editor of your choice. Put this command in a start-up file (page 329) to set this variable each time you log in.

# Always use **visudo** to edit the *sudoers* file

> A syntax error in the *sudoers* file can prevent you from using **sudo** to gain **root** privileges. If you edit this file directly (without using **visudo**), you will not know that you introduced a syntax error until you find that you cannot use **sudo**. The **visudo** utility checks the syntax of *sudoers* before it allows you to exit. If it finds an error, it gives you the choice of fixing the error, exiting without saving the changes to the file, or saving the changes and exiting. The last choice is usually a poor one, so **visudo** marks it with **(DANGER!)**.

In the *sudoers* file, comments, which start with a hashtag (#), can appear anywhere on a line. In addition to comments, this file holds three types of entries: user privilege specifications, aliases, and defaults. Each of these entries occupies a line. You can continue a line by terminating it with a backslash (\).

# **USER PRIVILEGE SPECIFICATIONS**

The format of a line that specifies user privileges is as follows (the whitespace around the equal sign is optional). In each case,

```
user_list host_list = [(runas_list)] command_list
```

+   - The *user_list* specifies the user(s) this specification line applies to. This list can contain usernames, groups (prefixed with %), and user aliases (next section). You can use the builtin alias ALL to cause the line to apply to all users.
+   - The *host_list* specifies the host(s) this specification line applies to. This list can contain one or more hostnames, IP addresses, or host aliases (next section). You can use the builtin alias ALL to cause the line to apply to all systems that refer to this *sudoers* file.
+   - The *runas_list* specifies the user(s) the commands in the *command_list* can be run as when **sudo** is called with the **–u** option (page 432). This list