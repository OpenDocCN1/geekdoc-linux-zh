# Disabling Users

Disabling users involves removing their access to the system without actually removing their accounts. This measure is generally used to ensure that accounts are not broken into undetected when the users should not be accessing them— say, while they are on vacation or when they are behind on payments.

# Disabling Users At The Command Line

To disable a user's account at the command line, do the following:

+   1. Log in as root.
+   2. Type `"vi /etc/passwd"`—or `"vi /etc/shadow"` if you are using shadow pass- words—to open the user management file.

> **TIP:** If all the entries in /etc/passwd have an "x" for the password entry (second item), you need to look at /etc/shadow.

+   3. Locate the entry for the account you want to disable.
+   4. Change the second field in the entry to an asterisk (*). Although adding almost any single character to this field prevents anyone from logging into the account, the asterisk has a special meaning to the system. It renders the password for the account into a nonsensical string of characters.
+   5. Type `";wq"` to save and exit the file.

# Disabling Users In GNOME

To disable a user's account in GNOME, do the following:

+   1. If GNOME is not already started, start it by typing either `"startx"` or `"init 5"` at the command line.
+   2. Log in as root.
+   3. Click on the GNOME footprint icon to open the main menu.
+   4. Click on System|Linuxconf. The Linuxconf tool opens.
+   5. Find the Users Accounts option in the list on the left side of the screen.
+   6. Click on Users Accounts|Normal|User Accounts to pull up the Users Accounts tab shown earlier in Figure 2.2.
+   7. Single-click on the item you want to change within the Account list. This action pulls up the User Information tab shown earlier in Figure 2.15.
+   8. Click on the The Account Is Enabled checkbox to select it.
+   9. Click on the Accept button to activate the change and return to the Users Accounts tab.