In order to install packages on a Red Hat Linux system, you need to be root. If you're logged into a user account, you need to log out and log again as root. You also need to be at a command prompt; if you're in some sort of windowed system, you need to either exit to a command prompt, or open a terminal window.

+   1.  At the command prompt, type the following command:
+       rpm -ivh <package name>.rpm
+       The v and h flags are optional, but they give you some visual feedback that lets you keep track of how your installation is going.
+   2.  Repeat the command for each package you want to install.
+   3.  Log out of the root account.
+   4.  Log back in to your user account.
+   5.  Type *usekde* at the command prompt.
+       A couple of system messages show up on your screen while your computer sets KDE as your default user interface. As soon as the messages stop, you're ready to test.
+   6.  Type *startx* to start the X Window System.
+       If you're already running X Windows for some reason, shut it down and restart it.
+       If KDE opens, you've successfully installed it! Congratulations!

If KDE is not running, something went wrong during the installation. Try re-installing, following this procedure to the letter. If it still fails, go back a step, re-download the packages, and reinstall. If that doesn't work, consult Chapter 16 for more advanced sources of help.

# Installing KDE on a Debian Linux system

Debian packages install according to the FHS, or File Hierarchy Standard.
As with Red Hat, Debian installations require that you work from a command line and that you be logged in as root. If you are currently logged into a user account, log out and back in again with your root password.

+   1.  At the command prompt, type the following command:
+       dpkg -i <package name>.deb
+   2.  Repeat the command for each package you want to install.
+   3.  Log out of the root account.
+   4.  Log back into your user account.