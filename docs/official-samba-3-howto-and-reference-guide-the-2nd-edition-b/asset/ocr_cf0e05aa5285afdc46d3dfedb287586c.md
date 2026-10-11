+   In the box labeled **Copy Profile** to add your new path, such as, `c:\temp\foobar`.
+   Click on **Change** in the **Permitted to use** box.
+   Click on the group “Everyone”, click on **OK**. This closes the “choose user” box.
+   Now click on **OK**.

Follow these steps for every profile you need to migrate.

# ### 26.2.5.2 Side Bar Notes

You should obtain the SID of your NT4 domain. You can use the `net rpc info` to do this. See Chapter 12, “Remote and Local Management: The Net Command”, Section 12.13 for more information.

# ### 26.2.5.3 moveuser.exe

The Windows 200x professional resource kit has **moveuser.exe**. **moveuser.exe** changes the security of a profile from one user to another. This allows the account domain to change and/or the username to change.

This command is like the Samba **profiles** tool.

# ### 26.2.5.4 Get SID

You can identify the SID by using **GetSID.exe** from the Windows NT Server 4.0 Resource Kit.

Windows NT 4.0 stores the local profile information in the registry under the following key: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList`

Under the ProfileList key, there will be subkeys named with the SIDs of the users who have logged on to this computer. (To find the profile information for the user whose locally cached profile you want to move, find the SID for the user with the **GetSID.exe** utility.) Inside the appropriate user’s subkey, you will see a string value named *ProfileImagePath*.

# ## 26.3 Mandatory Profiles

A mandatory profile is a profile that the user does not have the ability to overwrite. During the user’s session, it may be possible to change the desktop environment; however, as the user logs out, all changes made will be lost. If it is desired to not allow the user any ability to change the desktop environment, then this must be done through policy settings. See Chapter 25, “System and Account Policies”.