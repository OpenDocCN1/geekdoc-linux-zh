
2. Log in as root.
3. Click on the GNOME footprint icon to open the main menu.
4. Click on the System menu.
5. Click on the Linuxconf item on the System menu. The Linuxconf tool opens.
6. Find the Users Accounts option in the list on the left side of the screen.
7. Click on Users Accounts/Normal/User Accounts to pull up the Users Accounts tab shown in Figure 2.2.
8. Click on the Add button to open the User Account Creation tab shown in Figure 2.3.
9. The only field that you must fill in is the first, Login Name. Fill in the user's account name here. If you want to leave everything else to their defaults, skip to Step 16.
10. If you want to, add a full name or nickname for the user account in the Full Name field.
11. If you want to assign the account to a primary group that is not the default user group—identical to the user's login name—then enter the group's name in the Group text box. There is also a drop-down list box available for you to click on and choose from if you want to use an existing group.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_61_0.png)

Figure 2.2 The GNOME Linuxconf Users Accounts configuration tab.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_62_0.png)

Figure 2.3 The GNOME Linuxconf User Account Creation tab.

12. If you want the user to belong to other groups as well, as listed in /etc/group, enter these group names in the Supplementary Groups field.
13. If you want to use a home directory that is not /home/loginname, then enter the path to the directory in the Home Directory field.
14. If you do not want the account to use the default (bash) shell, then enter the path to the shell in the Command Interpreter field.
15. If you want to use a specific UID instead of the next one in line, then type that number into the User ID field.
16. Click on the Accept button to pull up the Changing Password tab shown in Figure 2.4.
17. Type the user's default password into the New UNIX Password field.
18. Click on the Accept button to test the password for its security soundness.
19. If the password is detected to be a security risk, you will get the Error tab shown in Figure 2.5. If not, skip to Step 21.
20. Click on the Ok button to close the Error tab and open the Changing Password tab. Type the password again in the Retype New UNIX Password field. However, I recommend that you choose a more secure password.

> Remember: Passwords are a system's first line of defense.

21. Click on the Accept button to complete the account addition process.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_63_0.png)

Figure 2.4 The GNOME Linuxconf Changing Password tab.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_63_1.png)

Figure 2.5 The GNOME Linuxconf Error tab.

**Related solution:** Setting Password Rules | **Found on page:** 285

## Creating Shell Accounts In KDE

To create a full shell account in KDE, do the following:

1. If KDE is not already started, start it by typing either "startx" or "init 5" at the command line.
2. Log in as root.
3. Click on the KDE menu icon.
4. Click on Utilities/Konsole to open a terminal.
5. Type "kuser &" and press Enter to open the KDE User Manager shown in Figure 2.6.
6. Click on User/Add to open the Enter Username dialog box, as shown in Figure 2.7.
7. Type in the username for the new account.
8. Click on OK to pull up the User Properties dialog box, shown in Figure 2.8.
9. Fill in the fields of information you want to assign to the user.
10. Choose a shell in the Login Shell drop-down list box. The standard Linux shell is /bin/bash.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_64_0.png)

Figure 2.6 The KDE User Manager dialog box.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_64_1.png)

Figure 2.7 The KDE User Manager Enter Username dialog box.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_65_0.png)

Figure 2.8 The KDE User Manager User Properties dialog box for the user “dog”.

11. Keep the defaults of having the Create Home Directory and Copy Skeleton items checked, as well as the User Private Group, unless you want this particular user only to be added to the users group in /etc/group.
12. Click on the Set Password button to open the Enter Password dialog box.
13. Click on OK to accept the password.
14. Click on OK to close the User Properties dialog box.
15. Click on File/Quit to bring up the Data Was Modified dialog box shown in Figure 2.9.
16. Click on the Save button to save the changes and close the User Manager.

| **Related solution:** | **Found on page:** |
| --- | --- |
| Getting A Command Prompt | 19 |

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_65_1.png)

Figure 2.9 The KDE User Manager Data Was Modified dialog box.

## Creating Restricted Access Accounts

Creating a restricted access account can be trickier than adding a standard, full user shell account. Some tools are provided in the GUI, but making the account from the command line is a fairly quick procedure.

### Creating Restricted Access Accounts At The Command Line

To add a restricted access account at the command line, do the following:

1. Log in as root.
2. Type "vi /etc/passwd" to open the account management file.
3. Type "G" to go to the end of the file.
4. Type "o" to open a new line below the cursor, and go into Insert mode.
5. Create an entry for the user. Because restricted access tends to mean "no shell access," be sure to assign the /bin/false shell. Also, do not assign a home directory to the user. If the last user in the file is UID and GID 560, then the entry might look like this:

```
cat::561:561:House Kitty:/dev/null:/bin/false
```

> TIP: The location /dev/null in Unix and Linux stands for "throw it away."

6. Press the Esc key and then type ":wq" to save and exit the file.
7. Type "vi /etc/shadow" to edit the shadow password file if you are using the shadow suite—the file will not exist if you do not have the suite activated. You need to add an entry there, too, because the shadow suite directs programs that need to authenticate users to the shadow file. For more on this file, see Chapter 9.

> NOTE: You only need to edit /etc/shadow if you have the shadow suite enabled. The file will not exist if the suite is not in use. In all sections previous to this under the Immediate Solutions, the programs that handled your user creation work also handled /etc/shadow for you, so this aspect was handled transparently.

8. Type "G" to go to the end of the file.
9. Type "o" to open a new line below the cursor, and go into Insert mode.
10. Add a line in the format “loginname:……”: For example, for the cat user mentioned earlier, it would be “cat:……”:

> NOTE: There are eight colons (:), one for each /etc/shadow field, as explained in Chapter 9.

11. Press the Esc key and then type “:wq!” to save and exit the file. The exclamation point (!) is necessary to override the read-only setting for /etc/shadow.
12. Add the user’s password by typing “passwd *loginname*.”
13. Enter the user’s default password. Make it a secure one or one that has been chosen already. The user can’t get to a shell prompt to change it.
14. Enter it again to check for typos.
15. If you want to be doubly sure, type “tail /etc/passwd” to confirm that there is now an “x” in the password field of the user’s entry. Then type “tail /etc/shadow” to see that all of the fields for the user are now filled in.

> **TIP:** The *useradd* command also has flags that you can use to create some types of restricted access accounts. Typing “useradd *loginname* -N -g *opusers* -s */bin/false*” will create a POP-only account with no home directory.

### Creating Restricted Access Accounts In GNOME

To create a restricted access account in GNOME, do the following:

1. If GNOME is not already started, start it by typing either “startx” or “init 5” at the command line.
2. Log in as root.
3. Click on the GNOME footprint icon to open the main menu.
4. Click on the System menu.
5. Click on the Linuxconf item on the System menu. The Linuxconf tool opens.
6. Find the Users Accounts option in the list on the left side of the screen.
7. Click on the plus next to the Special Accounts submenu if necessary to expand it.
8. Click on one of the menu items listed in Table 2.1.

**Table 2.1** *Choices in the Linuxconf Special Accounts submenu*.

| Option | Purpose |
| --- | --- |
| POP | The account needs access to POP email, but not a shell. |
| PPP | The account needs dial-in access to use PPP through the server, but no shell. |
| SLIP | The account needs dial-in access to use SLIP through the server, but no shell. |
| UUCP | The account needs dial-in access to use UUCP through the server, but no shell. |
| Virtual POP | The account needs access to POP email for a virtual domain, but not a shell. |
