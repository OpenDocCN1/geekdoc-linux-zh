| Command | Description |
| --- | --- |
| rpm -qa | List all installed packages |
| rpm -qf <filename> | Determine the (installed) package that <filename> belongs to |
| rpm -Uhv <package.rpm> | Update/install the file package.rpm showing a progress bar |
| rpm -F -v ./*.rpm | Update (freshen) all installed packages using the RPM files in the current directory |
| rpm --help | Get help about the different options and parameters |

More information and options about RPM can be found in the manual page (man rpm), and in the RPM how-to http://www.rpm.org. You can also display a short overview by running rpm --help.

# 3.3 User administration

Linux is a multi-user operating system. To differentiate between the various users, each has to log in with a unique user name and password. Each user belongs to a primary user group, but he can be a member of other groups (up to 16 groups). Each user name is associated with a user ID (UID), which is unique throughout the system. The same applies to user group names and group IDs (GIDs).

Usually each user has a personal home directory. This is space on the file system (usually a directory below /home, for example /home/username) which belongs to him and where he can store his files (for example, e-mail or text documents). Other users generally have no access to the files stored there.

It is one of the root user's tasks to add and remove user or group accounts. To do this from a menu you can use the program Linuxconf to add, modify or delete groups and users. In the next section we will provide details about user administration from the command prompt.

You should carefully consider adding user groups before adding users. Sometimes there are concerns about restricting access to some parts of the user system. You can do this by creating separate user groups to control access to various files and file systems. Also if you are going to be creating a system with many users, you should consider creating separate groups