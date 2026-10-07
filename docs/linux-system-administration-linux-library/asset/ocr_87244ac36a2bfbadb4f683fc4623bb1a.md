# Adding New Users

To add a new user to the system, you must have root access, and you must follow a series of general steps. The required steps are:

+   1. Create a record for the user in /etc/passwd.
2. Set the user's password.
3. Specify a login shell for the user.

There are also two optional steps. These help to configure a useful environment, but all account types require these steps. They are:

+   4. Create a home directory for the user.
5. Populate the user's home directory with various useful files. (This step isn't described because it is very system-specific. You might want to add a README file, for instance, for the benefit of new users.)

You perform these as discrete steps, but you can ease your administrative burden by automating the process using either user-creation scripts, which have existed for years, or graphical user interfaces, which have appeared more recently.

# Adding a User from the Linuxconf GUI

For the simplest default accounts, many administrators find it best to work with the command line, simply switching to the useradd and passwd commands, as described in the next section. To create accounts that include nonempty defaults, however, you may prefer to work with a GUI, such as Linuxconf. In particular, creating any of the special accounts mentioned earlier in this chapter from Linuxconf takes care of the peculiarities of that account's specific authentication sequence. For that reason, creating these accounts is most easily done with the Linuxconf tool. The format of the GUI itself provides excellent cues for the optional fields.

In order to create a user account using Linuxconf under a Red Hat Linux system, simply invoke the utility from a root shell in either the X Window System or a text console by typing `linuxconf`. If you invoke Linuxconf when you're running X, the program conducts an X-based display. You can run it without X, however, in which case the program produces a text-mode display.

Once the Linuxconf screen comes up, you'll need to select Accounts > Users from the menu. Doing so will expand the window and bring a list of users on the right side of the Linuxconf window, as shown in Figure 6.1. To add a user, click the Add button. You'll then be presented with the User Account Creation screen shown in Figure 6.2.