# TOPIC D

# Set Advanced Permissions

Now that you have modified file and directory ownership, you can set advanced permissions for users. There may be instances when you have to use special permissions to enable users to access files or directories. In this topic, you will set advanced permissions.

While it is desirable to allow only users with root or administrative permissions to execute certain commands, sometimes other users need to be able to issue them. Setting advanced permissions will allow other users to execute and maintain system utilities so that the Linux+ administrator does not have to. This will save the administrator time and effort.

# Special Permissions

Special permissions are used when normal permissions become inadequate, usually in the case of processes. Through special permissions, less privileged users are allowed to execute a file that can usually be run only by the root user. Set User ID (SUID), or setuid, is the permission that allows a user who executes a file to have similar permissions as the owner of the file. Set Group ID (SGID), or setgid, is the permission that allows a user who executes a file to have similar permissions as the group owner of the file.

![](bbox=[0.78, 0.33, 0.9, 0.39])

# The SUID and SGID Permissions

The SUID and SGID commands are powerful tools that enable users to perform tasks without problems that could arise with users having the actual permissions of that group or user. However, these can be dangerous tools too.

While changing the permissions of a file to be either SUID or SGID, the following points should be considered:

+   *   Use the lowest permissions needed to accomplish a task. It is recommended not to give a file the same SUID or SGID as the root user. A user with fewer privileges often can be configured to perform the task.
*   Watch for back doors. If the user runs a program with the SUID set to root, then the user retains root as the effective UID when the user goes through the back door. The following can be used as back doors:
    *   Programs that enable you to shell out.
    *   Programs with multiple entrances and exits.

# The chattr Command

The chattr command is used to change the attributes of a file on a Linux filesystem.

![](bbox=[0.78, 0.74, 0.9, 0.8])

The following table lists the description for the options used in the syntax of the chattr command.

| Command Option | Used To |
| :--- | :--- |
| `-R` | Recursively change the attributes of directories and their contents. |