+   -  chgrp—Changes the group ownership of a file or directory.
+   -  chown—Changes the owner of a file or directory.
+   -  chmod—Changes the access permissions of a file or directory.

These commands, which modify file ownerships and permissions, can be used to model organizational structure and permissions in the real world of your Fedora system (see the next section, “Managing Groups”). For example, a human resources department can share health-benefit memos to all company employees by making the files readable (but not writable) by anyone in an accessible directory. On the other hand, programmers in the company’s research and development section, while being able to access each other’s source code files, would not have read or write access to HR pay-scale or personnel files (and certainly would not want HR or Marketing poking around R&D).

These commands are used to manage group and file ownerships and permissions from the command line. Use the chgrp command to allow (or restrict) groups of users access to specific directories and files. The chown command can be used to set ownerships, but may only be used by root. Use the chmod command to set read and write permissions for files you own. Refer to Chapter 5 of this book or the man page of each command for details on these commands.

# User Stereotypes

As is the case in many professions, exaggerated characterizations (stereotypes or caricatures) have emerged for users and system administrators. Many stereotypes contain elements of truth mixed with generous amounts of hyperbole and humor and serve to assist us in understanding the characteristics of and differences in the stereotyped subjects. The stereotypes of the “luser” and the “BOFH” (users and administrators, respectively) also serve as cautionary tales describing what behavior is acceptable and unacceptable to the computing community.

Understanding these stereotypes allows you to better define the appropriate and inappropriate roles of system administrators, users, and others. The canonical reference to these terms is found in the alt.sysadmin.recovery FAQ found at http://www.ctrl-c.liu.se/~ingvar/asr/overview.html.

# Managing Groups

Groups establish relationships among users in which they share a common set of permissions. An individual cannot read or write to a file owned by another user. But if users are in the same group, they may both read and write to files owned by the group (depending on the group permissions) while retaining the privacy and security of their own files.

Group permissions can be used to facilitate group work on a project involving common files and to control access to devices such as the modem and floppy drive. This approach also represents a secure method of limiting access to system resources to only those users who need them. As an example, the sysadmin could put the users andrew, paul, damon,