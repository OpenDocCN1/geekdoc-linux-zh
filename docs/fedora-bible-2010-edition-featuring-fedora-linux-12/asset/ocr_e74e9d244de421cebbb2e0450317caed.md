![](bbox=[0.16, 0.1, 0.87, 0.39])

# Administering a Mailing List with mailman

Mailman is a popular open source package for managing e-mail discussion lists. Besides offering flexible administrative interfaces for setting up and managing lists, it also has Web-based interfaces that make it easy for people to join lists, access discussion list archives, and tune their own preferences.

If you need more information about configuring mailman, there are plenty of places to go. Check the mailman Web site at www.gnu.org/software/mailman/mailman.html. Also view README files in /usr/share/doc/mailman-*. 

> **NOTE:** If you used mailman previously in an earlier version of Fedora, note that the mailman installation directory has moved from /var/mailman to /usr/lib/mailman. If you made any changes to files in the /var/mailman directory, you need to move those files to the /usr/lib/mailman directory after you upgrade the mailman software package.

The following is a brief procedure for configuring a discussion list using mailman:

+   1. Install the mailman RPM by running yum install mailman.

+   2. Start your Web server (if it isn't already running) as follows:
+   
+   ```bash
+   # service httpd start
+   # chkconfig httpd on
+   ```

+   3. Create a password for your site as follows:
+   
+   ```bash
+   # /usr/lib/mailman/bin/mmsitepass
+   New site password: *****
+   Again to confirm password: *****
+   ```