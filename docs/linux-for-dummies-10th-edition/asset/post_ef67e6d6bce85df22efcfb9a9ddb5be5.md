
## Managing Users and Groups

Whether you support a Linux system with hundreds of users, or just have a user account for you and one for your cat, you need to know how to manage user accounts. This section walks through the basics you need to know to manage user accounts on your Linux system.

### Finding the right tool

Not all desktop Linux distributions include a useful GUI user management tool. However, user management tools are available for each of the common desktops, so finding one that works in your Linux distribution shouldn't be hard (see Chapter 15 on how to install software).

For example, the default Ubuntu user management tool is somewhat weak. While it tries to hide some of the complexities of creating user accounts, it limits you in what you can do when creating a new user account. However, the GNOME 3 project provides some great administration tools, including the GNOME User and Group utility. This utility allows you to perform just about any user or group function required on your system. Just use the Ubuntu Software application (see Chapter 15) and install the GNOME User and Groups program. Figure 17–1 shows the GNOME Users and Groups utility after it’s started.

![](img/577d3bff979ee86b07f9836e0df274ce_339_0.png)

Be careful when selecting the Users and Groups utility from the Ubuntu Software list. If you search for “Users and Groups” you see three different versions for different desktops. Just read the description and make sure you select the GNOME version.

![](img/577d3bff979ee86b07f9836e0df274ce_339_1.png)

FIGURE 17–1: The GNOME user manager utility.

In openSUSE, the main administrator tool is YaST. Fortunately, YaST includes a very good user management tool. To get to it, follow these steps:

- 1. **From the KDE menu, choose Applications > System > Administrator Settings.**
- 2. **In the YaST Control Center window, select the Security and Users icon on the left-hand side of the window.**
- 3. **Click the User and Group Management icon that appears on the right-hand side of the window.**

The main window contains four tabbed panes — one for managing users, one for managing user groups, one for setting the default user properties, and one for defining the user authentication method used for the system (such as whether you want to use a centralized network authentication server for multiple workstations). The main User and Group Management window is shown in Figure 17–2.

![](img/577d3bff979ee86b07f9836e0df274ce_340_0.png)

All user and group management tools have pretty much the same abilities and features. Instead of trying to walk through every possible situation, the following sections walk through the basics for adding, modifying, and deleting users and groups using the YaST User and Group Management tool. You can apply these same principles to whichever tool you're using for your desktop environment.

## Adding new users

When you first installed your Linux system, it created a user account for you. That account has its own home folder for storing files. If you’re in an environment where others use the same system, it’s a good idea to create separate user accounts for each user. That way, you don’t have to worry about the cat accidentally deleting your important documents.

If you need to add additional user accounts, here’s what you need to do:

- 1. **While in the Users tab, click the Add button.**
   The screen prompts for information about the new user account. In YaST, that’s the User Data tab, as shown in Figure 17-3.

![](img/577d3bff979ee86b07f9836e0df274ce_341_0.png)

- 2. **Type the full name of the user for documentation purposes in the User’s Full Name text box.**
- 3. **Type a username for the user in the Username text box.**
- 4. **Enter a password for the user in the Password text box, and then retype it in the Confirm Password text box.**
   For security you should always use passwords that aren’t common words, contain a mixture of numbers and upper and lowercase letters, and are a minimum of eight characters long.

![](img/577d3bff979ee86b07f9836e0df274ce_341_1.png)

- 5. **Click the Details tab to view the account details.**

You can customize several account features, or use the default settings as defined in your Linux system, as shown in Figure 17-4.

![](img/577d3bff979ee86b07f9836e0df274ce_342_0.png)

- 6. **(Optional) Modify any of these settings:**
   - **User ID:** Linux tracks user accounts by the user ID and not the username. Each user account must be assigned a unique user ID. Normally the user management tool picks the next available user ID, but you can change that if needed.
   - **Home Directory:** User accounts normally have their own user directory under the `/home` directory to store files. This defines the location of the user directory.
   - **Home Directory Permission Mode:** Normally each user account has permissions to only their user directory. You can change the permissions to allow users in the same group to read others’ home directories (see Chapter 7).
   - **Login Shell:** Linux supports several different command line shell environments (see Chapter 16). Normally the *bash* shell is used by default.
   - **Default Group:** Some Linux distributions (such as Ubuntu) assign each user account to a unique group, while others (such as openSUSE) assign users to a common group.
   - **Additional Groups:** A user account can be a member of multiple groups, often used for sharing files; you can select these groups from the list.

- 7. **Click the Password Settings tab.**

Linux allows you to control how often passwords need to be changed. The Password Settings tab provides fields that allow you to control when the user account's password must be changed, or can be changed, as shown in Figure 17-5.

- 8. **Click OK to create the new user.**

![](img/577d3bff979ee86b07f9836e0df274ce_343_0.png)

After the new user account is created, it appears in the user list under the User tab. Some utilities provide additional features for managing the new user account. The YaST tool has two tabs — one for uploading SSH keys for the user account to access remote hosts, and another for using plugin features, such as assigning disk quotas to the new user account.

> **TIP**
> Most Linux distributions use the same tool to modify or delete existing user accounts. Just select the existing user from the list and click the button to either edit or delete the user account. When you edit the user account you see the exact same prompts as when you created the account, allowing you to change any of the settings you previously assigned.

> **TIP**
> Some tools allow you to retain the user's home directory after deleting the user account. This can come in handy when you need to access some of the personal files from that user. However, the files are still be assigned to the old user ID of the original owner. You most likely need to change those assignments (see Chapter 7).

## Adding new groups

Groups help you manage access to files and folders on the system. Each file and folder contains three sets of permissions — one set for the owner, another set for the group the file or folder is assigned to, and the last set for all other users on the system. By assigning a file or folder to a special group, you can allow all users that belong to that group to have full access to the file or folder.

Here's what you need to do to create a group in the openSUSE YaST user and group manager tool:

- 1. **Click the Groups tab in the User Management tool.**
   It lists the existing groups, and the users currently assigned to each group. Because many groups are system-related, the tool filters out those and only displays standard user groups, as shown in Figure 17-6.

![](img/577d3bff979ee86b07f9836e0df274ce_344_0.png)

FIGURE 17-6: The Groups tab in the YaST User Management tool.

- 2. **Click the Add button.**
   The Create New Group window opens, as shown in Figure 17-7.

- 3. **Type the name of the new group in the Group Name text box.**
