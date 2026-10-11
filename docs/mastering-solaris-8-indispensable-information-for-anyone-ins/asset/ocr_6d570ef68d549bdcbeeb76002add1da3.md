Here is the syntax for the *chown* command:

*chown <options> <username>:<groupname> <filename(s)>*

The *<username>* can be either the logon name or the user identification number (UID) of a user, and similarly, *<groupname>* can be either the group or its group identification number (GID). If you want to change the owner and not the group, you omit *<groupname>* from the command. You must be the root to change the ownership of a file or directory to someone else. Once you have changed the ownership, only the new owner of the object or the system superuser or root can change the ownership attribute. The three options offered by Solaris for *chown* are –f (don't report errors), –R (recursively move through a directory and subdirectory to change ownership), and –h (change the ownership of a symbolic link without changing the ownership of the file to which the link originally points). Of these three options, –R is particularly important and widely used. Therefore, the command *chown –R barries \** gives ownership of all files in the current directory and all files in any subdirectories to *barries*. The *chown* command may be limited in operation when disk quotas are in place; otherwise, this command can be used to defeat disk quotas by reassigning ownership.

The syntax for the *chgrp* command is as follows:

*chgrp <options> <groupname> <filename(s)>*

The *chgrp* command is very similar in operation to the *chown* command. The same three options described previously also apply to the *chgrp* command: –f, –R, and –h. The *chown* command is somewhat limited in what it allows standard users to do. However, the *chgrp* command allows any user to change the group of a file to any group that that user is a member of, which is quite useful.

The command line is not the only place that you can go to view a file or directory's permissions; you can also view and change permissions in the File Manager. For each object in the File Manager, there is a Properties dialog box that displays this information in an easy-to-understand format. In addition to the various permissions, you can also view the current owner and group names and modify the permissions (see Figure 5.3).

To view and modify the permissions for a file or folder, follow these steps:

+   1. Click a file or folder to select it. (You can also press the Tab or arrow keys to move to an object and then press the Spacebar key to select it.)
+   2. Choose the *Properties* command from the Selected menu. (You can also press Ctrl+Backspace.) The Properties dialog box appears.
+   3. Click the permission you want to change. (You can also press the Tab key to move to the permission and then press the Spacebar key to select it.)