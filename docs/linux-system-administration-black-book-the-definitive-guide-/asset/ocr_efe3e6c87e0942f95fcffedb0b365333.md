![](bbox=[0.0, 0.16, 0.1, 0.33])

# Changing User Defaults At The Command Line

If you want to change the account creation defaults at the command line, do the following:

+   1. Log in as root.
+   2. Type “useradd -D” to display the current defaults.
+   3. Determine what defaults you want to change. The options available are listed in Table 2.3.
+   4. Build the statement by beginning it with **useradd -D**, and then add each item to be changed. For example:
+   useradd -D -g users -s /bin/ksh

+   5. Verify that the defaults are now correct by typing “useradd -D” again.

# Changing User Defaults In GNOME

There is no specific way to change user defaults in GNOME. Instead, open a terminal window and change them at the command line.

| Related solution: | Found on page: |
|---|---|
| Getting A Command Prompt | 14 |

# Changing User Defaults In KDE

To change user defaults in KDE, do the following:

+   1. If KDE is not already started, start it by typing either “startx” or “init 5” at the command line.

Table 2.3 Options for changing account creation defaults with useradd.

| Flag | Purpose | Valid Entries |
|---|---|---|
| b | Change the default home directory. | Path to the new home hierarchy; current value /home. |
| e | Change the default date to expire the account. | Date in the format mm/dd/yy. |
| f | Change the default wait after a password expires. If this wait time is exceeded without the password being updated, disable the account. | Number of days to wait. Enter “0” if the account should expire immediately. To not use this feature at all, enter “-1” (default). |
| g | Change the default group that new users are assigned to. | Existing group name or GID. |
| s | Change the default shell that new users are assigned to. | Path to the already installed shell. |