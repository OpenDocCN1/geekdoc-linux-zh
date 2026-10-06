
# KDE Control Center: System Module (Continued)

| | |
|---|---|---|
| New type | To add a new session, enter the name of the new session type, and click **Add new**. |
| Available types | Lists available session types. To remove a session type, highlight it, and click **Remove**. |
| Users | The GUI Login window presents a list of users for the convenience of the person logging in, who can click a user in the list to fill the **Login:** text box or can enter a login name directly into the text box.
This tab divides the users into three groups: **Remaining users, Selected users, and No-show users**. Move the users between the boxes by highlighting a user and clicking the arrows between the boxes. The **Show users** frame specifies which users are presented in the GUI Login window. **No-show users** are never displayed, **Selected only** presents the **Selected users**, but all no-show present the **Remaining users** and the **Selected users**, and **None** does not present any users. **Sort users** displays the users in alphabetical order.
Highlight a user, and click the icon just above the **Show users** frame to change the icon that represents the user in the GUI Login window. |
| Convenience | *Use the items in this tab only on a home system that is not connected to a network. Anything you change security in order to make it easier to log in.* |
| Automatic login | |
| Enable auto-login | Enables you to log in to the user as specified in the **Preselect User** frame (following). Performs **Truly automatic login** when you kill the X server (CONTROL-ALT-BACKSPACE). |
| Truly automatic login | Logs in the specified user automatically each time the Login window is displayed. |
| Preselect User | Specifies a user name that automatically appears in the Login text box of the GUI window. You can specify that no name appear, the name of the previous user who logged in, or that user's name specified in the **User** drop-down menu appear. Checking **Focus password** causes the cursor to appear in the Password text box, ready for the preselected user to enter a password. |
| Password-less login | Enables users in the **Skip password check** column to log in without providing a password. |
| Miscellaneous | **Automatically log in again after X server crash** causes KDE to log you in again after the X server crashes and you bring it up. |
| Printing Manager | Refer to "KDEPrint: Manages Printers" on page 1014. |

# KDE Control Center: Network Module

Select this module from K menu: Control Center⇒Network; you can select the individual functions from K menu: Preferences⇒Network. The Network module of the KDE Control Center mixes simple and complex tasks (Table 17-11). Set up basic e-mail and news tickers here, or work on LAN browsing by setting up the LiSA or ResLISA daemon.

| KDE Control Center: Network Module | Table 17-11 |
| --- | --- |
| Email | Sets up your e-mail information and specifies a default e-client. |
| Kisdndock | Automatically starts the KDE ISDN Dock, which allows you to connect/disconnect quickly to ISDN (page 1474) links when you start KDE. Run redhat-config-network to start the Network Configuration module (page 987), and run internet-droid to start the Internet Configuration Wizard (page 1023). |
| LAN Browsing | Sets up LISA (LAN Information Server, lisa-home.sourceforge.net) or ResLISA for browsing your LAN. Functioning similarly to MS Network Neighborhood, LISA relies solely on the TCP/IP stack and on SMB (page 1492). The resLISA program is more secure than LISA; The *LISA Handbook* (docs.kde.org/2.2.2/kdenwork/lisa/index.html) describes both. Using the *Guided LISA Setup* makes it easier to set up LISA. |
| Preferences | |
| Timeout Values | Specifies the length of time to wait for the specified network operation to complete. The default values usually work well; adjust them if your connection is very slow. |
| FTP Options | |
| Enable Passive Mode (PASV) | Enables *passive FTP* (page 1484) so that you can use ftp through a firewall. |
| Mark partially uploaded files | Uses a special filename for files as they are being uploaded and changes the name when the upload is complete. |
| SOCKS | Enables and sets up SOCKS (page 1493) support on the local system. |

# Configuring User and Group Accounts

More than a login name is required for a user to be log in and use the system. A user should have the necessary files, directories, permissions, and optionally a password in order to log in. Minimally a user must have an entry in the /etc/passwd and /etc/shadow files and a home directory. The following describe several ways you can work with user accounts. Refer to page 390 and the NIS-HOWTO when you want to run a Network Information Service (NIS or NIS+) to manage the passwd database.

# redhat-config-users: Manages User Accounts

| | | |
|---|---|---|
| GNOME | GNOME menu: System Settings⇆Users and Groups start-here: System Settings⇆Users and Groups | |
| KDE | K menu: System Settings⇆Users and Groups start-here: System Settings⇆Users and Groups | |
| graphical | redhat-config-users | |

The Red Hat User Manager is a graphical tool that enables you to add, delete, and modify system users and groups.

The Search filter selects users or groups whose name match the string, which include wildcards, that you enter in the Search filter text box. The string must match the beginning of a name. Characters in the name, following the match, is discounted. For example, *nob matches nobody and nfsnobody, whereas nob matches only nobody. After you enter the string, click Apply filter or press RETURN.

> Red Hat User Manager: User and Group Properties

The Red Hat User Manager window has two tabs just above the display area of the window:

- Click the Users tab to display the list of users. Highlight a user, and click Properties on the toolbar to work with the properties of the highlighted user.
- Click the Groups tab to display the list of groups. Highlight a group, and click Properties on the toolbar to work with the properties of the highlighted group.

To create a new user or group, click the Add User or Add Group button on the toolbar. The User Manager displays the Create New User window, which is similar to the Data tab of the User/Group Properties window (Table 17-12 and Table 17-13). Enter the information for the new user or group and close the window. Once the user or group exists, you can work with its properties to add/change/remove information. To modify a user or group, highlight the user or group, and click Properties on the toolbar.

# Red Hat User Manager: Users

In this table [CNU] indicates an item that is present only in the Create New User window.

| | |
|---|---|
| User Name | The identification string (login name) that you use to log in on the system. Sometimes it resembles the user's name. |
| Full Name | The user's real name or how the user would like to be thought of. Can include other other identifying text, such as a phone extension. |
| Password | The string that the user enters, after the User Name, to log in on the system. For more information, refer to "Keeping the System Secure" on page 1070. |
| Confirm Password | A repetition of the password to make sure that you got it right first time. |
| Create home directory [CNU] | Causes the User Manager to create a home directory for the user. |
| Home Directory | By default the name of the new home directory is /home/username, where username is the User Name. You can specify a different path/or name. |
| Login Shell | The shell the user wants to log in. Leave the default (bash) when you do not know or care. |
| Enable account expiration | Enables you to set a date when the account expires. This is different from the date the password expires; the user can do nothing about it. |
| Account expires on date | Sets the date when the account expires. |
| User account is locked | Sets an administrative lock that causes the user name and password not to work. Turn off the lock by clicking the box to remove the check mark. |
| Password Info | For more information on passwords, see "Keeping the System Secure" on page 1070. |
| Enable password expiration | Enables you to set time periods within which the user must or must not change his or her password. |
