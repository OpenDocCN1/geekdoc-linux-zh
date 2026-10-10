Likewise, you can drag an application from the Window List to move that application to another workspace.

+   - **Add more workspaces** — Right-click the Workspace Switcher, and select Preferences. You can add workspaces (up to 32).

+   - **Name workspaces** — Right-click the Workspace Switcher and select Preferences. Click in the Workspaces pane to change names of workspaces to any names you choose.

You can view and change information about Metacity controls and settings using the `gconf-editor` window (as root, type **yum install gconf-editor**, then **gconf-editor** as a regular user from a Terminal window). As the window says, it is not the *recommended* way of changing preferences. So, when possible, you should change the desktop through GNOME preferences. However, `gconf-editor` is a good way to see descriptions of each Metacity feature.

From the `gconf-editor` window, select **apps** \u2192 **metacity**. Then choose from **general**, **global_keybindings**, **keybindings_commands**, **window_keybindings**, and **workspace_names**. Click each key to see its value, along with short and long descriptions of the key.

# ## Switching to another user

If you want to log in as another desktop user without closing your current desktop session, you can use the Fast User Switch feature of GNOME. Look for the User Switcher applet in your top panel (by default, it should show your name on the applet) or add the applet yourself (it’s identified as User Switcher from the Add to Panel window).

To use Fast User Switch, click the User Switcher panel and select **Quit**. Choose **Switch User** to see a list of user names on your system. To log in as one of those users, click on the name and log in (when the login screen appears). A desktop for the new user appears, while the previous desktop keeps running on a different virtual terminal.

After you have logged in and started a desktop for another user, you can use the same User Switcher applet to switch between the multiple user desktops. A check box appears next to the names of users that have desktops launched on the different virtual terminals accessible from your display.

# ## Exiting GNOME

When you are done with your work, you can either log out from your current session or shut down your computer completely. If you have multiple user sessions open, you should log out of each of those first (to make sure you don’t lose any unsaved work.)

To exit from GNOME, do the following:

+   1. Click the **System** button from the panel.
+   2. Select **Log Out** from the menu. A pop-up window appears, asking if you want to Log out.