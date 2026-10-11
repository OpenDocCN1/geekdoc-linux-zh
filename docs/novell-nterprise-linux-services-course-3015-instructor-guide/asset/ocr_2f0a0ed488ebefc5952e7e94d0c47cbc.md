+   10. For Automatic Sync, select **Enforced**.

+   11. For Save Pass Phrase, select **Hidden**.

+   12. For Sync to Server Delay, enter **30**; then select **Enforced**.

+   13. For iFolder Location, select **Hidden**.

+   14. Select **Update**.

+   15. Return to the _terminal session_; then enter `tail index.html`.
+   Note the debug output that was captured. Return to and refresh this window any time you want to see what kind of information is logged when iFolder events take place (i.e., logging out and back in, synchronizing files, etc.)

+   16. (Optional) In the File Manager - Super User Session, you can browse to and double-click the index.html file to see its full content and refresh it when needed.

+   17. Test the new configuration for the iFolder user:
+   a. From your Windows workstation, log out of the iFolder client by doing one of the following:
+   - If your iFolder client dialog is open, select **File** > **Logout**.
+   - If your iFolder client dialog is closed, right-click the iFolder client icon in the system tray; then select **Logout**.
+   b. Log in to your iFolder user by right-clicking on the _iFolder icon_ in the system tray; then select **Login**.
+   c. For the iFolder user you changed settings for, enter the _user ID_ and **novell** for the password; then select your server DNS name from the drop-down list.
+   d. Select **Login**.
+   e. For the pass phrase, enter **novell**; then select **OK**.
+   f. Right-click the iFolder client icon; then select **Account Information**.