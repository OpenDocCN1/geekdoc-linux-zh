
## Part IV: Log In as User geeko and Remove the New User Account

To log in as user geeko and remove the new user account, do the following:

- 1. From the bottom panel, log out by selecting Computer > Logout.
- 2. In the Log Out dialog, select Log Out.
  X Window is restarted and the GUI login screen appears.
- 3. Log in as geeko with a password of novell.
- 4. Start YaST by doing the following:
  a. From the GNOME desktop, select Computer > More Applications > System > YaST.
  b. In the Password Needed dialog, type a password of nov3ll.
  c. Select Continue.
  The YaST Control Center appears.
- 5. Select Security and Users > User Management.
- 6. From the list of users, select tux; then select Delete.
- 7. In the Confirmation dialog, make sure Delete Home Directory /home/tux is selected; then select Yes.
- 8. Select Finish.
- 9. Verify that the user tux has been removed by doing the following:
  a. Start the Nautilus file manager by double-clicking the geeko’s Home icon on the desktop.
  The content of Geeko’s home directory is displayed.
  b. Browse to the /home directory.
  Notice there is only one entry for user geeko.
  c. Browse to the /etc directory.
  d. Open the passwd file by double-clicking on it.
  Notice that the entry for tux has been removed from the end of the file.
  e. Close gedit and the Nautilus window.
- 10. Close the YaST Control Center.

## Part V: Get User and Group Information from the Command-Line

To get the user and group information from a command line, do the following:

- 1. As user geeko, start a terminal emulation from the main menu of the GNOME desktop.
- 2. Switch to user root by entering su - with a password of nov3ll.
- 3. Display all information in the /etc/group file by entering

```bash
less /etc/group
```

- 4. Write down the GIDs of the following groups:
  a. ftp
  b. lp
  c. nobody
  d. root
  e. www
  f. users

- 5. Exit by typing q.

- 6. Display the contents of the /etc/passwd file by entering

```bash
less /etc/passwd
```

- 7. Write down the UIDs of the following groups:
  a. ftp
  b. lp
  c. nobody
  d. root
  e. wwwrun
  f. geeko

- 8. Exit by typing q.

- 9. Display the identity information of the logged-in user by entering

```bash
id
```

Because you have root permissions, you can see UID, GID, and group information for root.

- 10. Switch back to user geeko by entering

```bash
exit
```

- 11. Enter id again.

Notice that the groups displayed for geeko are different from those displayed for root.

- 12. Close the terminal window by entering

```bash
exit
```

## Objective 3—Manage File Permissions and Ownership

You can change the current values associated with ownership and permissions by knowing how to do the following:

- Understand File Permissions
- Change File Permissions with chmod
- Change File Ownership with chown and chgrp
- Modify Default Access Permissions
- Configure Special File Permissions

### Understand File Permissions

You can use the `ls -l` command to display the contents of the current directory along with the assigned permissions for each file or subdirectory.

For example, entering `ls -l my_file` displays the following permissions for my_file:

```text
geeko@da10:~> ls -l my_file
-rw-r--r-- 1 geeko users 0 2006-02-07 19:10 my_file
geeko@da10:~>
```

Look at the first 10 characters of the output (“-rw-r--r--”). The first character (“-”) is not relevant for permissions, because it indicates the type of the file, which can be one of the following:

- - (Normal file)
- d (Directory)
- l (Link)

The remaining nine characters show the file permissions.

You can assign the following permissions to a file or directory:

- *Read (r)*—This permission allows the file to be read or the contents of a directory to be listed.
- *Write (w)*—This permission allows a file to be modified. When set on a directory, it allows files to be created or deleted within the directory.
- *Execute*—This permission allows a file to be executed. When set on a directory, it allows it to change into the directory using the `cd` command.

If a permission is set, the character is shown, otherwise a “-” appears.

The permission characters are grouped (“rwx rwx rwx”):

- *Characters 1 to 3*—Represent the permissions of the file owner.
- *Characters 4 to 6*—Represent the permissions of the owning group.
- *Characters 7 to 9*—Represent the permissions of all other users—those not covered by the previous permissions.

Each file (and directory) can belong to only one user and one group. In the previous example, the name of the file owner (geeko) is shown in the ls output next to the file permissions. The name of the owning group (users) is shown next to the file owner.

You can also view the permissions, owner, and group from the Nautilus file manager. In Nautilus, right-click the icon of the file you want to look at, select **Properties** from the menu, and select the **Permissions** tab. See Figure 9-11.

![](img/9129877170834ca9d5fdac5319bf5f12_305_0.png)

Figure 9-11

From this dialog, you can change the Read and Write permissions for Owner, Group, and Others by selecting the appropriate option.

You can modify the group ownership of the file or directory to other groups you are a member of by selecting the group from the **File group** drop-down list. Only root can change the owner of a file or change the owning group beyond the groups a user is a member of.

### Change File Permissions with chmod

You can use the chmod command to add (“+”) or remove (“−”) permissions. Both the owner of a file and root can use this command.

The following options can be used to change the permissions:

- *u*—Change permissions for the owner (user).
- *g*—Change permissions for the group.
- *o*—Change permissions for others.
- *a*—Change permissions for all (owner, group, and others).

Table 9-2 shows examples of using the command chmod.

| Example | Result |
|---|---|
| `chmod u+x` | The owner is given permission to execute the file. |
| `chmod g=rw` | All group members can read and write. |
| `chmod u=rwx` | The owner receives all permissions. |
| `chmod u=rwx,g=rw,o=r` | All permissions are given for the owner, read and write for the group, read for all other users. |
| `chmod +x` | All users (owner, group, others) receive executable permission (depending on umask). |
| `chmod a+x` | All users (owner, group, others) receive executable permission (a for all). |

Table 9-2

In the following example, the user geeko allows the other members of the group users to write to the hello.txt file by using chmod:

```
geeko@da10:~ > ls -la hello.txt
-rw-r--r-- 1 geeko users 0 2006-04-06 12:40 hello.txt
geeko@da10:~ > chmod g+w hello.txt
geeko@da10:~ > ls -la hello.txt
-rw-rw-r-- 1 geeko users 0 2006-04-06 12:40 hello.txt
```

Using the option -R (recursive) and a specified directory, you can change the access permissions for all directories and files and subdirectories beneath it. Besides using letters (rwx), you can also use the octal way of representing the permission letters with groups of numbers.

Every file and directory in a Linux system has a numerical permission value assigned to it. This value has three digits.

The first digit represents the permissions assigned to the file or directory owner. The second digit represents the permissions assigned to the group associated with the file or directory. The third digit represents the permissions assigned to others.

Each digit is the sum of the following three values assigned to it:

- Read: 4
- Write: 2
- Execute: 1

For example, suppose a file named myfile.txt has 754 permissions assigned to it.

This means the owner of the file has read, write, and execute permissions (4+2+1), the group associated with the file has read and execute permissions (4+1), and others have read permissions (4).

By using number equivalents, you can add the numbers, as shown in Table 9-3.

| Owner | Group | Others |
|---|---|---|
| rwx | r-x |  |
| 4+2+1 (4+2+1=7) | 4+1 (4+1=5) | 4 (4) |

Table 9-3

Table 9-4 shows examples of using numbers instead of letters.

| Example | Result |
|---|---|
| `chmod 754 hello.txt` | All permissions are given for the owner, read and execute for the group, read for all other users (rwx r-x r--). |
| `chmod 777 hello.txt` | All users (user, group, others) receive all permissions (rwx rwx rwx). |

Table 9-4

### Change File Ownership with chown and chgrp

The user root can use the chown command to change the user and group affiliation of a file by using the following syntax:

```
chown new_user.new_group file
```

To change the owner, but not the group, you can use the following command syntax:

```
chown new_user file
```

To change the group, but not the user, you can use the following command syntax:

```
chown .new_group file
```

You can also change the group affiliation of a file with the chgrp command using the following syntax:

```
chgrp new_group file
```

A normal user can use the chown command to allocate a file that he owns to a new group by using the following syntax:

```
chown .new_group file
```

The user can only change the group affiliation of the file that he owns if he is a member of the new group.
