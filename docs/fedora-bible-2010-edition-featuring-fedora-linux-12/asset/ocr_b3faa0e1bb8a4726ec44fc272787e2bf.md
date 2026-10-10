**Guest Account** — Set this field to a user name that you want assigned to requests from anonymous users. Even with User mode security set globally, you can assign guest access to particular Samba shares (such as printers).

With User mode security (which is being used in this example), any user who wants to access a Samba share must have a regular user account on the Linux system. (Refer to Chapter 10 for information on adding user accounts.)

![](bbox=[0.23, 0.22, 0.66, 0.48])

+   6. To add a user as a Samba user (that is, one who can access your Samba server), select Preferences → Samba Users. The Samba Users window appears.
+   7. Click Add User. The Create New Samba User window appears.
+   8. Provide information for the following fields in the Create New Samba User window and click OK:
+   * **Unix Username** — Click this check box, and then select the Linux user name to which you want to give access to the Samba server.
+   * **Windows Username** — This is the user name provided by the user when he or she requests the shared directory. (Often, it is the same as the Unix Username.)
+   * **Samba Password** — Type the Samba password, and then retype it into the Confirm Samba Password field.
+   9. Repeat the previous step for each user you want to access the Samba shared directory.
+   10. Now that you have configured the default values for your Samba server, add a directory to share by clicking File → Add Share. The Create Samba Share window appears.
+   11. Fill in the following fields shown in the Create Samba Share window:
+   * **Directory** — Type the name of the directory you want to share.
+   * **Description** — Type any description you like of the Shared directory.