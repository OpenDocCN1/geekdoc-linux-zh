
## Add a User Account

Follow these steps to add a user account in AdminSuite:

1. Click the Users icon in the left pane of the AdminSuite window. (See the preceding section for an explanation of how to open the AdminSuite tool.)
2. Double-click the User Accounts icon in the right pane of the AdminSuite window. The Set Initial View dialog box appears (shown in Figure 11.18). The Set Initial View dialog box controls which users you see in the User Accounts window.

![](img/256e02a6afce528d264a8d911fa0ff20_480_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_480_1.png)

3. Click the Show All User Accounts radio button, the Show No User Accounts radio button, or the Filter User Accounts radio button. Then click the OK button. If you click the Filter User Accounts radio button, set the filter you desire before you click the OK button. You can alter your view of the User Accounts window by selecting commands from its View menu.
4. Select the Add User command from the Action menu to display the Add User Wizard, shown in Figure 11.19. In the first six steps of the wizard, you fill in the username, UID, password, primary group, home directory, and mail server for the new user account. The seventh step asks you to review the information before committing the new user account to the user database.

**FIGURE 11.19**
The Add User Wizard

![](img/256e02a6afce528d264a8d911fa0ff20_481_0.png)

5. Enter the information requested, review the final screen, and then click the Finish button. The new user is added to the User Accounts window and selected.

### Add Multiple User Accounts

Because the AdminSuite is used in network environments, administrators are often faced with the task of adding many users to the network at once. The AdminSuite has a mechanism that allows you to create many users in a single operation. You can manually enter the names one at a time from a text file, or you can create a automatically generated series of names.

Follow these steps to create multiple user accounts at once:

1. Select the Add Multiple Users command from the Action menu in the User Account window. The Add Multiple Users Wizard dialog box shown in Figure 11.20 appears.
2. Select the Specify a Text File radio button, the Type Each Name radio button, or the Automatically Generate a Series of User Names radio button.

For the text file selection, you will need to supply the path to a file that contains names as line entries, with each name on a single line. The Automatically Generate selection adds a number to a username that you specify, creating as many user accounts as you indicate.

![](img/256e02a6afce528d264a8d911fa0ff20_482_0.png)

3. Complete the steps in the wizard, then review the information and click the Finish button. Solaris adds the user accounts to the home directory server you selected in the AdminSuite tool.

## Modify User Accounts

You can also modify specific user accounts in the AdminSuite. To view user properties, double-click a user account of interest in the User Accounts window. The User Properties dialog box, shown in Figure 11.21, appears.

There are seven tabs in the User Properties dialog box (once you have made the changes you desire, click the OK button to put them into effect):

**General** On this tab you can set a name and ID number for a user. You can also specify the login shell and the duration of the account. Information about the account availability appears only if your password gives you the right to view this information.

**Group** Use this tab to change a user’s group memberships.

**Home Directory** You can set the user’s home directory on this tab, as well as share the directory and set all users’ access.

**Password** On this tab, you can set or reset a user’s password. An administrator can use this tab to restore a user’s forgotten password or reset a password that has expired.

**Password Options** On this tab are settings that determine when a password expires, when to alert a user that the password is about to expire, and how long before a specific password can be used again.

**Mail** The Mail tab shows the name of the mail server as well as the user’s mailbox.

**Rights** On this tab, you can view and modify the rights of a user account. You can either grant a right by checking its corresponding check box or deny a right by unchecking the check box. Categories of rights listed include Audit Management, Device Allocation, Cron and At Jobs, Login Control, Execution Profile Management, Role Management, Machine Administration, File Systems, Computers/Networks, Log Viewer, Serial Ports, and User, Groups & Mailing List Rights.

![](img/256e02a6afce528d264a8d911fa0ff20_483_0.png)

## Deleting User Accounts

You can also use the AdminSuite to delete user accounts. To do so, follow these steps:

1. Click the user account you wish to delete.
2. Select the **Delete** command from the Action menu. The warning dialog box shown in the following graphic appears.

![](img/256e02a6afce528d264a8d911fa0ff20_484_0.png)

3. Click the Delete button to confirm the deletion.

Solaris deletes the user account from all entries in the directory services database and removes the user account from membership in all of the groups that it belonged to. This procedure does not delete either the home directory or a user’s mailbox. You will need to manually delete those associations from the system that they are stored on (typically a server).

## Managing Network Groups with AdminSuite

Using the AdminSuite to work with groups is similar to using it to create and manage user accounts. First I’ll show you the steps necessary to create groups in the AdminSuite:

1. Click the Groups icon in the left pane of the AdminSuite window. (See “Using AdminSuite 3 for Account Management” earlier in this chapter for instruction on opening the AdminSuite tool.)
2. Double-click the Groups icon in the right pane of the AdminSuite window. The Set Initial View (Filter Groups) dialog box appears (shown in Figure 11.22).
3. Click the Show All Groups radio button, the Show No Groups radio button, or the Filter Groups radio button, then click the OK button.

For the Filter Groups selection, set the filter you desire before you click the OK button. You can alter your view of the Groups window by selecting commands from its View menu.

4. Select the Add Group command from the Action menu to display the Add Group dialog box (shown in Figure 11.23). In the Add Group dialog box, you can create a new group (either a local group or a group on a domain somewhere on the network) and assign members to it.

**FIGURE 11.22**
The Set Initial View (Filter Groups) dialog box

![](img/256e02a6afce528d264a8d911fa0ff20_485_0.png)

**FIGURE 11.23**
The Add Group dialog box

![](img/256e02a6afce528d264a8d911fa0ff20_485_1.png)

5. Enter the group name in the Group Name text box and the Group ID in the Group ID Number spin box, then click the OK button. The new group is added to the groups database along with the GID and members you assigned.

A system administrator will often have to add a number of users at a single time to a group in a domain. AdminSuite provides a means to do just that using the Copy to Group or Mailing List command. The procedure is straightforward and convenient to perform.

To add a number of users to a group at once, follow these steps:

1. In the AdminSuite window, double-click the User Accounts icon in the left pane to view the user accounts icons in the right pane.
2. Click a user of interest, then hold down the Ctrl key and click the additional user accounts you wish to add to the group.
3. Select the Copy to Group or Mailing List command from the Action menu.
4. Click the Groups icon, then click the group you want to add the users to. To add the user accounts to more than one group, hold down the Ctrl key and click additional groups to extend the range of your selection.
5. Select the Choose Paste User(s) into Group command from the Action menu. Solaris adds those user accounts to the group or groups you selected.
6. Confirm that the user accounts were added to the groups by clicking on the groups and selecting the Properties command from the Action menu. If you were successful, you will see the user accounts listed in the Group Members list box.

## Modify Group Accounts

You can also modify specific group accounts in the AdminSuite. To view the group properties, double-click a group account of interest in the Groups window. The Group Properties dialog box, shown in Figure 11.24, appears.

You are limited to changing just the group name and GID number in the Group Properties dialog box. Once you have made the changes you desire, click the OK button to put them into effect. To delete users from a group, open the group in the Groups window, click the user to select it, and press the Delete key. You can select multiple user accounts to delete by holding down the Ctrl key and clicking on additional user accounts to add them to your range of selection.
