the groupshow subcommand, but will show up when the information is queried via the id command or a similar tool. When pw is used to add a user to a group, it only manipulates /etc/group and does not attempt to read additional data from /etc/passwd.

# 3. Adding a new member to a group:

```
# pw groupmod project0 -m bob
# pw groupshow project0
project0:* :1100:mansoor,bob
```

# 4. Using the id command to determine group membership:

```
% id mansoor
uid=1001(mansoor) gid=1001(mansoor) groups=1001(mansoor), 1100(project0)
```

In this example, mansoor is a member of the groups mansoor and project0.

# 23.3.2 Adding/Deleting and Maintaining Users and Groups in a GUI-Based Interface on PC-BSD

The easiest and most efficient way to create and manage user accounts and groups on PC-BSD is by using the GUI-based User Manager. The first step to launching the User Manager is to open a root window from the Kickoff Application Launcher in the lower-left corner of the screen, under Applications>Utilities>Root Terminal. Then, in the terminal window that appears, type the following, as shown in Figure 23.1:

```
# pc-usermanager
```

The system then launches the User Manager in its own window, as shown in Figure 23.2. If you click the Remove button for a highlighted user, a pop-up menu will ask if you would like to also delete the user's home directory (along with all of their files). If you click No, the user will still be deleted but their home directory will remain. If you have only created one user account, the Remove button will be grayed out as you need at least one user to be able to login to the PC-BSD system.

![](bbox=[0.42, 0.82, 0.65, 0.92])