# # Installing Software For Users To Run

There are a number of things to keep in mind when you are preparing to install software for your users, or even for your own use with a non-superuser account:

+   * A user has to have permissions to run the program. Therefore, do not place it in a location that is accessible to root only.
+   * Do not loosen the permissions on a current directory to allow user access to the programs contained therein. This action is counterproductive for security purposes.
+   * If the application allows users to write data, be sure to configure it carefully so that it is secure.
+   * If the application uses some kind of hierarchy of user types, be sure to set this properly.
+   * Install the man pages—online manuals—for the package.

# # Creating Groups

It is useful at times to create a new group to place users in rather than using one that already exists. This group information goes into the file /etc/group, but none of the methods discussed in this section requires you to edit that file directly.

# ## Creating Groups On The Command Line

To create a new group at the command line, do the following:

+   1. Log in as root.
+   2. Type “groupadd *groupname*” to create the new group.

# ## Creating Groups In GNOME

To create a new group in GNOME, do the following:

+   1. If GNOME is not already started, start it by typing either “startx” or “init 5” at the command line.
+   2. Log in as root.
+   3. Click on the GNOME footprint icon to open the main menu.
+   4. Click on System|Linuxconf. The Linuxconf tool opens.
+   5. Find the Users Accounts option in the list on the left side of the screen.
+   6. Click on Users Accounts|Normal|Group Definitions to pull up the User Groups tab shown earlier in Figure 2.14.

![](bbox=[0.91, 0.16, 0.95, 0.32])