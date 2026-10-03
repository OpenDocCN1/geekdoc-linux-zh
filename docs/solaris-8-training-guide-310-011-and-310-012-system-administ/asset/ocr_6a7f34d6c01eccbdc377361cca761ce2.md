# APPLY YOUR KNOWLEDGE

# Exercises

# 19.1 Using AdminSuite

In this exercise, you use AdminSuite to add a new user account.

Estimated Time: 10 minutes

+   1. Log in as root, and start up AdminSuite as follows:
   `/opt/SUNWseam/3_0/bin/admapp &`
2. When the AdminSuite Log On screen appears, select the local system and fill in the empty fields:
   User Name: root
   Password: `<root password>`
3. From the AdminSuite main window, click the Users icon.
4. Click the User Accounts Icon in the right pane.
5. With the User Accounts icon still highlighted, click the Action button located in the toolbar in the right pane.
6. From the pull-down menu, click Add User.
   A wizard for setting up the new user account appears.
7. In the first window that appears, fill in the fields as follows:
   User Name: admin1
   Full Name: Administrative Assistant
8. Click the right arrow located at the bottom of the window to continue.

+   9. In the next window, accept the default User ID number that is assigned, and click the right arrow to continue.
10. In this window, click the radio button next to User Must Use This Password At First Login. Then, assign a password in the Password fields, and click the right arrow to continue.
11. In the next two windows, you are prompted for a Primary group and home directory for the new user account. Accept the defaults that are presented.
12. A summary window follows. Click Finish on the summary window, and the new user account is set up.

# 19.2 Using the Solaris Management Console

In this exercise, you add an administrative role in the Solaris Management Console and delegate administrative tasks to a non-root user.

Estimated Time: 15 minutes

+   1. For this exercise, you need an account for a non-root user named `admin1`. Create a new account for `admin1` with a group ID of 10.
2. As root, start up the Solaris Management Console as follows:
   `smc &`
3. Click This Computer in the navigation pane of the Console window. Then click the System Configuration tool and the Users tool. When the Log In window appears, enter root as the username, and enter the root password. Click the OK button to continue.