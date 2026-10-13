# EXERCISE 8-2

# Real and Fake Shells

Do not run this exercise unless a regular user has already been created on the local system. Otherwise, an error might require a cold restart of the system. If desired, run Exercise 8-1 first, as that allows you to create a new regular user on the target system.

+   1. Open the /etc/passwd file. Find a current regular user, with a UID of 500 or above.
+   2. Identify the default shell. It's specified in the last column, normally /bin/bash for regular users.
+   3. Change the default shell to /sbin/nologin, and save the changes to the /etc/passwd file.
+   4. Open a different console. Press the CTRL-ALT-F2 keys to open a different console. (If you're already in the second virtual console, substitute F3, F4, F5, or F6 for F2. If you're in a KVM-based VM in the GUI, you can move to the second virtual console by clicking Send Key | CTRL-ALT-F2.
+   5. Try logging in as the modified user. What happens?
+   6. Return to the original console. If it's the GUI, it should be accessible with either the ALT-F1 or ALT-F7 key combinations. If that is not possible (such as when the GUI is not installed), you should still be able to log in as the root administrative user.
+   7. Reopen the /etc/passwd file. Restore the /bin/bash shell to the target regular user.

# Delete a User

The removal of an user account is a straightforward process. The easiest way to delete a user account is with the userdel command. By default, this command does not delete that user's home directory, so administrators can transfer files from that user perhaps to an employee who has taken over the tasks of the deleted user. Alternatively, the userdel -r username command deletes that user's home directory along with all of the files stored in that home directory.