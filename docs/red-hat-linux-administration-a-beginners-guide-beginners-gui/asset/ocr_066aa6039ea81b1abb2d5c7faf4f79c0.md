+   5. The applications staff members are **jwang**, **dgranda**, and **iwilnikka**.

+   6. The sales staff consists of **dnneni**, **pvenet**, and **kmadsen**.

+   7. Each executive is also a member of one of the other groups. The research group is headed by **pcedood**. The applications group is headed by **rolson**. The sales group is headed by **cbenfield**.

+   8. Determine the groups that no longer exist, and delete them.

+   9. Determine the users who no longer exist, and delete them.

+   10. Add new groups and users.

+   11. Ensure that each user is a member of the correct primary and secondary groups.

# Project Summary

There’s not much different about the process of organizing users and groups once you know where they belong. In a real reorganization, unfortunately, there tend to be misunderstandings, unspoken assumptions, and other communications and planning problems that muddy the process somewhat. On the technical side, you should also be aware of the ramifications of deleting users and groups who owned files on the system. Learn more about that in the section called “Handle Orphaned Files.”

# CRITICAL SKILL
**5.4**
Running Programs as Other Users

Normally, when a program is run by a user, it inherits all of the rights (or lack thereof) that the user has. If the user can’t read the **/var/log/messages** file, neither can the program. Note that this permission can be different from the permissions of the user who owns the program file (usually called *the binary*). For example, the **ls** program (which is used to generate directory listings) is owned by the root user. Its permissions are set such that all users of the system can run the program. Thus, if the user **rwhte** runs **ls**, that instance of **ls** is bound by the permissions granted to the user **rwhte**, not **root**.

# SetUID and SetGID Programs

However, there is an exception. Programs can be tagged with what’s called a *SetUID bit*, which allows a program to be run with permissions from the program’s owner, not the user who is running it. Using **ls** as an example again, setting the *SetUID* bit on it and having the file owned by **root** means that if the user **rwhte** runs **ls**, that instance of **ls** will run with root permissions, not with **rwhte**’s permissions. The *SetGID bit* works the same way, except instead of applying to the file’s owner, it is applied to the file’s group setting.