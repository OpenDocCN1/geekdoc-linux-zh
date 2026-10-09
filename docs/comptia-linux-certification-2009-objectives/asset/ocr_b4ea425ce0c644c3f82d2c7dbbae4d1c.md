+   4. Configure Apache to authenticate users.

+   a. Using the vi editor, open the .htaccess file.

+   b. Enter Authname "This is a trusted website." to specify the message to be displayed in the authentication dialog box.

+   c. Enter Authuserfile "/var/www/html/.htpasswd" to indicate the name of the file that contains details about users who have access to the website.

+   d. Enter Authtype basic to specify the type of authentication.

+   e. Type require valid-user to specify that all valid users can access the website.

See Code Sample 3.

+   f. Press Esc to switch to the command mode.

+   g. Save and close the file.

+   h. Clear the terminal window.

# Code Sample 3

```
Authname "This is a trusted website."
Authuserfile "/var/www/html/.htpasswd"
Authtype basic
require valid-user
```