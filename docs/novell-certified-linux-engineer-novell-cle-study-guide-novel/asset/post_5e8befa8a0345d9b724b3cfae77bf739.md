
of your network. For the CLE exam, however, you only need to know how to complete the following iFolder management tasks:

- Configuring user access
- Configuring server parameters
- Installing and configuring the iFolder client
- Monitoring the iFolder system

We'll cover each of these topics in this section. Let's start with configuring user access.

## Configuring User Access

Before users can use the iFolder service on your server, you must configure the user objects in your eDirectory tree with iFolder access. To do this, you must first define the contexts within your tree that will be serviced by the iFolder server. Only user objects that reside within these contexts can use iFolder.

Following that, you must enable user objects to use iFolder. Both of these tasks are done using the iFolder Management Console. The iFolder Management Console is a web-based utility used specifically to configure the iFolder service on your server.

To access the iFolder Management Console, open a browser window and navigate to https://*your_server_IP_address*/iFolderServer/Admin. When you do, the screen in Figure 8.4 appears.

![](img/c7771e8540507f2b00c088c7a411b57b_353_0.png)

**FIGURE 8.4**
The iFolder Management Console.

Using the iFolder Management Console, you configure user access by completing the following steps.

- Open a web browser and navigate to https://your_server_IP_address/iFolderServer/Admin.
- Under Welcome to iFolder, select Global Settings.
- Authenticate as your admin user. After authentication, the screen shown in Figure 8.5 appears.

![](img/c7771e8540507f2b00c088c7a411b57b_354_0.png)

- Define the contexts where users who are authorized to use iFolder reside by completing the following:
- Under Global Settings, select User LDAPs. The screen in Figure 8.6 appears.

![](img/c7771e8540507f2b00c088c7a411b57b_354_1.png)

- Under User LDAPs, select your iFolder server. Notice that the only context displayed is the one you specified for the Admin context during installation; this is shown in Figure 8.7.
- Click Add.
- Click Search.

**FIGURE 8.7**
The iFolder Context Configuration screen.

![](img/c7771e8540507f2b00c088c7a411b57b_355_0.png)

- e. In the **Search Results** screen, select the container you wish to add and then click **Add**.
- f. Repeat this process until all the containers you want to enable are selected.

> **TIP** By default, iFolder will only search for users in the specified contexts. If you wish all subcontainers beneath the selected containers to be included, be sure to mark **Search Subcontexts**.

- g. Click **Update**.
- 5. Enable user access to iFolder by completing the following steps:
    - a. Select the **User Management** icon.
    - b. In the iFolder Management Console, select **Advanced Search**. The screen in Figure 8.8 appears.
    - c. Configure your search criteria to perform a filtered search for user objects; then click **Search**. To view all users, leave the search field blank and then click **Search**. The screen in Figure 8.9 appears.
    - d. Mark the users you want to enable for iFolder access.
    - e. Select **Enable checked users as iFolder users**.
    - f. When prompted to confirm the operation, click **OK**.

At this point, user access to iFolder has been configured. Before allowing users to log in, however, you need to configure various parameters for your iFolder server.

![](img/c7771e8540507f2b00c088c7a411b57b_356_0.png)

**FIGURE 8.8**
**The iFolder User Search screen.**

![](img/c7771e8540507f2b00c088c7a411b57b_356_1.png)

**FIGURE 8.9**
**The iFolder User Search Results screen.**

## Configuring Server Parameters

To configure global policies for your iFolder server, complete the following steps:

- 1. In the iFolder Management Console, select the **Global Settings** icon.
- 2. Select **Global Policies**.
- 3. In the **Global Policies** screen, select **Display** next to Server Policies. The screen shown in Figure 8.10 appears.
- 4. In the **Initial Client Quota** field, enter a quota for user file storage.
- 5. In the **Session Timeout** field, enter the amount of time, in minutes, after which a session will be terminated if no synchronization occurs.

**FIGURE 8.10**
The iFolder Global Server Policies screen.

![](img/c7771e8540507f2b00c088c7a411b57b_357_0.png)

If, for some reason, you don’t want synchronized user files to be saved in `/var/opt/novell/ifolderdata/ACCOUNTS`, you can change the iFolder storage location in your server’s file system. This is done by completing the following steps:

- 1. Create a directory in the file system where you want iFolder data saved.
- 2. Copy the existing contents of `/var/opt/novell/ifolderdata` to the new directory.
- 3. Open the `/etc/opt/novell/ifolder/httpd_ifolder_unix.conf` file in a text editor.
- 4. Scroll down to the **iFolderServerRoot** line, shown in Figure 8.11.

**FIGURE 8.11**
Editing the iFolder Conf file.

![](img/c7771e8540507f2b00c088c7a411b57b_357_1.png)

- 5. Change the value of the **iFolderServerRoot** parameter to the new directory you just created.
- 6. Save the changes to your file.
- 7. Change the owner of the new directory to the **novlwww** user.
- 8. Change the group associate with the directory to the **novlwww** group.

Steps 7 and 8 can be accomplished by entering `chown novlwww:novlwww directory_name` at a shell prompt.

> **TIP**

- 9. Change the permissions of the new directory to **700**.

Step 9 can be done by entering `chmod 700 directory_name` at a shell prompt.

> **TIP**

- 10. Restart the **novell-httpd** service.

The next thing you need to do is set global client policies on your server. These policies serve as the default parameters for iFolder clients that attach to your server. For most parameters, you can choose from the following levels, as shown in Figure 8.12.

![](img/c7771e8540507f2b00c088c7a411b57b_358_0.png)

**FIGURE 8.12**
iFolder Client Policies.

- **On**—Selecting this item enables a given setting. If this is the only parameter selected for a given setting, the policy will be applied by default, but users can override the policy using configuration settings in the iFolder client.
- **Enforced**—If this item is selected for a given setting, the policy will be applied by default. Users will be able to see the policy in their iFolder Client Configuration screen. However, the policy will be grayed out and users will not be able to override the setting.
- **Hidden**—If this item is selected for a given setting, the policy will be enforced by default, but it will not be visible in the iFolder Client Configuration screen.

Using these levels, you can configure the following iFolder policies in the Global Client Policies screen:

- **Encryption**—Enabling this policy encrypts user files stored on the iFolder server using the pass phrase.
- **Save Password**—Enabling this policy allows the user to save his or her password in the iFolder client.
- **Save Pass Phrase**—Enabling this policy allows the user to save his or her pass phrase in the iFolder client.
- **Recover Pass Phrase**—Enabling this policy allows the network administrator to recover a user's lost pass phrase. You should use this policy with caution. Because the pass phrase is used as the key to encrypt files, allowing the administrator to see a user's pass phrase also gives him or her the ability to decrypt the user's files on the iFolder server.
- **Automatic Sync**—Enabling this policy will cause iFolder clients to automatically synchronize changes with the iFolder server. If this policy is disabled, users must manually synchronize their iFolder clients with the iFolder server.
- **Sync to Server Delay**—If the Automatic Sync policy is enabled, this policy configures the amount of time, in seconds, after which a change that's made to a file in the iFolder directory is synchronized to the iFolder server.
- **Sync from Server Interval**—If the Automatic Sync policy is enabled, this policy specifies the interval in seconds that the iFolder client waits between queries to the iFolder server to download updated files.
- **Conflict Bin Space**—This policy specifies the amount of space to be reserved for Conflict Bin files for each iFolder user. By default, the space allocated is 25MB. If users primarily work with word processing documents, this allocation should be sufficient. If your users work with graphic, video, or audio files, you should consider increasing the amount of space allocated to the Conflict Bin.
- **iFolder Location**—This policy specifies the default location for the iFolder directory on the users' workstations.

> **WARNING**
> It's important that you understand that the policies marked with an asterisk in Figure 8.12 are not dynamic. They are applied only when the iFolder user account is first created. If you change one of these policies after user accounts have been created, you must delete the user accounts and re-create them in order for the change to be applied.
