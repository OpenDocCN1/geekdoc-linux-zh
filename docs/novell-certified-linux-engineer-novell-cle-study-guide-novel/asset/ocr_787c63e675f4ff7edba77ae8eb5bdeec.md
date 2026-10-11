Install the Pure-FTP service on your server by completing the following steps:

+   1. Start YaST on your server by selecting **Applications**, **SUSE Menu**, **System**, **YaST2**.
+   2. When prompted, supply your root user's password (**novell**).

> When you do this, you'll notice that YaST returns a password error but runs anyway. You can safely disregard the error message.

+   3. Select **Install or Remove Software**.
+   4. In the **Filter** drop-down list, select **Package Groups**.
+   5. Select **zzz All**.
+   6. In the top-right frame, scroll down to and select **pure-ftpd**.
+   7. Click **Accept**.
+   8. When prompted, insert **UnitedLinux 1.0 CD #2** and then click **OK**.
+   9. Wait while the package is installed.
+   10. When the installation is complete, click **Close**.

Follow these steps to manage the pure-ftpd service on your server:

+   1. Open a terminal session and change to your root user account by entering `su -` and supplying a password of **novell**.
+   2. At the shell prompt, enter `cd /etc/init.d`.
+   3. Enter `ls`. You should see a script for the pure-ftpd daemon, as shown in Figure 3.32.

![](bbox=[0.15, 0.68, 0.64, 0.93])

# **FIGURE 3.32**
The pure-ftpd script.