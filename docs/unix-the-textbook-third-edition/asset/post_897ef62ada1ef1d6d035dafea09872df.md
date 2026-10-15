
the groupshow subcommand, but will show up when the information is queried via the id command or a similar tool. When pw is used to add a user to a group, it only manipulates /etc/group and does not attempt to read additional data from /etc/passwd.

## 3. Adding a new member to a group:

```
# pw groupmod project0 -m bob
# pw groupshow project0
project0:* :1100:mansoor,bob
```

## 4. Using the id command to determine group membership:

```
% id mansoor
uid=1001(mansoor) gid=1001(mansoor) groups=1001(mansoor), 1100(project0)
```

In this example, mansoor is a member of the groups mansoor and project0.

## 23.3.2 Adding/Deleting and Maintaining Users and Groups in a GUI-Based Interface on PC-BSD

The easiest and most efficient way to create and manage user accounts and groups on PC-BSD is by using the GUI-based User Manager. The first step to launching the User Manager is to open a root window from the Kickoff Application Launcher in the lower-left corner of the screen, under Applications>Utilities>Root Terminal. Then, in the terminal window that appears, type the following, as shown in Figure 23.1:

```
# pc-usermanager
```

The system then launches the User Manager in its own window, as shown in Figure 23.2. If you click the Remove button for a highlighted user, a pop-up menu will ask if you would like to also delete the user's home directory (along with all of their files). If you click No, the user will still be deleted but their home directory will remain. If you have only created one user account, the Remove button will be grayed out as you need at least one user to be able to login to the PC-BSD system.

![](img/02e070097d401d3bf7de4bf1c470b267_1118_0.png)

![](img/02e070097d401d3bf7de4bf1c470b267_1119_0.png)

## FIGURE 23.2 User Manager window.

![](img/02e070097d401d3bf7de4bf1c470b267_1119_1.png)

## FIGURE 23.3 User Manager - Advanced Mode window.

While a removed user will no longer be listed, the user account will not actually be deleted until you click the Apply button. A pop-up message will indicate that you have pending changes if you close User Manager without clicking Apply. If you change your mind, click No and the user account will not be deleted; otherwise, click Yes and the user will be deleted and User Manager will close.

The password for any user can be changed by first highlighting the user name then clicking the Change Password button. You will not be prompted for the old password in order to reset a user's password; this can be handy if a user has forgotten their password and can no longer log into the PC-BSD system. If you click the Change Admin Password button, you can change the root user's password.

If you click the Advanced View button, this screen will change to show all of the accounts on the system, not just the user accounts that you created. An example is seen in Figure 23.3.

The accounts that you did not create are known as system accounts and are needed by the operating system or installed applications. You should not delete any accounts that you did not create yourself, as doing so may cause a previously working application to stop working. Advanced View provides additional information associated with each account, such as the user ID number, full name (description), home directory, default shell, and primary group.

Figure 23.4 shows the Add User Account Creation screen that opens when you click the Add button under Advanced View.

![](img/02e070097d401d3bf7de4bf1c470b267_1120_0.png)

## FIGURE 23.4 Add User window.

This screen is used to input the following information when adding a new user or system account:

- Full Name: This field provides a description of the account and can contain spaces. If it is a user account, use the person’s first and last name. If it is a system account, input a description to remind you which application uses the account.
- Username: The name the user will use when they log in to the system; it is case sensitive and can not contain any spaces. If you are creating a system account needed by an application, use the name provided by the application’s installation instructions. If the name that you choose already exists as an account, it will be highlighted in red and the utility will prompt you to use another name.
- Home Directory: Leave this field empty for a user account as the system will automatically create a ZFS dataset for the user’s home directory under /usr/home/username. We supply more information on the structure and administration of the ZFS file system in Chapter 24. However, if you are creating a system account it is important to override this default by typing in /var/empty or /nonexistent unless the application’s installation instructions specify that the account needs a specific home directory.
- Shell: This drop-down menu contains the shells that are available to users when they are at a command prompt. You can either keep the default or select a shell which the user prefers.
- Primary Group: If you leave the default button of New Group selected, a group will be created with the same name as the user. This is usually what you want unless you are creating a system account and the installation instructions specify a different group name. The drop-down menu for specifying a group name will only show existing groups, but you can quickly create a group using the Groups tab.
- Password: The password is case sensitive and needs to be confirmed.
- Encrypt Files: If this box is selected, the user’s home directory will automatically be encrypted with PEFS. When the user logs in, the contents of their home directory are automatically decrypted after they enter their password. When they logout, the contents of their home directory are automatically encrypted and will appear as gibberish to other users who do not know the password. For this reason, it is important
