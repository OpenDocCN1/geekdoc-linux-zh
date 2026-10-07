# User Accounts and Login

Every user on a Linux system is listed in the file /etc/passwd. This file contains several fields of information about each user, including the user's home directory, encrypted password, and login shell. If you've installed a more secure system than the standard UNIX system (such as the shadow password system), the /etc/passwd file is not used in the same way, but the following commands and descriptions still apply.

Whenever you log in to Linux, either from a remote computer or from the Linux console, you enter your username and password. The login program compares the entries against the /etc/passwd file to see if you are granted access. If you accepted, your login shell is started (the command-line prompt appears), with the current directory being your home directory.

There are many user accounts on the Linux system that are not used by regular users to log in and work on the system. These user accounts are used by regular programs to complete various tasks. Having separate user accounts provides more security for the things we need to do.

For example, a Web server often runs as nobody, which is a standard user account on Linux. Nobody has very few rights, if someone accessing the Web server were to gain control of the Web server to execute programs, access to the system would be very limited.

There are many security issues surrounding the /etc/passwd file. People can try to decrypt passwords if they have access to this file. They may try to disable accounts or capture users' keystrokes from the log files as they enter their passwords. All these security issues are discussed in later chapters.

If you want to add new users or see what users are on your system, you can do one of the following things:

+   1. Type this command to see the names of home directories for users that actually log in to the Linux system:
   `ls -1 /home`
2. Type this command with a new username, then respond when prompted for more information:
   `adduser nickw`
3. Start the LISA administration utility:
   `lisa`
4. Select System Administration -> System Configuration -> User Administration.
5. From the User Administration, you can view all users and groups (see the next section), and complete other user-related system administration tasks.