Use a Web browser to access the following URL: http://apache.nice.com/chapter12. Apache will send the 401 status header and WWW-Authenticate response header to the browser with the realm (set in AuthName) and authentication type (set in AuthType) information. The browser will display a pop-up dialog box that requests a username and password.

Check whether you can get in without a username or password, by entering nothing in the entry boxes in the dialog box and pressing the OK button. This should result in an authentication failure. The browser receives the same authentication challenge again, so it displays another dialog box.

Choosing the Cancel button results in the browser's displaying the standard “Authentication Required” error message from Apache.

Pressing the Reload button on the browser requests the same URL again, and the browser receives the same authentication challenge from the server. This time, enter reader as the username, enter bought—it as the password, and press the OK button. Apache will now allow you to access the directory.

You can change the “Authentication Required” message if you want by using the ErrorDocument directive:

ErrorDocument 401 /nice_401message.html

Insert this line in your httpd.conf file and create a nice message in the nice_401message.html file.

Instead of allowing a single user called reader to access the restricted area, as demonstrated in the previous example, in the next example, you will allow anyone belonging to a group named asb_readers to access the same directory. Assume this group has two users: pikejb and bcariad. Follow these steps to give the users in group asb_readers directory access.

+   1. Create a password file called .htpasswd using htpasswd.
+      Using the htpasswd utility, create the users pikejb and bcariad.
+   2. Create a group file.
+      Using a text editor such as vi, create a file named /data/web/apache/secrets/.htgroup. This file has a single line, as follows:
+      asb_readers: pikejb bcariad
+   3. Create an .htaccess file.