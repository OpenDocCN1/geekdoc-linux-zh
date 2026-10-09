![](bbox=[0.37, 0.1, 0.75, 0.52])

Figure 16-3  The Account Properties window, User Privileges tab

# CHANGING ADVANCED USER SETTINGS

When you click the button labeled Settings, users-admin displays the Change Advanced User Settings window (Figure 16-3). This window has the following three tabs:

+   1. Contact Information tab  
+   The Contact Information tab allows you to input a location, work phone, and home phone associated with the user.

+   2. User Privileges tab  
+   The User Privileges tab (Figure 16-3) enables you to add and remove privileges for a user. Place a tick in the check box next to each of the privileges you want to grant a user; remove the tick from those privileges you do not want to grant. The most important of these privileges is **Administer the system**. Putting a tick in this box adds the user to the **admin** group, which in turn allows the user to use **sudo** (page 421) to gain root privileges. Click **OK**.

+   3. Advanced tab  
+   The Advanced tab allows you to modify the home directory, shell, group, and UID of the user. The users-admin utility fills in these values for a new user. Typically you do not need to modify these entries. This tab also allows you to disable an account (except for the first account that was set up).
+   
+   When you are finished entering information under each of the tabs for the user, click **OK**. At this point users-admin adds the user to or modifies the user on the system and closes the window, leaving the Users Settings window visible.