Disable: Only Allow Local User Profiles
Disable: Prevent Roaming Profile Change from Propagating to the Server

**Change of Profile Type:** From the start menu right-click on the **My Computer** icon, select **Properties**, click on the **User Profiles** tab, select the profile you wish to change from **Roaming** type to **Local**, and click on **Change Type**.

Consult the MS Windows registry guide for your particular MS Windows version for more information about which registry keys to change to enforce use of only local user profiles.

> **NOTE**
> 
> The specifics of how to convert a local profile to a roaming profile, or a roaming profile to a local one, vary according to the version of MS Windows you are running. Consult the Microsoft MS Windows Resource Kit for your version of Windows for specific information.

# ### 26.2.2 Windows Client Profile Configuration Information

# #### 26.2.2.1 Windows 9x/Me Profile Setup

When a user first logs on in Windows 9x, the file user.DAT is created, as are folders **Start Menu**, **Desktop**, **Programs**, and **Nethood**. These directories and their contents will be merged with the local versions stored in c:\windows\profiles\username on subsequent logins, taking the most recent from each. You will need to use the \[global\] options `preserve case = yes, short preserve case = yes`, and `case sensitive = no` in order to maintain capital letters in shortcuts in any of the profile folders.

The user.DAT file contains all the user's preferences. If you wish to enforce a set of preferences, rename their user.DAT file to user.MAN, and deny them write access to this file.

+   1.  On the Windows 9x/Me machine, go to **Control Panel -> Passwords** and select the **User Profiles** tab. Select the required level of roaming preferences. Press **OK**, but do not allow the computer to reboot.
+   2.  On the Windows 9x/Me machine, go to **Control Panel -> Network -> Client for Microsoft Networks -> Preferences**. Select **Log on to NT Domain**. Then, ensure that the Primary Logon is **Client for Microsoft Networks**. Press **OK**, and this time allow the computer to reboot.

Under Windows 9x/Me, profiles are downloaded from the Primary Logon. If you have the Primary Logon as “Client for Novell Networks”, then the profiles and logon script will be