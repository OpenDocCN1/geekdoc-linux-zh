each dialog box to back out of the menu hierarchy. When you come to a dialog box labeled Status of the system, press [Enter] to take the default action, which is to apply the changes you've made.

At this point, Web-based access has been enabled. To test it out, go to one of the systems that you added to the access control list. Launch your Web browser, and enter the following URL:

```
http://<host>:98/
```

(Replacing <host> with your system's hostname, of course.)

You should see the main Linuxconf page. Note that you will need to enter your system's root password to gain access beyond the first page.

# Adding a User Account — Quick Reference

+   1. Start Linuxconf by typing linuxconf at the shell prompt
+   2. Open [Config] -> [Users accounts] -> [Normal] -> [User accounts]
+   3. Select Add
+   4. Enter the account's login and full names
+   5. Enter information in other fields only as necessary
+   6. Select Accept
+   7. Enter the initial password for the account
+   8. Reenter the initial password for the account in the Confirmation field
+   9. Select Accept

# Adding a User Account — General Overview

Adding a user is one of the most basic tasks you will encounter in administering your system. To add a user:

+   - Start Linuxconf by typing linuxconf at the shell prompt.
+   - Open [Config] -> [Users accounts] -> [Normal] -> [User accounts] This will open the Users accounts tab (see figure 8-3).
+   - If you have more than 15 accounts on the system, Linuxconf will provide you with a filter screen (see figure 8-2). You can use this to select a smaller range of