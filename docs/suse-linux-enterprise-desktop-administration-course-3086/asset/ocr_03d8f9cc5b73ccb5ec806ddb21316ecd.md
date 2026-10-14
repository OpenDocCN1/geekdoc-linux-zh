The next time the user logs in to GNOME, the deleted GConf files are copied back into the user's home directory.

Therefore, Sabayon should be considered a means to provide a stable configuration that can easily be restored by logging out and in again rather than a way to restrict users.

![](bbox=[0.05, 0.25, 0.18, 0.38])

# Exercise 14-3: Set Mandatory Values for Preferences

In this exercise, you use the Desktop Profile Editor to set mandatory preferences.
Use the Desktop Profile Editor (Sabayon) to lock the screen of all users after five minutes of inactivity.

# Detailed Steps to Complete This Exercise

To set mandatory preferences, do the following:

+   1. On the GNOME desktop, select Computer > More Applications > System > Desktop Profile Editor. Enter the root password (n0v311) in the dialog that appears.
+   2. In the User Profile Editor dialog, select Add. Then, in the Add Profile dialog, enter penguins as the profile name; then select Add.
+   3. Select Edit; an xnest window opens.
+   4. In this window, select Computer > Control Center > Screensaver. Move the Set Session as Idle After slider to 5 minutes.
+      Also toggle the settings for Activate screen saver when session is idle and Lock screen when sreensaver is active off and on once.
+      Close the dialog.
+   5. In the menu of the xnest window, select Edit > Changes.
+      Click on the locks in front of the entries that set the idle_delay key to 5 minutes, activate the screen saver when the session is idle, and lock the screen when the screen saver is active.
+   6. In the menu of the xnest window, select Profile > Save. Close the xnest window.
+   7. In the User Profile Editor window, make sure penguins is selected; then select Users.
+   8. In the Users for Profile Penguins dialog, select Use This Profile for All Users.
+   9. Log out from the GNOME desktop. Log in again. Try to change the screen saver settings.

![](bbox=[0.07, 0.85, 0.22, 0.95])

If you can still edit the screen saver settings, open a terminal window, killall gconfd-2, delete .gconf* directories and files, and log out and back in again. Then try again to change the screen saver settings.