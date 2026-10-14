
## Figure 12.6

Active Directory Users and Computers MMC snap-in.

![](img/415c89a1ede71e11e5040a0038b6916c_528_0.png)

## Figure 12.7

New user properties window.

![](img/415c89a1ede71e11e5040a0038b6916c_528_1.png)

## Figure 12.8

New user password options window.

![](img/415c89a1ede71e11e5040a0038b6916c_529_0.png)

## Table 12.9 User Password Options

| Option | Description |
|---|---|
| User must change password at next logon | Setting this option forces the user to change their password the next time they log on to the Windows 2000 domain. It is recommended that you make new users change their default passwords. |
| User cannot change password | Setting this option prevents a user from changing their password. This option is rarely used for regular users, but you may find it useful for service accounts. |
| Password never expires | Setting this option prevents the password from expiring, despite the system default settings. This option is useful for Administrator and service accounts. |
| Account is disabled | Setting this option prevents the account from being used on the Windows 2000 domain. This option is useful in preventing old user accounts from being used before they are permanently removed from the domain. |

## Understanding User Account Properties

Up to now, you have seen a limited set of properties associated with the user account. This section will describe in detail the different properties you can configure for user accounts in Windows 2000 domains. To begin, double-click the account we just created to display the user Properties window in Figure 12.9.

As you can see, there are several tabs available. Each tab provides access to a different set of properties, which are described in Table 12.10.

In addition to the properties pages available for the user account, the Action menu provides several options when a user account is selected in the right pane. Table 12.11 describes these options.

This section has provided you with the necessary background to understand user accounts in Windows 2000. The next section will provide you with an overview of Windows 2000 groups.

Figure 12.9
User Properties window.

![](img/415c89a1ede71e11e5040a0038b6916c_530_0.png)

## Table 12.10 User Account Properties

| Property Tab | Description |
|---|---|
| General | Allows you to specify general user account information, including: <br>- Name. <br>- Description. <br>- Office location. <br>- Telephone number. <br>- Email address. <br>- Web page URL. |
| Address | Allows you to specify the user's address. |
| Account | Allows you to specify account-specific options, including: <br>- Logon name. <br>- Allowed logon hours (default is all hours). <br>- Allowed workstations (default is all workstations). <br>- Miscellaneous account options. <br>- Account expiration. |
| Profile | Allows you to specify the location of the user's roaming profile, logon script, and home folder. |
| Telephones | Allows you to specify numbers for the following telephone types: <br>- Home. <br>- Pager. <br>- Mobile. <br>- Fax. <br>- IP phone. |
| Organization | Allows you to specify the following organization-specific options: <br>- Title. <br>- Department. <br>- Company name. <br>- Manager. <br>Using this property page can help you to keep track of your organization's structure. |
| Remote control | Allows you to configure remote-control options that are applicable during a Terminal Services session. |
| Terminal Services Profile | Allows you to specify the location of a user’s roaming profile and home directory when logged on to a Terminal Services session. This page also allows you to enable/disable Terminal Services access. |
| Member Of | Allows you to specify the groups to which the user belongs. |
| Dial-in | Allows you to enable/disable dial-in permission and the available callback options. |
| Environment | Allows you to configure Terminal Services startup options, including: <br>▪ Which program, if any, to start after logon. <br>▪ Connections to network resources. |
| Sessions | Allows you to configure Terminal Services timeout and reconnection settings. |

## Table 12.11 Action Menu Options

| Action Menu Options | Description |
|---|---|
| Copy | Allows you to create a new account based on the settings in the currently selected account. Some of the settings copied include the profile and account options. |
| Add members to a group | Allows you to add the selected account to a group. |
| Disable Account | Allows you to disable the user account, preventing users from using the account to log on to workstations or access network resources. |
| Reset Password | Allows you to reset the account’s password, without having to know the old password. |
| Move | Allows you to move the account to a different container. |
| Open home page | Allows you to open the user’s home page, if it has been specified in the account properties. |
| Send mail | Allows you to send email to the user, if their email address has been configured in the account properties. |
