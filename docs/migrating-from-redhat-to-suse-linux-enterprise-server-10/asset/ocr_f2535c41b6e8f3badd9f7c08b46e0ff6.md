You can use the following in this dialog to add local users to the system (account information is stored in the files **/etc/passwd** and **/etc/shadow**):

+   -   **User Data.** Enter the full user name, the login name, and the password.
+   
+       To provide effective security, a password should be 8 or more characters long. The maximum length for a password ranges from 8 to 128 characters, depending on the algorithm used to hash the password. While the Crypt algorithm commonly used in the past used only the first eight characters of the password, more recent algorithms allow longer passwords.
+   
+       Passwords are case-sensitive. Special characters are allowed, but they might be hard to enter depending on the keyboard layout.

+   -   **Password Settings.** Select this option to change advanced password settings (such as password expiration). The default settings are suitable in most cases.

+   -   **Details.** Select this option to edit details of the user account. The default settings are suitable in most cases.

+   -   **Receive System Mail.** Select this option to forward all emails addressed to root to this user.

+   -   **Automatic Login.** Select this option to enable automatic login for this user. This option logs in the user automatically (without requesting a password) when the system starts.
+   
+       You should not enable this feature on a production system.

+   -   **User Management.** Select this option to add more users (with the YaST User Management module).

> You can add other users later (after installation), but you have to create at least one user during installation so you don't have to work as the user root after the system has been set up.

**1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED**