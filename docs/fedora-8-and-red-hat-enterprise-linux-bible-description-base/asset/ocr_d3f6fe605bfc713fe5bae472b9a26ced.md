Notice that this listing says that `test` is a directory (`d`), the owner is `chris`, the group is `sales`, and the file was most recently modified on Jan 24 at 12:17 p.m. Suppose that you want to prevent everyone else who uses this computer from using or viewing the files in this directory. The permissions for the directory are `rwxr-x--x`. I explain what these permissions mean later in this section.

**NOTE:** When you add a new user in Fedora or RHEL, by default, the user is assigned to a group of the same name. For example, in the preceding text, the user `chris` would be assigned to a group `chris`. This approach to assigning groups is referred to as the *user private group* scheme. For more information on user private groups, refer to Chapter 11.

+   1. For now, type the following:
+      `$ chmod 700 test`
+   
+      This step changes the permissions of the directory to give you complete access and everyone else no access at all. (The new permissions should read like `rwx------`. ) (See the “Understanding file permissions” section later in this chapter for more information on permissions.)
+   2. Make the `test` directory your current directory as follows:
+      `$ cd test`

# # Identifying Directories

When you need to identify your home directory on a shell command line, you can use the following:
* `$HOME` — This environment variable stores your home directory name.
* `~` — The tilde (~) represents your home directory on the command line.

You can also use the tilde to identify someone else’s home directory. For example, `~chris` would be expanded to the chris home directory (probably `/home/chris`).

Other special ways of identifying directories in the shell include the following:
* `.` — A single dot (.) refers to the current directory.
* `..` — Two dots (..) refers to a directory directly above the current directory.
* `$PWD` — This environment variable refers to the current working directory.
* `$OLDPWD` — This environment variable refers to the previous working directory before you changed to the current one.