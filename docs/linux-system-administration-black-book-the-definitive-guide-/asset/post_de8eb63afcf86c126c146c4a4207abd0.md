
# Changing User Defaults At The Command Line

If you want to change the account creation defaults at the command line, do the following:

- 1. Log in as root.
- 2. Type “useradd -D” to display the current defaults.
- 3. Determine what defaults you want to change. The options available are listed in Table 2.3.
- 4. Build the statement by beginning it with **useradd -D**, and then add each item to be changed. For example:
  `useradd -D -g users -s /bin/ksh`
- 5. Verify that the defaults are now correct by typing “useradd -D” again.

## Changing User Defaults In GNOME

There is no specific way to change user defaults in GNOME. Instead, open a terminal window and change them at the command line.

| Related solution: | Found on page: |
|---|---|
| Getting A Command Prompt | 14 |

## Changing User Defaults In KDE

To change user defaults in KDE, do the following:

- 1. If KDE is not already started, start it by typing either “startx” or “init 5” at the command line.
- 2. Log in as root.
- 3. Click on the KDE menu icon.
- 4. Click on Utilities/Konsole to open a terminal.
- 5. Type “kuser &” and press Enter to open the KDE User Manager shown earlier in Figure 2.6.
- 6. Click on File/Preferences to pull up the Edit Defaults dialog box shown in Figure 2.13.
- 7. If you want to change the default shell, choose it from the Shell drop-down list box.
- 8. If you want to change where new home directories go, change the entry in the Base Of Home Directories text box. The directory listed in this box will be the top home directory, within which all user home directories will be created.
- 9. If you do not want user home directories to be automatically created, deselect the Create Home Dir checkbox. You might want to do this if you almost always create non-shell accounts.
- 10. If for some reason you do want a home directory created but do not want the items from the skeleton directory put into it, be sure the Copy Skeleton To Home Dir checkbox is deselected.
- 11. If you don’t want to use Red Hat’s default, which creates a new group for every user, be sure to deselect the User Private Group checkbox.
- 12. When you are finished making your changes, click on the OK button.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_74_0.png)

Figure 2.13 The KDE User Manager Edit Defaults dialog box.

## Renaming Users

Renaming a user account may involve changing the user’s name in /etc/passwd, /etc/shadow, and /etc/group. In addition, the home directory must be moved with the renamed account (unless you have reason to leave it where it is).

### Renaming Users At The Command Line

To rename a user’s account at the command line, do the following:

- 1. Log in as root.
- 2. Type “usermod -d /home/newname -m -l newname oldname”.

### Renaming Users In GNOME

To rename a user’s account in GNOME, do the following:

- 1. If GNOME is not already started, start it by typing either “startx” or “init 5” at the command line.
- 2. Log in as root.
- 3. Click on the GNOME footprint icon to open the main menu.
- 4. Click on System Linuxconf. The Linuxconf tool opens.
- 5. Find the Users Accounts option in the list on the left side of the screen.
- 6. Click on the Normal option under the Users Accounts menu.

> NOTE: Follow Steps 7 through 12 only if you are using the Red Hat default of assigning a special group to every new user or if you want to change the group name while you’re changing the rest.

- 7. Click on the Group Definitions option under the Normal menu to pull up the User Groups tab shown in Figure 2.14.
- 8. Click on the special group assigned to the account you want to rename. For example, if I wanted to change the “dog” account to “canid,” I would click on the dog group in the listing. Clicking on one of the groups opens the Group Specification tab.
- 9. Select the contents of the Group Name text box within the Group Specification tab.
- 10. Type the new name of the group.
- 11. Click on the Accept button. This action returns you to the User Groups tab shown in Figure 2.14.
- 12. Click on the Quit button to close the User Groups tab.
- 13. Click on the User Accounts option under the Normal menu to pull up the Users Accounts tab shown earlier in Figure 2.2.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_76_0.png)

Figure 2.14 The GNOME Linuxconf User Groups tab.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_76_1.png)

Figure 2.15 The GNOME Linuxconf User Information tab showing the “dog” user.

- 14. Single-click on the item you want to change within the Account list. This action pulls up the User Information tab shown in Figure 2.15.
- 15. Select the text in the Login Name text box.
- 16. Replace the current login name with the one you want to use.

**NOTE:** You can change any of the other items within the text boxes at this point as well.

- 17. Replace the current Group entry with the username or another default group you want to change the account to.
- 18. You may need to replace the account's home directory to match its new username. For example, if you changed "dog" to "canid" then you would change "/home/dog" to "/home/canid".
- 19. Click on the Accept button. This action may open the User Home Directory tab shown in Figure 2.16.
- 20. If the dialog box shown in Figure 2.16 opens, click on the Yes button to create the new home directory. This action returns you to the Users Accounts tab.

### Renaming Users In KDE

KDE does not provide a GUI-based method for renaming a user account. You will need to follow the instructions in the section “Renaming Users At The Command Line” for how to proceed.

**Related solution:**  
Getting A Command Prompt  
**Found on page:** 19

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_77_0.png)

# Disabling Users

Disabling users involves removing their access to the system without actually removing their accounts. This measure is generally used to ensure that accounts are not broken into undetected when the users should not be accessing them—say, while they are on vacation or when they are behind on payments.

## Disabling Users At The Command Line

To disable a user's account at the command line, do the following:

- 1. Log in as root.
- 2. Type `"vi /etc/passwd"`—or `"vi /etc/shadow"` if you are using shadow passwords—to open the user management file.

> **TIP:** If all the entries in /etc/passwd have an "x" for the password entry (second item), you need to look at /etc/shadow.

- 3. Locate the entry for the account you want to disable.
- 4. Change the second field in the entry to an asterisk (*). Although adding almost any single character to this field prevents anyone from logging into the account, the asterisk has a special meaning to the system. It renders the password for the account into a nonsensical string of characters.
- 5. Type `";wq"` to save and exit the file.

## Disabling Users In GNOME

To disable a user's account in GNOME, do the following:

- 1. If GNOME is not already started, start it by typing either `"startx"` or `"init 5"` at the command line.
- 2. Log in as root.
- 3. Click on the GNOME footprint icon to open the main menu.
- 4. Click on System Linuxconf. The Linuxconf tool opens.
- 5. Find the Users Accounts option in the list on the left side of the screen.
- 6. Click on Users Accounts | Normal | User Accounts to pull up the Users Accounts tab shown earlier in Figure 2.2.
- 7. Single-click on the item you want to change within the Account list. This action pulls up the User Information tab shown earlier in Figure 2.15.
- 8. Click on the The Account Is Enabled checkbox to select it.
- 9. Click on the Accept button to activate the change and return to the Users Accounts tab.

Table 2.3 Options for changing account creation defaults with useradd.

| Flag | Purpose | Valid Entries |
|---|---|---|
| b | Change the default home directory. | Path to the new home hierarchy; current value /home. |
| e | Change the default date to expire the account. | Date in the format mm/dd/yy. |
| f | Change the default wait after a password expires. If this wait time is exceeded without the password being updated, disable the account. | Number of days to wait. Enter “0” if the account should expire immediately. To not use this feature at all, enter “-1” (default). |
| g | Change the default group that new users are assigned to. | Existing group name or GID. |
| s | Change the default shell that new users are assigned to. | Path to the already installed shell. |
