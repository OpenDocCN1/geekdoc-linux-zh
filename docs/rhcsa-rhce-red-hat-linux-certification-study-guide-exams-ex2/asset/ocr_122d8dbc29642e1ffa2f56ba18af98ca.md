more Linux administrators can understand, often including commands that you can run and that will address the subject problem.

To start the Browser from the GNOME desktop, click Applications | System Tools | SELinux Troubleshooter or run sealert -b from a GUI-based command line. The command is available from the setroubleshoot-server package.

# EXERCISE 4-3

# Test an SELinux User Type

In this exercise, you'll configure a user with the staff_u SELinux user type and test the results. You'll need a GUI, and at least one regular user other than the root administrative user.

+   1. If necessary, create a regular user. Even if you already have a regular user, a second regular user for the purpose of this exercise may reduce risks. Users can always be deleted, as discussed in Chapter 8. To that end, the useradd user1 and passwd user1 commands create a user named user1 with a password.
+   2. Review the SELinux types of current users with the semanage login -l command.
+   3. Configure the desired user as a staff_u user with the semanage login -a -s staff_u user1 command. Substitute as desired for user1.
+   4. If you're completely logged in to the GUI, log out. Click System | Log Out, and click Log Out in the window that appears.
+   5. Log into the GUI with the newly revised staff_u account, user1 (or whatever else you may have configured in step 3). If you don't already see a GUI login screen, press ALT+F1 or ALT+F7.
+   6. Try various administrative commands. Do you have access to the su command? What of sudo? What administrative tools discussed so far in this book are accessible? Is there a difference whether that tool is started from the GUI command line or from the GUI menu?
+   7. Log out of the new staff_u account, and log back into the regular account,
+   8. Delete the new user from the staff_u list; if that's user1, you can do so with the semanage login -d user1 command.
+   9. Confirm the restored configuration with the semanage login -l command.