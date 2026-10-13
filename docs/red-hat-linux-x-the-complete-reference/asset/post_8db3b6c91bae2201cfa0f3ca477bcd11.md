
## Managing Groups

You can manage groups using either shell commands or window utilities like the Red Hat User Manager.

### /etc/group and /etc/gshadow

The system file that holds group entries is called /etc/group. The file consists of group records, with one record per line and its fields separated by colons. A group record has four fields: a group name, a password, its ID, and the users who are part of this group. The Password field can be left blank. The fields for a group record are as follows:

- **Group name** The name of the group, which must be unique
- **Password** With shadow security implemented, this field is an **x**, with the password indicated in the /etc/gshadow file.
- **Group ID** The number assigned by the system to identify this group
- **Users** The list of users that belong to the group, separated by commas

Here is an example of an entry in an /etc/group file. The group is called engines, the password is managed by shadow security, the group ID is 100, and the users who are part of this group are chris, robert, valerie, and aleina.

```
engines:x:100:chris,robert,valerie,aleina
```

As in the case of the /etc/passwd file, it is best to change group entries using a group management utility like groupmod, groupadd, or the Red Hat User Manager. All users have read access to the /etc/group file. With shadow security, secure group data such as passwords are kept in the /etc/gshadow file, to which only the root user has access.

### User Private Groups

A new user can be assigned to a special group set up for just that user and given the user's name. Thus the new user dylan is given a default group also called dylan. The group dylan will also show up in the listing of groups. This method of assigning default user groups is called the User Private Group (UPG) scheme. UPG is currently used on Red Hat systems. The supplementary groups are additional groups that the user may want to belong to. Traditionally, users were all assigned to one group named users that would subject all users to the group permission controls for the users group. With UPG, each user has its own group, with its own group permissions.

### Group Directories

As with users, you can create a home directory for a group. To do so, you simply create a directory for the group in the /home directory and change its group to that of the group, along with allowing access by any member of the group. The following example creates a directory called engines and changes its group to that of the engines group:

```
mkdir /home/engines
chgrp engines /home/engines
```

Then the read, write, and execute permissions for the group level should be set with the chmod command, discussed later in this chapter:

```
chmod g+rwX /home/engines
```

change it, and execute lets them run it (used for scripts and programs). The following example first changes the group for the mymodel file to engines. Then it copies the mymodel file to the /home/engines directory and sets the group read and write permission for the engines group.

```
$ chgrp engines mymodel
$ cp mymodel /home/engines
$ chmod g+rw /home/engines/mymodel
```

### Managing Groups with the Red Hat User Manager

You can add, remove, and modify any groups easily with the Red Hat User Manager. First, access the Red Hat User Manager by clicking the Users & Groups icon in the System Settings window, listed in the Start Here window. Then click the tabbed panel labeled Groups in the Red Hat User Manager window. This will list all your current groups. There will be three fields for each entry: Group Name, Group ID, and Group Members.

To add a group, just click the Add Group button. This opens a small window where you can enter the group name. The new group will be listed in the User Manager's Groups listing. To add users as members of the group, select the group's entry and click the Properties button. This opens a window with tabbed panels for Group Data and Group Users. The Group Users panel lists all current users with check boxes. Click the check boxes for the users you want to be members of this group. If you want to remove a user as member, click the check box to remove its check. Click OK to effect your changes. If you want to remove a group, just select its entry in the User Manager's Groups panel and then click the Delete button.

### Managing Groups Using groupadd, groupmod, and groupdel

You can also manage groups with the groupadd, groupmod, and groupdel commands. These command line operations let you quickly manage a group from a terminal window.

#### groupadd and groupdel

With the groupadd command, you can create new groups. When you add a group to the system, the system places the group's name in the /etc/group file and gives it a group ID number. If shadow security is in place, changes are made to the /etc/gshadow file. The groupadd command only creates the group category. You need to add users to the group individually. In the following example, the groupadd command creates the engines group:

```
# groupadd engines
```

You can delete a group with the groupdel command. In the next example, the engines group is deleted:

```
# groupdel engines
```

#### groupmod

You can change the name of a group or its ID using the groupmod command. Enter groupmod -g with the new ID number and the group name. To change the name of a group, you use the -n option. Enter groupmod -n with the new name of the group, followed by the current name. In the next example, the engines group has its name changed to trains:

```
# groupmod -n trains engines
```

## Controlling Access to Directories and Files: chmod

Each file and directory in Linux contains a set of permissions that determine who can access them and how. You set these permissions to limit access in one of three ways: You can restrict access to yourself alone, you can allow users in a predesignated group to have access, or you can permit anyone on your system to have access. You can also control how a given file or directory is accessed.

### Permissions

A file or directory may have read, write, and execute permissions. When a file is created, it is automatically given read and write permissions for the owner, enabling you to display and modify the file. You may change these permissions to any combination you want. A file could also have read-only permission, preventing any modifications.

### Permission Categories

Three different categories of users can have access to a file or directory: the owner, the group, an all others not belonging to that group. The owner is the user who created the file. Any file you create, you own. You can also permit a group to have access to a file. Often, users are collected into groups. For example, all the users for a given class or project could be formed into a group by the system administrator. A user can grant access to a file to the members of a designated group. Finally, you can also open up access to a file to all other users on the system. In this case, every user not part of the file's group could have access to that file. In this sense, every other user on the system makes up the "others" category. If you want to give the same access to all users on your system, you set the same permissions for both the group and the others. That way, you include both members of the group (group permission) and all those users who are not members (others permission).

### Read, Write, Execute Permissions

Each category has its own set of read, write, and execute permissions. The first set controls the user's own access to his or her files-the owner access. The second set controls the access of the group to a user's files. The third set controls the access of all other users to the user's files. The three sets of read, write, and execute permissions for the three categories-owner, group, and other-make a total of nine types of permissions.

The ls command with the -l option displays detailed information about the file, including the permissions. In the following example, the first set of characters on the left is a list of the permissions set for the mydata file:

```
$ ls -l mydata
-rw-r--r-- 1 chris weather 207 Feb 20 11:55 mydata
```

An empty permission is represented by a dash, -. The read permission is represented by r, write by w, and execute by x. Notice there are ten positions. The first character indicates the file type. In a general sense, a directory can be considered a type of file. If the first character is a dash, a file is being listed. If the first character is d, information about a directory is being displayed.

The next nine characters are arranged according to the different user categories. The first set of three characters is the owner's set of permissions for the file. The second set of three characters is the group's set of permissions for the file. The last set of three characters is the other users' set of permissions for the file.

### Permissions on GNOME

On GNOME, you can set a directory or file permission using the Permissions panel in its Properties window. Right-click the file or directory entry in the file manager window and select Properties. Then select the Permissions panel. Here you will find a table of boxes with columns for Read, Write, and Execute along with rows for Owner, Group, and Other. Check the appropriate box for the permission you want. Normally, the Read and Write boxes for owner permission will already be set. You can specify the group you want access
