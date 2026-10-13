![](bbox=[0.1, 0.17, 0.18, 0.25])

> Be security conscious when working with multiple consoles. It is easy to forget that multiple consoles and user accounts are open. Before you leave the computer, check each console to make sure that no users are logged in. This helps to prevent unauthorized entry into the system.

# Task: Exploring the Login Process

Before you can drive your new operating system around the block, you'll need to turn the key to start the engine. Your key is your username and password. Follow these steps to learn how to log in to the superuser account and your unprivileged user account:

+   1. Access the superuser account. At the login prompt, type root and press Enter. The password prompt will appear.
+   2. Type the root password and press Enter. The shell prompt for the root user account displays and might look something like the following:
+      `[root@localhost /root]#`
+   3. Change to a different console. Press Alt+F2.
+   4. Access your user account. At the login prompt, type the username for the unprivileged user account that you set up during the installation and press Enter. You will be asked for the account's password. Type the password and press Enter.
+   5. Temporarily change to the superuser account from the unprivileged user account. Type su and press Enter. You'll be asked for the password for the root user account. Type the password and press Enter. The shell prompt will look something like the following:
+      `[root@localhost rusty]#`
+   6. Exit the superuser account. Type exit and press Enter. You'll be returned to your user account and once again the shell prompt might look like the following:
+      `[rusty@localhost rusty]$`

You'll want to do your daily work from this user account. To get back to the console at which the root user is logged in, press Alt+F1.

# Troubleshooting the Installation

You might need some extra help during the installation. There are a number of places where you can find some good information. One good source is the Linux HOWTOs. You might find these in the filesystem, but if not there, they are on the Web at www.linuxdocs.org. Here's a list of Linux HOWTOs that you might find useful: