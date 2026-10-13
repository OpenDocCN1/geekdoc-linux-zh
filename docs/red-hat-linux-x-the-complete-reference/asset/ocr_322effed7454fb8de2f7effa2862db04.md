# Configuring Users

Currently, the easiest and most effective way to add new users on Red Hat is to use redhat-config-users, also known as the Red Hat User Manager. You can access it from the GNOME desktop's Start Here window's System Settings window. The redhat-config-users window will display panels for listing both users and groups (see Figure 4-2). A button bar will list various tasks you can perform, including creating new users or groups, editing current ones (Properties), or deleting a selected user or group.

![](bbox=[0.1, 0.3, 0.6, 0.5])

Figure 4-2: The Red Hat User Manager, redhat-config-users

To create a new user, click the New button. This opens a window with entries for the username, password, and login shell, along with options to create a home directory and a new group for that user. Once you have created a user, you can edit its properties to add or change features. Select the user's entry and click Properties. This displays a window with tabbed panels for User Data, Account Info, Password Info, and Groups. On the Groups panel, you can select the groups that the user belongs to, adding or removing group memberships.

Alternatively, you can use the useradd command in a terminal window or command line to add user accounts and the userdel command to remove them. The following example adds the user dylan to the system:

```
$ useradd dylan
```

One common operation performed from the command line is to change a password. Any user can change his or her own password with the passwd command. The command prompts you for your current password. After entering your current password and pressing ENTER, you are then prompted for your new password. After entering the new password, you are asked to reenter it. This is to make sure you actually entered the password you intended to enter.

```
$ passwd
Old password:
New password:
Retype new password:
$
```

**Tip** You can use the redhat-config-rootpassword tool (Root Password on System Settings) to change the password for the root user.