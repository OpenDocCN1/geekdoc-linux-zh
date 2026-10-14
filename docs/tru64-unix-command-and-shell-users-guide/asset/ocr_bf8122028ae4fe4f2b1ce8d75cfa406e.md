+   - Character restrictions
+     - Minimum number of alphabetic characters
+     - Minimum number of other characters, such as punctuation or numbers
+     - Minimum number of characters in a new password that must be different from the old password
+     - Maximum number of consecutive duplicate characters allowed in a password
+   - Time restrictions
+     - Maximum number of weeks before your password expires
+     - Number of weeks before you can change a password

See your system administrator for more information about password restrictions. There are several levels of security and access control that may be installed or activated on your system. See the Security manual for additional information about access control.

# 1.5.2 Password Procedures

To set or change your password, follow these steps:

+   1. Enter the passwd command:
+      $ passwd
+      The system displays the following message (identifying you as the user) and prompts you for your old password:
+      Changing password for username
+      Old password:
+      If you do not have an old password, the system does not display this prompt. Go to step 3.
+   2. Enter your old password. For security reasons, the system does not display your password as you enter it.
+      After the system verifies your old password, it is ready to accept your new password, and displays the following prompt:
+      New password:
+   3. Enter your new password at the prompt.
+      Remember that your new password entry does not appear on the screen. Finally, to verify the new password (since you cannot see it as you enter), the system prompts you to enter the new password again:
+      Retype new password: