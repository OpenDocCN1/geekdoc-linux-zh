Assume that a new employee named Jenny Barnes will be taking over Mary's job. We want to convert the mary account to a new name (-1 jenny), new comment (-c "Jenny Barnes"), and home directory (-d /home/jenny). We could do that with the following command:

```
# usermod -l jenny -c "Jenny Barnes" -d /home/jenny mary
```

Furthermore, if after converting the account we learn that Jenny prefers the tcsh shell, we could make that change with the -s option (-s /bin/tcsh):

```
# usermod -s /bin/tcsh jenny
```

Alternatively, we could use the chsh command to change the shell. The following is an example:

```
# chsh -s /bin/tcsh jenny
```

The chsh command is handy because it enables a user to change his or her own shell setting. Simply leave the user name parameter off when invoking the command, and chsh assumes the currently logged-in user as the account to change.

# Modifying user accounts with Red Hat User Manager

To use the desktop to change an existing account, you can use the Red Hat User Manager. Here's how to add a new user from the Red Hat User Manager window:

+   1. From the GNOME desktop, click on Programs → System → User Manager (or type redhat-config-users from a Terminal window as root user). The main Red Hat User Manager window appears.

+   2. Click on the user name of the account you want to modify, then select Action → Properties. A User Properties window appears, as shown in Figure 11-3:

![](bbox=[0.07, 0.62, 0.45, 0.82])

+   3. There are four tabs of information you can modify for the user you selected:

+   * User Data — This tab contains the user information you created when you first added the user account.