# Table A.4

# Creating and Editing Files

| COMMAND | DESCRIPTION |
|---|---|
| ed | Choose a line-oriented text editor. |
| emacs | Choose a tremendously powerful, somewhat easy to use text editor. |
| emacs -n | Open emacs and force a terminal-window- (not graphical window-) oriented session. |
| emacs filename | Open emacs and edit filename. |
| joe | Choose a fairly friendly editor. |
| pico | Choose for menu-oriented, user-friendly text editing. |
| pico filename | Open and edit filename in pico. |
| pico -w filename | Disable word wrapping for filename in pico. This is particularly useful for configuration files. |
| vi | Choose a powerful editor with lots of power but little ease of use. |
| vi filename | Open and edit filename in vi. |

# Table A.5

# Controlling File Ownership and Permissions

| COMMAND | DESCRIPTION |
|---|---|
| chgrp | Change the group association of files or directories. |
| chgrp groupname filename | Change the group association of filename to groupname. |
| chgrp -R group directory | Recursively change the group association of directory and all subdirectories and files within it to group. |
| chmod | Change the permissions for a file or directory. |
| chmod a-w file | Remove write permission for file for all (everyone). |
| chmod g+w file | Add write permission for file for the current group. |
| chmod -R go-rwx * | Revoke all permissions from everyone except the user for all files in the current directory and all subdirectories and their contents. |
| chmod u=rwx,g=rx,o=r file | Set the permissions on file to user read, write, and execute, group read and write, and others read. |
| chmod ugo- * | Revoke all permissions for everything in the current directory from everyone. |
| chown | Change the ownership of files or directories. |
| chown -R user directory | Recursively change the ownership of Directory and all contents to user. |
| chown user file | Change the ownership of file to user. |
| umask 022 | Specify the default permissions for all created files. |