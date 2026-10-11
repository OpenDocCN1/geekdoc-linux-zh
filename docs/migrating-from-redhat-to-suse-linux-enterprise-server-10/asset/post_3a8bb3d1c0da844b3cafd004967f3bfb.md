
To set the properties of the user (such as the UID, the home directory, the login shell, group affiliation, and additional user account comments), select the **Details** tab. The following appears:

![](img/63e88022bf135307e3eac051ad238b5b_100_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_100_1.png)

Enter or edit information in the following fields:

- **User ID (uid).** For normal users, you should use a UID greater than 99 because the lower UIDs are used by the system for special purposes and pseudo logins.
  - If you change the UID of an existing user, the permissions of the files of this user owns must be changed. This is done automatically for the files in the user's home directory, but not for files located elsewhere.

![](img/63e88022bf135307e3eac051ad238b5b_101_0.png)

If this does not happen automatically, you can change the permissions of the user files in the home directory (as root) by entering `chown -R username /home/username`.

- **Home Directory.** The home directory of the user. Normally this is `/home/username`.
  - You can select an existing directory by selecting **Browse**.
- **Additional User Information.** This field can contain up to 3 parts separated by commas. It is often used to enter `office,work phone,home phone`.
  - This information is displayed when you use the `finger` command on this user.
- **Login Shell.** From the drop-down list select the default login shell for this user from the shells installed on your system.
- **Default Group.** This is the group to which the user belongs. Select a group from the list of all groups configured on your system.
- **Groups.** Select all additional memberships you want to assign to the user from the list.

To set various password parameters (such as duration of a password), select the **Password Settings** tab. The following appears:

![](img/63e88022bf135307e3eac051ad238b5b_102_0.png)

Enter or edit information in the following fields:

- **Days before Password Expiration to Issue Warning**. Enter the number of days before password expiration that a warning is issued to users.
  - Enter -1 to disable the warning.
- **Days after Password Expires with Usable Login**. Enter the number of days after the password expires that users can continue to log in.
  - Enter -1 for unlimited access.

- **Maximum number of days for the same password.** Enter the number of days a user can use the same password before it expires.
- **Minimum number of days for the same password.** Enter the minimum age of a password before a user can change it.
- **Expiration date.** Enter the date when the account expires. The date must be in the format YYYY-MM-DD.
  - Leave the field empty if the account never expires.

Save the settings for the new or edited user by selecting **Accept**.

A new user appears in the list.

Configure your server with the new settings by selecting **Finish**.

### Group Administration

You can administer groups from the following window:

![](img/63e88022bf135307e3eac051ad238b5b_104_0.png)

A list of groups appears with information such as group name, Group ID (*GID*), and group members.

Select **Set Filter**; then select one of the following to change the groups listed:

- **Local Groups**. Groups created on your local server to provide permissions for members assigned to the group.
- **System Groups**. Groups created by the system for use with services and applications.
- **Custom**. A customized view of groups based on the settings configured with **Customize Filter**.
- **Customize Filter**. This option lets you combine listed group sets (such as Local Groups and System Groups) to display a customized view (with Custom) of the groups list

Additional sets of groups are added to the Set Filter drop-down list (such as LDAP) as you configure and start services on your server.

You can create a new group or edit an existing group by selecting Add or Edit. The following appears when you select Edit:

#### Figure 2-16

![](img/63e88022bf135307e3eac051ad238b5b_105_0.png)

Enter or edit information in the following fields:

- **Group Name.** The name of the group. Avoid long names. Normal name lengths are between two and eight characters.
- **Group ID (gid).** The GID number assigned to the group. The number must be a value between 0 and 60000. GIDs to 99 represent system groups. GIDs beyond 99 can be used for normal users. YaST warns you if you try to use a GID that is already in use.
- **Password** (optional). Require the members of the group to identify themselves while switching to this group (see **man newgrp**). To do this, assign a password.
  - For security reasons, the password is represented by asterisks (`***`).
- **Confirm Password**. Enter the password a second time to avoid typing errors.
- **Group Members**. Select which users should be members of this group.
  - A second list appears (when you select Edit) that shows users for which this group is the default group. This list cannot be edited from YaST.

When you finish entering or editing the group information, select **Next**. You are returned to the Group Administration dialog. Save the configuration settings by selecting **Finish**.

The information you enter when creating or editing users and groups with YaST is saved to the following user administration files:

- `/etc/passwd`
- `/etc/shadow`
- `/etc/group`

### Set Defaults for New User Accounts

You can use YaST to select default settings to be applied to new user accounts.

From the Gnome desktop, press **Alt+F2**, enter `yast2` and enter the root password when prompted. Select **Security and Users > User Management**. You can also start the User Management module directly from a terminal window as root by entering `yast2 users`.

Select **Expert Options > Defaults for New Users**. The following appears:

#### Figure 2-17

![](img/63e88022bf135307e3eac051ad238b5b_107_0.png)

You can enter or edit information in the following fields:

- **Default Group.** From the drop-down list select the primary (default) group.
- **Secondary Groups.** Enter a list of secondary groups (separated by commas) to assign to the user.
- **Default Login Shell.** From the drop-down list select the default login shell (command interpreter) from the shells installed on your system.
- **Default Home.** Enter or browse to the initial path prefix for a new user’s home directory. The user’s name will be appended to the end of this value to create the default name of the user’s home directory.
- **Skeleton Directory.** Enter or browse to the skeleton directory. The contents of this directory will be copied to the user’s home directory when you add a new user.
- **Default Expiration Date.** Enter the date on which the user account is disabled. The date must be in the format YYYY-MM-DD.
  - Leave the field empty if this account never expires.
- **Days after Password Expiration Login Is Usable.** This setting enables users to log in after passwords expire. Set how many days login is allowed after a password expired.
  - Enter -1 for unlimited access.

Save the configuration settings by selecting **Next > Finish**. The values are written to the file **/etc/default/useradd**.

```
dal0:~ # cat /etc/default/useradd
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
GROUPS=video,dialout
CREATE_MAIL_SPOOL=no
```

You can also use the command line program **useradd** to view or change the defaults. The option **--show-defaults** displays the same as the cat above. The option **--save-defaults** followed by an option with a value changes them:

```
dal0:~ # useradd --save-defaults -d /export/home
dal0:~ # useradd --show-defaults
GROUP=100
HOME=/export/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
GROUPS=video,dialout
CREATE_MAIL_SPOOL=no
```

The manual page for useradd lists the possible options.

> **useradd** on SUSE Linux Enterprise Server 10 does not create a home directory for a new user by default; use the option **-m** to create a home directory when creating a new user.
