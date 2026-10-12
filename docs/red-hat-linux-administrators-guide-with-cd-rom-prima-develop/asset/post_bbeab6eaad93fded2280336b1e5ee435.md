
## Configuring User Settings under Linuxconf

With the inclusion of Linuxconf into the Red Hat release, even the most naive administrator can effectively configure the networking, set up multiple users, fix system files, and change passwords. As seen in Figure 6.1, there are three main categories that can be edited under the main Linuxconf window; Config, Control, and Status.

The first section handles networking, user accounts, file systems, miscellaneous services and the manner in which you want Linux to boot. This is probably the main section that you, as an administrator, will be using for setting up clients or accounts. It is also useful for editing the network configuration.

The next section, Control, as shown in Figure 6.2 contains entries for the Control-panel, Control files and systems, date and time and Features. These sections allow you to manipulate aspects of Linux operation.

The first section, Control-panel, does not allow you to configure files or settings, but to change active processes. These include shutting down the system, mounting and unmounting partitions, as well as configuring superuser tasks. The second subdirectory edits configuration files, changes permissions on files, and edits Linuxconf addons. The third section allows you to edit the date and time on the box, including your time zone. You can even use this section to retrieve the correct time from an atomic clock server elsewhere on the Internet. The last section defines special Linuxconf behavior, such as setting up the keyboard map.

In this last, and undoubtedly extremely short, section as shown in Figure 6.3, you can view the kernel boot messages, any additional boot messages and review previous Linuxconf messages. This is especially useful when wanting to verify any changes made by someone else to the file systems.

For the next few sections you will examine the first category, Config, and look at setting up user accounts. Under the Config tab in the main Linuxconf menu, select the User Accounts option. You will be presented with three separate tabs for configuring differing accounts: Normal, Special accounts, and Policies. For simple user account setup, the first option under the Normal heading is sufficient. See Figure 6.4 for a display of the differing account types.

Not only can you modify the normal accounts, but you can change group definitions as well as the root password. Restricting access to the Linuxconf program is essential if you do not wish others to be altering your root password. It is prudent to always log off once you are through with Linuxconf in order to prevent anyone from tampering with your settings. Much like you would never leave a root shell open on your desktop, the same holds true with the Linuxconf program.

![](img/a0884097af3186d9b4f616aaa3f065b0_225_0.png)

**FIGURE 6.1**
*Linuxconf is divided into three main categories for easy modification of files. The main Config window handles most tasks needed by administrators.*

![](img/a0884097af3186d9b4f616aaa3f065b0_226_0.png)

**FIGURE 6.2**
*The second category in the Linuxconf menu, Control, allows you to change running Linux utilities and to modify system settings.*

### ADMINISTERING THE SYSTEM

After selecting the Normal accounts button, you will be presented with a window much like the one in Figure 6.5. Here you can set all the variables for every user account on your system.

![](img/a0884097af3186d9b4f616aaa3f065b0_227_0.png)

**FIGURE 6.3**
*The third category in the Linuxconf menu, Status, checks the Linux logs.*

![](img/a0884097af3186d9b4f616aaa3f065b0_227_1.png)

**FIGURE 6.4**
*The User account configurator menu, which sets up various account types on the Linux operating system.*

You may modify each account by highlighting the respective username. Normally you will see only the account login name, a more verbose name describing in greater detail the account type, the UID of that user and the group to which he, she, or it belongs. You can add an individual account with minimal effort and with little knowledge of the command-line options. The Quit, Add, and Help buttons below the user information window will assist in configuring a new account.

When you select a user, a dialog box will appear that contains more information regarding that user. As shown in Figure 6.6, you will see the regular Base info tab describing basic user info as well as the Params tab and the Privileges tab.

![](img/a0884097af3186d9b4f616aaa3f065b0_228_0.png)

**FIGURE 6.5**
*The User accounts menu allows you to add, edit, or delete users from off of your system.*

![](img/a0884097af3186d9b4f616aaa3f065b0_229_0.png)

**FIGURE 6.6**
*The User information dialog box allows you to define the variables associated with the user. This window saves the information in the /etc/passwd file.*

Here you can specify any information you may wish to set for a particular user. Normally, you need only enter the login name and then click **Accept** to create the new account. The other fields, such as group, Home directory, Command interpreter, and User ID will be completed by the Linuxconf program for you. If you like, you may return later and modify the preselected settings and add or modify any fields you wish.

You will also be prompted automatically to enter a new password for that user. Again, like the command-line options, if Linux determines the password you selected to be unsafe, you will be warned but allowed to continue if you wish. If you are unsure as to the group with which you wish to associate a particular user, you are given a drop-down menu and can choose any of the pre-defined groups. If you create another group later on, you can return to this menu and change the selection. The same is true for the Command interpreter option. Though optional, Red Hat will assign bash to the user as the default shell. If that user desires another shell you can select from the list of installed shells on your system.

In the next tab under the User information section, **Params** (see Figure 6.7), the administrator can enter information about the life of the account or the life of the user’s password.

![](img/a0884097af3186d9b4f616aaa3f065b0_230_0.png)

**FIGURE 6.7**
*The Params tab under the User information window sets account and password variables for each user account.*

You can set the minimum number of days to maintain the password, or the number of days after which it must be changed. You can also specify that the system prompt the user to change his or her password a specified number of days before it expires, after which that user will no longer be able to log on to the system. Unlike the Base info tab, the Params tab, which stores information in the /etc/passwd file, stores the entered information in the /etc/shadow file.

Linuxconf goes beyond much of the regular command-line input. In other words, you are not required to know exactly which configuration files require editing or where in the system directories that file is located. The last tab, Privileges, is placed elsewhere in the system than in the /etc/passwd or /etc/shadow files where the previous options are edited. The GUI configuration makes the process much easier than editing specific files by hand.

The Privileges tab (see Figure 6.8) makes it simple to set user permissions. It is so simple that improper use or ignorance of what this utility can do could result in security problems.

If you wish to allow a certain user control over the Linuxconf program, you may define his or her privileges in this window. He or she may use not only Linuxconf, but can also exercise control over other various system settings if you so desire.

The Linuxconf program contains so many options that explaining them all would require an entire book. However, each tab offers a Help option that attempts to explain many of the terms and uses associated with each option.

In addition to offering user configuration options, Linuxconf also provides a User definitions option. Figure 6.9 shows the User definitions screen, which displays each group and its respective members. The screen also offers the option of adding additional groups and configuring their settings.

In most Linux distributions, there are more groups available in the Group file than there are users listed in the standard User file. Many of these groups should be left alone, as they perform specific tasks relative to the system. Unless you are sure what function each group performs, do not change or delete their settings.

To add a new group, you click the Add button. Linuxconf then displays the Group specification window (see Figure 6.10).

Here you need to enter integral user information regarding multiple or group accounts, comprising items such as the group name, the group ID (GID), and the members who will belong to the new group. Creating groups under Linuxconf is a useful feature when you want to share a certain directory with only specific users.

![](img/a0884097af3186d9b4f616aaa3f065b0_231_0.png)

**FIGURE 6.8**
*The Privileges tab does not so much set directory and file permissions as grant the user access to control and execute certain root-privileged tasks. These are privileges over general system utilities.*
