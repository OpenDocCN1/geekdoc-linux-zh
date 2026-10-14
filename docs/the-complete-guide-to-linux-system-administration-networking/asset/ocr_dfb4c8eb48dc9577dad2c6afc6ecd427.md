# CREATING AND MANAGING USER ACCOUNTS

To complete any operation in Linux, a person must first log in using a valid user account name and password. Setting up and maintaining these user accounts is an important part of the work of a system administrator. In Chapter 3, "Using the Shell," you learned how to manage the initialization files for a user account, such as .profile and .bashrc. In Chapter 4, "Understanding Users and File Systems," you learned where user account information is stored. In this section you learn how to create new accounts and make changes in those accounts. In general, the process of creating new user accounts runs like this, though the exact steps you need to perform vary depending on the number of users you are creating, the system configuration in which you are working, and other factors:

+   1. Add default files that you want to be part of every user's home directory to the /etc/skel directory (the functioning of this directory is described later in this chapter).
+   2. Create a home directory for all users. Typically, this is /home, which is installed by default on most Linux systems, but you can also create subdirectories for groups of user accounts, such as /home/CS185 and /home/CS110.
+   3. Configure default settings to be used for all users, either in /etc/login.defs or in /etc/default/useradd (as discussed later in this chapter).
+   4. Create groups so that you can assign membership to user accounts that you create.
+   5. Create a user account for each person using either command-line or graphical utilities, as described in this section.
+   6. Create a valid password for each user and give the user that password so he or she can begin using the account.

In general, the more user accounts you have on your Linux system, the more time you will spend managing them. More users also means more security risks—thus proper management and tracking of user accounts is crucial to keeping the system secure.

# Managing User Accounts Graphically

Recall that each line in the /etc/passwd file contains fields defining a new user account. An example line might look like this one:

```
john1:x:500:500:John Lim:/home/john1:/bin/bash
```

The fields include (from left to right): the user name, a password (or an x to indicate that the shadow password system is used), a UID, a GID, a comment field (used for the full name on regular user accounts), the user's home directory, and the user's default shell.

You have learned about the vipw command that you can use to edit the /etc/passwd file directly to define a new user account. After adding a line to /etc/passwd, you need to use the passwd command to define a password, then create the home directory and add any