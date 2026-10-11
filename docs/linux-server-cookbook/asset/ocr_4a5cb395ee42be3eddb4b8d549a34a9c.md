directories. In contrast, a regular user can only modify the group of files and directories only when the target group is one of the groups they belong to. Table 5.10 shows all the possible syntax options:

| Syntax | Description |
| :--- | :--- |
| `chown user:group file(s)/dir(s)` | Change user and group owners for the specified files and/or directories. |
| `chown user file(s)/dir(s)` | Change the user owner for the specified files and/or directories. |
| `chown user: file(s)/dir(s)` | Same as the previous syntax. |
| `chown :group file(s)/dir(s)` | Change group owner for the specified files and/or directories |

*Table 5.10: Command chown possible syntax*

The user and group can be specified using the name or the **group id**. Old versions of command *chown* were using dot (.) as a separator instead of the colon (:).It is still a valid separator but not recommended to use anymore. The Argument can be a file, directory, or a list of files and/or directories separated by space. The popular options for command *chown* are shown in *table 5.11*:

| Option | Description |
| :--- | :--- |
| -C, --changes | Shows the actions done but only the changes. |
| -v, --verbose | Shows all the actions done as well as the skipped ones. |
| --reference=SOURCE | Copy the owner and group owners from a specified source |
| -R, --recursive | Change all the permissions of all files and subdirectories for the specified directory. |

*Table 5.11: Popular options for command chown*

*Figures 5.12, 5.13*, and 5.14 feature examples using the command **chown**:

+   • Try to change the owner of a file being a regular user:
+   
+   ```
+   agonzalez@ubuntu:~$ ls -l example.txt
+   -rw-rw-r-- 1 agonzalez agonzalez 37 Jul 3 19:27 example.txt
+   agonzalez@ubuntu:~$ chown testuser example.txt
+   chown: changing ownership of 'example.txt': Operation not permitted
+   ```
+   *Figure 5.12: Output example using command chown*

+   • Change the group owner for a file being a regular user: