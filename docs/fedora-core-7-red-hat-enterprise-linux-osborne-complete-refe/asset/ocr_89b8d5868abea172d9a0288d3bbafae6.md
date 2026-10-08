collected into groups. For example, all the users for a given class or project could be formed into a group by the system administrator. A user can grant access to a file to the members of a designated group. Finally, you can also open up access to a file to all other users on the system. In this case, every user not part of the file's group could have access to that file. In this sense, every other user on the system makes up the *others* category. If you want to give the same access to all users on your system, you set the same permissions for both the group and the others. That way, you include both members of the group (group permission) and all those users who are not members (others permission).

# Read, Write, Execute Permissions

Each category has its own set of read, write, and execute permissions. The first set controls the user's own access to his or her files—the owner access. The second set controls the access of the group to a user's files. The third set controls the access of all other users to the user's files. The three sets of read, write, and execute permissions for the three categories—owner, group, and other—make a total of nine types of permissions.

The `ls` command with the `-1` option displays detailed information about the file, including the permissions. In the following example, the first set of characters on the left is a list of the permissions set for the `mydata` file:

```
```
$ ls -1 mydata
-rw-r--r-- 1 chris weather 207 Feb 20 11:55 mydata
```
```

An empty permission is represented by a dash, -. The read permission is represented by **r**, write by **w**, and execute by **x**. Notice there are ten positions. The first character indicates the file type. In a general sense, a directory can be considered a type of file. If the first character is a dash, a file is being listed. If the first character is **d**, information about a directory is being displayed.

The next nine characters are arranged according to the different user categories. The first set of three characters is the owner's set of permissions for the file. The second set of three characters is the group's set of permissions for the file. The last set of three characters is the others' set of permissions for the file.

# Permissions on GNOME

On GNOME, you can set a directory or file permission using the Permissions panel in its Properties window (see Chapter 6). Right-click the file or directory entry in the file manager window and select Properties. Then select the Permissions panel. Here you will find Access pop-up menus for Owner, Group, and Other where you can set Read, Write, and Execute permissions. You can specify the group you want access provided to from the Group drop-down menu. This displays the groups a user belongs to. The root user can change the owner of the file, listing all possible users from the Owner pop-up menu. You can even change the SELinux security context for the file or directory.

# chmod

You use the `chmod` command to change different permission configurations. `chmod` takes two lists as its arguments: permission changes and filenames. You can specify the list of permissions in two different ways. One way uses permission symbols and is referred to as